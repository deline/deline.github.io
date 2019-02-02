---
id: 1043
title: Installing Groovy on a Mac
date: 2011-01-13T21:37:42+00:00
author: deline
layout: post
guid: http://www.delineneo.com/?p=1043
permalink: /2011/01/installing-groovy-on-a-mac/
categories:
  - Programming
tags:
  - groovy
  - java
---
Having heard about Groovy and Grails for the last few years but not having actually had a look at it I installed Groovy on my Mac the other week for a bit of a play. It&#8217;s always good and fun to have a look at a different language even if if you&#8217;re not going to use it in your day to day job. Coming from predominantly a Java background Groovy seemed like a good choice as it runs on the Java platform and the language is similar. Having had the opportunity to use Objective-C for a few months last year and seeing how in some ways it was more powerful than Java (but also in other ways frustrating), I was curious to see what power Groovy gave to a developer.

The first step though was to get Groovy installed on my Mac. So I thought I&#8217;d put a post up mainly for anyone new to developing on a Mac. Whilst I&#8217;ve had my Mac for a year or so, I hadn&#8217;t really had it setup for anything other than Java until recently, and there were definitely some things that were a little different to what I was used to on Windows as well from my prior limited stint in Ubuntu land.

These instructions are based on a setup for OS X. I&#8217;d imagine the setup may be similar on any other version?

  1. Java should already be installed on your machine. Confirm this by opening up a Terminal and typing in &#8216;**java -version**&#8216;.
  2. Download the binary Zip release of Groovy [from the Groovy site](http://groovy.codehaus.org/).
  3. Extract the contents into **/usr/local** &#8211; e.g. my install location is **/usr/local/groovy-1.7.6/**. You will probably need to need to use the **sudo** command for the extract as you will need to be superuser to write to the location.
  4. Check if a file called **environment.plist** exists in the following location **/Users/YOUR\_USER\_NAME/.MacOSX**. If it doesn&#8217;t create it.
  5. Open environment.plist in the Property List Editor
  6. Add an entry for **JAVA_HOME** if not present, ensure the value is the location of your Java installation. This should be **/System/Library/Frameworks/JavaVM.framework/Versions/CurrentJDK/Home**
  7. Add an entry for **GROOVY_HOME** if not present and ensure the value is the location Groovy is installed. E.g. **/usr/local/groovy-1.7.6**
  8. Add an entry for **PATH** if not present, and ensure the Groovy bin and Java bin directories are present by adding  **$JAVA\_HOME:$GROOVY\_HOME/bin**
  9. Log out and re log back in for the changes to take effect.
 10. Check that everything is all setup correctly by opening a Terminal and running **groovy -version** which should show you which version of Groovy is installed.