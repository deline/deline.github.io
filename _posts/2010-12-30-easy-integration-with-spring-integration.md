---
id: 1007
title: Easy integration with Spring Integration
date: 2010-12-30T21:22:31+00:00
author: deline
layout: post
guid: http://www.delineneo.com/?p=1007
permalink: /2010/12/easy-integration-with-spring-integration/
categories:
  - Programming
tags:
  - java
  - spring
  - twitter
---
So I&#8217;ve had the opportunity to use [Spring Integration](http://www.springsource.org/spring-integration) recently and I thought I&#8217;d do a blog post about it &#8211; partly for my own review/recap/learning but also for anyone out there looking to play around with it. In a nutshell Spring Integration lets you integrate with other systems without having to deal with all the boilerplate concerns of your typical enterprise integration solutions. It provides a [number of integration adapters straight out of the box](http://static.springsource.org/spring-integration/docs/2.0.0.RELEASE/reference/htmlsingle/#spring-integration-adapters) for common integration methods such as: files, jms, jdbc, ftp and so on (take a look at the Spring doco for the full set).

The general gist of things has you defining a series of channels of which the endpoint may be the entry or exit to the system. One endpoint may be the entry point to another channel. E.g. in the following A<&#8212;&#8212;&#8211;>B is a channel with A as the input and B as the output endpoints. B<&#8212;&#8212;&#8211;>C is another channel where the output B from the A<&#8212;&#8212;&#8211;>B channel is the input and C the output.

A<&#8212;&#8212;&#8211;>B<&#8212;&#8212;&#8211;>C

To really see how it all hangs together I&#8217;ve knocked together a little working example to integrate with Twitter using the built in Twitter Adapter. The app basically polls Twitter with a search on a hashtag, adds a field to the header then passes the message on to a service to be dealt with &#8211; in this case we are just going to print out to System.out. Sounds complicating, but Spring makes it easy &#8211; take a look at src/main/resources/twitter-integration.xml.

[xml]

<channel id="inboundMentionsChannel"/>

<channel id="inputServiceActivatorChannel"/>

[/xml]

This defines the channels, note that we haven&#8217;t actually specified what the endpoints are yet&#8230;

[xml]

<twitter:search-inbound-channel-adapter query="#springintegration" channel="inboundMentionsChannel">

<poller fixed-rate="5000" max-messages-per-poll="3"/>

</twitter:search-inbound-channel-adapter>

<header-enricher input-channel="inboundMentionsChannel" output-channel="inputServiceActivatorChannel">

<header name="headerField1" value="dummy header value"/>

</header-enricher>

[/xml]

This is the interesting stuff where we link all the endpoints and channels together. Lines 1-3 define the inbound adapter (endpoint) which connects the system with Twitter. This is a search-inbound-adapter that polls for a twitter search using the specified query &#8211; in this case the hashtag #springintegration.

Lines 4-7 defines a header enricher. This allows us to pop values into the message header that can be used downstream. For this example we&#8217;re just populating a field called &#8216;headerField1&#8217; with a dummy value. We&#8217;re not actually going to use this field for anything in the example but I wanted to show how easy it was to add info to the message header. The header enricher also has an input channel and output channel specified. As you may have worked out the input to the header enricher is from the endpoint of the &#8216;inboundMentionsChannel&#8217;, which in this case will contain the results from the Twitter search. And the outbound channel is to a service activator which references the TwitterService bean (bean is autowired).

If you take a look at TwitterService.java you&#8217;ll see that it prints out to System.out and adds the tweet to a list. Running the test case TwitterIntegrationTest.java you can check that the output matches the expected tweet search result count of 3.

[twitter-integration.zip](http://www.delineneo.com/wp-content/uploads/2010/12/twitter-integration.zip)
