---
id: 80
title: Using Maven and the YUI Compressor plugin to help optimise your site/application performance
date: 2010-05-18T22:43:13+00:00
author: deline
excerpt: |
  So in the last year or so I've picked up bits and pieces on how to use automated software build tools. I've mainly been using Maven and for the things I've had to do so far I'm pretty happy (apart from when the m2eclipse plugin chucks a spaz!).

  One cool way in which you can use Maven and the <a href="http://alchim.sourceforge.net/yuicompressor-maven-plugin/index.html" target="_blank">YUI Compressor plugin</a> is to minify and aggregate (if required) your javascript and CSS files at build time.

  This will help improve your site/application by minimising round trip times and the number of resource requests that need to be queued due to browser limitations on the number of active concurrent connections.

  You utilise the plugin by including the plugin into your pom.xml then defining the configuration that you want applied (e.g. files to include/exclude, aggregation rule etc). The YUI Compresspr plugin site has a couple of examples so refer to it for more info.

  One thing I came across though was that if you are using overlays and have resources in the overlay that need to be included in the compression/aggregation you will need to ensure the war is exploded at the start (e.g. process-resources). This is required so that the files are available for running the YUI Compressor plugin on prior to the building of the final war. If you don't do this step first the overlay is only unpacked during the package phase which is too late as YUI Compressor has already run.

  Anyways that's the tech blog for tonight. Time for sleep...
layout: post
guid: http://delineneo.com/?p=80
permalink: /2010/05/using-maven-and-the-yui-compressor-plugin-to-help-optimise-your-siteapplication-performance/
categories:
  - Technology
---
So in the last year or so I&#8217;ve picked up bits and pieces on how to use automated software build tools. I&#8217;ve mainly been using Maven and for the things I&#8217;ve had to do so far I&#8217;m pretty happy (apart from when the m2eclipse plugin chucks a spaz!).

One cool way in which you can use Maven and the <a href="http://alchim.sourceforge.net/yuicompressor-maven-plugin/index.html" target="_blank">YUI Compressor plugin</a> is to minify and aggregate (if required) your javascript and CSS files at build time.

This will help improve your site/application by minimising round trip times and the number of resource requests that need to be queued due to browser limitations on the number of active concurrent connections.

You utilise the plugin by including the plugin into your pom.xml then defining the configuration that you want applied (e.g. files to include/exclude, aggregation rule etc). The YUI Compresspr plugin site has a couple of examples so refer to it for more info.

One thing I came across though was that if you are using overlays and have resources in the overlay that need to be included in the compression/aggregation you will need to ensure the war is exploded at the start (e.g. process-resources). This is required so that the files are available for running the YUI Compressor plugin on prior to the building of the final war. If you don&#8217;t do this step first the overlay is only unpacked during the package phase which is too late as YUI Compressor has already run.

Anyways that&#8217;s the tech blog for tonight. Time for sleep&#8230;
