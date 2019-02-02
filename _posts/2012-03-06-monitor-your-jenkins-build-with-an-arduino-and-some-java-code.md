---
id: 1092
title: Monitor your Jenkins build with an Arduino (and some Java code)
date: 2012-03-06T22:35:45+00:00
author: deline
layout: post
guid: http://www.delineneo.com/?p=1092
permalink: /2012/03/monitor-your-jenkins-build-with-an-arduino-and-some-java-code/
categories:
  - Programming
tags:
  - arduino
  - java
---
So I got my hands on an Arduino kit a while back but hadn&#8217;t played around with it much. Whilst I await for some books to arrive so I can learn basic electronics and circuits (am a developer without engineering/electronics background&#8230;) I thought it&#8217;d be fun to see if I could write something simple that could be useful in my day to day job as a Java developer.

One of the tools we use is [Jenkins](http://http://jenkins-ci.org/ "Jenkins") and whilst we get emails and check the Jenkins Dashboard to see if a build has failed,  developers often have a tendency to not check their emails or check Jenkins to see what the state of the build is&#8230; As a result it may be hours or even a few days before someone realises the build is not passing&#8230;

So it seemed fitting to write some code to get a LED light to blink if the build is failing. To do this you&#8217;ll need the following:

  * Jenkins with the build you want to monitor setup
  * Arduino (I&#8217;m using an Uno)
  * A LED (though for test purposes if you&#8217;re using an Uno pin 13 has a LED built in which should be sufficient)

  1. Wire up your LED to one of the pins or do what I did and use the built in LED on pin 13.
  2. Write some code in your language of choice to grab the build status from Jenkins and send it serially to the Arduino. I chose to grab the status as JSON, but there are [other options available](https://wiki.jenkins-ci.org/display/JENKINS/Remote+access+API). I used Java and the Spring Framework to schedule a process to run every 5 seconds to grab the Jenkins status and send it across to the Arduino with the main grunt work being the code below: [sourcecode language=&#8221;java&#8221;]
  
    package com.delineneo.processor;</p> 
    import com.delineneo.communication.SerialCommunicator;
  
    import org.springframework.beans.factory.annotation.Autowired;
  
    import org.springframework.scheduling.annotation.Scheduled;
  
    import org.springframework.stereotype.Component;
  
    import org.springframework.web.client.RestTemplate;
    
    import java.io.IOException;
    
    import static org.apache.commons.lang.StringUtils.contains;
    
    /**
   
    * Created by IntelliJ IDEA.
   
    * User: deline
   
    * Date: 2/03/12
   
    * Time: 8:33 PM
   
    */
  
    @Component
  
    public class JenkinsStatusProcessor {
      
    private static final String JENKINS_URL = "http://localhost:8080/job/JenkinsStatus/api/json" ;
      
    private static final String SUCCESS\_BUILD\_COLOR = "blue";
      
    public static final char BUILD_FAIL = &#8216;0&#8217;;
      
    public static final char BUILD_SUCCESS = &#8216;1&#8217;;
    
    private RestTemplate restTemplate;
      
    private SerialCommunicator serialCommunicator;
    
    @Scheduled(fixedDelay=5000)
      
    public void process() {
    
    String jsonString = restTemplate.getForObject(JENKINS_URL, String.class);
    
    boolean buildSuccess = isBuildSuccessful(jsonString);
          
    try {
              
    serialCommunicator.send(buildSuccess ? BUILD\_SUCCESS : BUILD\_FAIL);
          
    } catch (IOException e) {
              
    e.printStackTrace();
          
    }
      
    }
    
    private boolean isBuildSuccessful(String jsonString) {
          
    if (contains(jsonString, SUCCESS\_BUILD\_COLOR)) {
              
    return true;
          
    }
          
    return false;
      
    }
    
    @Autowired
      
    public void setRestTemplate(RestTemplate restTemplate) {
          
    this.restTemplate = restTemplate;
      
    }
    
    @Autowired
      
    public void setSerialCommunicator(SerialCommunicator serialCommunicator) {
          
    this.serialCommunicator = serialCommunicator;
      
    }
  
    }
  
    [/sourcecode]
    
    In the **process** method we grab the status as JSON using Spring&#8217;s [RestTemplate](http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/web/client/RestTemplate.html) then search for the build status colours in the string. Blue represents success and I treat any other colour (yellow and red are the other ones) as a failure. We then send either a &#8216;0&#8217; or &#8216;1&#8217; for fail or success respectively.
    
    You might wonder why we send a char instead of a boolean&#8230; Serial write to the Arduino is as an int or byte array, and on the Arduino side read is done either as an int or a char. For example sending &#8216;A&#8217; will be received via the Arduino as either the char &#8216;A&#8217; or the int value 65 (the ascii value). This post on [bildr](http://bildr.org/2011/01/arduino-serial/) gives you a bit more info on why one might choose to read values as and int instead of a char.</li> 
    
      * Write some code for the Arduino to process the received data and set the LED to flashing if the build has failed. The code below listens on the serial port:
  
        [sourcecode language=&#8221;cpp&#8221;]
  
        /* JenkinsStatus will turn the LED at pin 13 on/off depending
   
        * on the value serially read.
   
        */
  
        const int BUILD_SUCCESS = 49;
  
        int inByte;
  
        int currentPinValue = 0;</p> 
        void setup() {
      
        Serial.begin(9600);
      
        pinMode(13, OUTPUT);
  
        }
        
        void loop() {
      
        if (Serial.available() > 0) {
          
        inByte = Serial.read();
          
        if (inByte == BUILD_SUCCESS) {
              
        digitalWrite(13, LOW);
          
        } else{
              
        digitalWrite(13, HIGH);
          
        }
      
        } else {
          
        currentPinValue = digitalRead(13);
          
        if (currentPinValue == HIGH) {
              
        delay(1000);
              
        digitalWrite(13, LOW);
              
        delay(1000);
              
        digitalWrite(13, HIGH);
          
        }
      
        }
  
        }
  
        [/sourcecode]
        
        In the **loop** if there&#8217;s data to be read we read it then determine if what state the LED on pin 13 needs to be in. The pin needs to be LOW (i.e. off) if the build is passing and HIGH (on) otherwise. Additionally, if there is no data to be read we want to keep the LED in a flashing state if it was set to HIGH (last read indicated build had failed).</li> </ol> 
        
        So that&#8217;s pretty much the long short of it, the full code is available on my Git repo &#8211; <https://github.com/deline/JenkinsStatus>
        
        Some thoughts on how JenkinsStatus could be improved:
        
          * Allow config of Jenkins details via properties files
          * Allow more than one Jenkins job to be monitored
          * Put in more LEDs for other states