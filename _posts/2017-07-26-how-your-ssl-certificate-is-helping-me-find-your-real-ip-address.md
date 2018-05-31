---
ID: 6004
post_title: 'How Your SSL Certificate Is Helping Me Find Your Real IP address&#8230;.'
post_name: >
  how-your-ssl-certificate-is-helping-me-find-your-real-ip-address
author: Robbie
post_date: 2017-07-26 15:22:54
layout: post
link: >
  https://xsses.rocks/how-your-ssl-certificate-is-helping-me-find-your-real-ip-address/
published: true
tags: [ ]
categories:
  - Tips
---
We all know that most people love to hide their servers behind WAFs and CDN's like Cloudflare etc.

Clear Example of this is www.cloudstress.com

which looks like the below which when you click it you can see the shodan plugin is saying yep this is on cloudflare so you will never know it's real ip.

[caption id="" align="alignnone" width="1280"]<a href="https://s2.postimg.org/4fuk9rel5/image.jpg"><img class="size-full" src="https://s2.postimg.org/4fuk9rel5/image.jpg" width="1280" height="401" /></a> Cloudflare[/caption]

Now we all know if the webmaster is a muppet the MX records will reveal the server it's hosted on this is how most cloudflare IP revealers work which may or may not work.

This does not help us in any way as it's not 100% as you can see in this DNS lookup there are no records to show the mail server or the servers real ip address.<img class="aligncenter size-full wp-image-6005" src="http://xsses.rocks/wp-content/uploads/2017/07/Capture.png" alt="" width="1271" height="571" />

Now comes the fun part the server owner probably is trying to follow best practises so they've made a SSL cert to ensure the data between Cloudflare -&gt; Server is secure so it's not intercepted by law enforcement.

So normally we would go to shodan and go see if there are any results.<img class="aligncenter size-full wp-image-6006" src="http://xsses.rocks/wp-content/uploads/2017/07/Capture-1.png" alt="" width="616" height="238" />

&nbsp;

&nbsp;

Ah crap no results what do we do now? well another good site bit like shodan is censys.io.

<img class="aligncenter size-full wp-image-6007" src="http://xsses.rocks/wp-content/uploads/2017/07/Capture-2.png" alt="" width="1587" height="529" /><img class="aligncenter size-full wp-image-6008" src="http://xsses.rocks/wp-content/uploads/2017/07/Capture-3.png" alt="" width="812" height="768" />And there we have it your SSL Certificate has lead to leaking your real IP and the page title confirms the site is the one we want.

<a href="https://s4.postimg.org/j3s6sn0zx/real.jpg"><img class="alignnone size-full" src="https://s4.postimg.org/j3s6sn0zx/real.jpg" width="1280" height="541" /></a>

Again shodan plugin will show you the server IP to confirm you hit the right place.

I've no idea who is behind this site or anything it was one i've chosen at random.