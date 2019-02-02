---
id: 83
title: Easy REST service development with Spring 3
date: 2010-08-09T19:10:17+00:00
author: deline
excerpt: |
  So I've had the opportunity of late to dabble with Spring 3. From what I had seen before I wasn't totally sold on the move to annotated controllers but after having used it for a few months I think I'm pretty much a convert to the new approach.
  
  One of the major advantages to this new style is that it makes it dead easy to create RESTful web services. You basically define your controller class and annotate your methods the methods you wish to expose as a REST call with the @RequestMapping annotation. With this annotation you can supply some additional attributes such as the URI pattern you wish to match and what HTTP method applies to the service,
  
  Combined with added support for JSON such as MappingJacksonJsonView and the Jackson JSON libraries one can very quickly whip up a fairly robust REST service.
  
  As a good starting resource the SpringSource blog has a good rundown: http://blog.springsource.com/2009/03/08/rest-in-spring-3-mvc/
layout: post
guid: http://delineneo.com/?p=83
permalink: /2010/08/easy-rest-service-development-with-spring-3/
categories:
  - Technology
---
So I&#8217;ve had the opportunity of late to dabble with Spring 3. From what I had seen before I wasn&#8217;t totally sold on the move to annotated controllers but after having used it for a few months I think I&#8217;m pretty much a convert to the new approach.

One of the major advantages to this new style is that it makes it dead easy to create RESTful web services. You basically define your controller class and annotate your methods the methods you wish to expose as a REST call with the @RequestMapping annotation. With this annotation you can supply some additional attributes such as the URI pattern you wish to match and what HTTP method applies to the service,

Combined with added support for JSON such as MappingJacksonJsonView and the Jackson JSON libraries one can very quickly whip up a fairly robust REST service.

As a good starting resource the SpringSource blog has a good rundown: http://blog.springsource.com/2009/03/08/rest-in-spring-3-mvc/