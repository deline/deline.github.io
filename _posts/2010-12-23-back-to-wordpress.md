---
id: 981
title: Back to WordPress
date: 2010-12-23T05:23:26+00:00
author: deline
layout: post
guid: http://delineneo.com/?p=981
permalink: /2010/12/back-to-wordpress/
categories:
  - Technology
---
So after a bit of procrastination I finally bit the bullet and attempted the migration of my website back to using WordPress as the CMS. For those tech dudes out there, or those who follow my happenings, you might remember I started out on Blogger, migrated to WordPress than on to Drupal. My main reason for moving back to WordPress is that whilst Drupal was awesome as a CMS I predominantly use my website to blog, and for that WordPress  excels. If I had to run a fully fledged website, I&#8217;d definitely fall back to Drupal though as there are things that it excels at there.

I&#8217;d put off the migration for ages as there is no quick and easy way to migrate from Drupal to WordPress. You have no choice but to run SQL commands. On top of that I still had my original WordPress blog that I wanted to &#8216;keep&#8217;. I&#8217;d never bothered to migrate these into my Drupal site, but now I was going back to WordPress I wanted them all in the same site.

So for anyone on the web thinking of making the move back (or to)&#8230; here are the steps that I followed&#8230; Do make sure you take a backup of your database before hand though, as whilst these steps seemed to work successfully for me, they may not necessarily work for everyone. Hence take these steps as a guide only&#8230;

  1. Take a look at <a title="Permanent Link to Convert – Import A Drupal 6 Based Website To WordPress v2.7" rel="bookmark" href="http://socialcmsbuzz.com/convert-import-a-drupal-6-based-website-to-wordpress-v27-20052009/">Convert – Import A Drupal 6 Based Website To WordPress v2.7</a> and follow the instructions there. Some differences for my setup is that I installed WordPress (Version 3.0.3) instead and didn&#8217;t bother to delete the Drupal tables as I was going to get my data back into Prod a different way.
  2. Check your development WordPress install and ensure it looks right
  3. OPTIONAL STEP: If you have a previous WordPress site that you want to keep content from as well, use the Export function in the previous install to download a WordPress export file. Import this into your new WordPress site using the Import function.
  4. On your development WordPress use the Export function to download a WordPress export file. This export files will contain all the data you want to use in your new site. E.g. in my case this was all my Drupal content plus the content from my original WordPress site.
  5. Install WordPress to your Production server
  6. Use the Import functionality to import the export file you downloaded in Step 4.
  7. Check that your Production WordPress looks correct.
