---
ID: 6055
post_title: Using Docker to Broadcast 5000 SSIDS
post_name: using-docker-to-broadcast-5000-ssids
author: Robbie
post_date: 2017-09-20 08:26:59
layout: post
link: >
  https://xsses.rocks/using-docker-to-broadcast-5000-ssids/
published: true
tags:
  - docker
  - spoof
  - ssid
categories:
  - Tips
---
So while reading a blog i love from <a href="https://www.twitter.com/jgamblin">@jgamblin </a>, I came across this lovely bit of his blog.
<a href="https://jerrygamblin.com/2016/11/27/spoofing-the-top-5000-ssids/">Spoofing the top 5000 ssids</a>


So i thought to myself could i make a docker version of this to make it quick and simple to do with out needing to install kali etc.

It turns out i could and very easily.

<a href="https://github.com/random-robbie/spoofssid-docker/">https://github.com/random-robbie/spoofssid-docker/</a>


Running this will give you <img src="https://s26.postimg.org/4ju3ybieh/capture.png">

Winning!

To run it simply type 

<code>sudo docker run --privileged --net=host -it txt3rob/spoofssid-docker /bin/bash start.sh</code> and it's done!


Check out the readme as i have made a version for a raspberry pi!