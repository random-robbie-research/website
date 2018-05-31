---
ID: 6129
post_title: 'Security.txt &#8211; Adding it to existing cpanel clients folders/'
post_name: >
  security-txt-adding-it-to-existing-cpanel-clients-folders
author: Robbie
post_date: 2017-12-11 10:00:44
layout: post
link: >
  https://xsses.rocks/security-txt-adding-it-to-existing-cpanel-clients-folders/
published: true
tags: [ ]
categories:
  - Tips
---
<p style="text-align: left;">After reading a few tweets i've seen a really good idea.

<a href="https://securitytxt.org/">https://securitytxt.org/</a>

<a href="https://securitytxt.org"><img class="aligncenter size-full wp-image-6131" src="https://xsses.rocks/wp-content/uploads/2017/12/Capture-1.png" alt="" width="1905" height="780" /></a>

basically adding a security.txt file to your root WWW directory to allow people to report security issues with your website and give them a link to your public PGP key and also a link to your little hall of fame.

I run a Cpanel server in work and we have around 80 clients so I had to add this to all of their websites.

I added the file's needed to the skeleton page /root/cpanel3-skel/public_html/ but I needed to add it to every client website.

How to add it to all current users websites:

https://gist.github.com/random-robbie/091269be8b6df8aa5719fbe0e7babd94</p>