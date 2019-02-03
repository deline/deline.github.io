---
id: 1166
title: Adventures with Swift and unit testing
date: 2014-08-17T21:21:17+00:00
author: deline
layout: post
guid: http://www.delineneo.com/?p=1166
permalink: /2014/08/adventures-with-swift-and-unit-testing/
categories:
  - Programming
tags:
  - ios
  - swift
---
Firstly, it&#8217;s been a long time with no blog. Life, the universe kind of caught up with me. That and I think blogging for a number of years in my late teens/early twenties kind of got the better of me&#8230; But from now on, let&#8217;s see how this blogging stuff goes. Hopefully it&#8217;ll be a place for me to brain dump my thoughts and learnings&#8230; Which brings me onto the topic of this post &#8216;Adventures with Swift and unit testing&#8217;.

Bit of background, about 5 years ago in my previous job I was part of an ios development team. Things were different back then. Where I worked didn&#8217;t practice TDD and the testing landscape was fairly immature with respect to mobile development.

Fast forward to the present and I work at place that does TDD and tooling/frameworks for testing ios development has vastly improved. It&#8217;s still somewhat behind what I&#8217;m used to as a Java developer, but we need to bear in mind the mobile ecosystem/environment is still relatively new in the timeframe of things (the first iPhone was only released in 2007).

At WWDC 2014 [Swift was introduced](https://developer.apple.com/swift/ "Introducing Swift"). I&#8217;ve read a bit here and there, but I&#8217;m finally getting round to giving it a try &#8211; TDD style. With Xcode 6 beta 4 access controls has been introduced which has provided a bit of an interesting situation with unit testing.

Access controls come in 3 flavours:

  * **Public** &#8211; as it states, accessible from it&#8217;s own module as well as any other code that imports the said module. Pretty much more or less the same as public in Java.
  * **Internal** &#8211; Only accessible within the defined module. Somewhat similar to package private in Java.
  * **Private** &#8211; Only accessible via the defining source code. Pretty much the same as private in Java.

What&#8217;s interesting is that by following good practices of encapsulation using the above access levels brings about some interesting implications for unit testing. This comes about because in ios developer a test target is not part of the applications module and thus cannot see anything that is not marked public. This is particularly frustrating as in Java something marked package private can still be accessed/seen in the test tree when in the same package.

The beta release notes actually state:

<pre>A limitation of the access control system is that unit tests cannot interact with the classes and
methods in an application unless they are marked public. This is because the unit test target is
not part of the application module.</pre>

Can this be worked around? Somewhat so&#8230; At the moment you could mark everything as public, but that seems rather unfortunate as it pretty much bypasses any encapsulation. Add the class under test to your unit test target.

Interestingly enough, on the [developer forums](https://devforums.apple.com/message/1010766#1010766) Chris Lattner has posted that they know the access control design doesn&#8217;t really work for unit testing&#8230;
