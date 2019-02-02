---
id: 1051
title: Simple RegEx and Closure example in Groovy
date: 2011-01-15T22:58:54+00:00
author: deline
layout: post
guid: http://www.delineneo.com/?p=1051
permalink: /2011/01/simple-regex-and-closure-example-in-groovy/
categories:
  - Programming
tags:
  - groovy
  - java
---
I&#8217;ve been intermittently reading [Groovy in Action](http://www.amazon.com/Groovy-Action-Dierk-Koenig/dp/1932394842) for the last few nights and whilst it all seems pretty straight forward, for me the real grasping of an understanding comes by writing some code to affirm what was read. That posed the dilemma of what to write, as since leaving uni most of my learning experiences in Java (and development concepts in general) have been in relation to real world business style scenarios. I gave a thought back to my high school days where I learnt how to program. Why not just start with a somewhat simple/trivial problem &#8211; e.g. a factorial calculator, or sentence word reverser and go from there? Sure it&#8217;s not anything too swish, but it seems a good way to get an understanding of the language.

So here I present a simple solution in Groovy that uses RegEx and Closures to captalise the first letter of each word in a string. I&#8217;ll also show you an even neater solution after&#8230;.

First up:

[groovy]

String testString = &#8216;the quick brown fox jumped over the lazy dog&#8217;
  
String regex = /bw*s?b/

testString.eachMatch(regex) { match ->
      
print match.capitalize()
  
}

[/groovy]

Lines 1 and 2 should be pretty self explanatory. We&#8217;ve based our regex of the basis that a word consists of word characters only, may have a space after the last word character and has a word boundary on either side.

Lines 4-6 is where the cool stuff happens, as for each word match we make we want to upper case the first letter and print it out. The method **eachMatch** takes two arguments a String regex and a closure. From the [Groovy docs](http://groovy.codehaus.org/Closures) &#8211; _&#8216;A Groovy Closure is like a &#8220;code block&#8221; or a method pointer. It is a piece of code that is defined and then executed at a later point.&#8217;_ In the example above we have defined the closure inline with one parameter **match** &#8211; parameters are listed before the **->**. The closure calls **capitalize** on the match and prints it out.

We could have easily defined the closure separatley and provided it to **eachMethod** as such:

[groovy]
  
Closure capitalize = { match -> print match.capitalize() }
  
testString.eachMatch(regex, capitalize)
  
[/groovy]

Seems pretty easy right? Not many lines of code and quite succinct about what is happening. Well as is often the case, I did a little Google and here&#8217;s an even easier solution:

[groovy]
  
String testString = &#8216;the quick brown fox jumped over the lazy dog&#8217;
  
print testString.split(&#8216; &#8216;).collect{ it.capitalize() }.join(&#8216; &#8216;)
  
[/groovy]

In the end my solution was a first attempt into using Groovy to solve a problem without having much exposure to the language whilst at the same time trying not to use my Java mindset. After seeing the alternative solution on the Internet it kind of shows that if you know what to use Groovy can make things even simpler as it&#8217;s definitely cleaner without using the RegEx.