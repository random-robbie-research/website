---
ID: 6104
post_title: 'Finding S3 Buckets by accident&#8230;.'
post_name: finding-s3-buckets-by-accident
author: Robbie
post_date: 2017-12-03 22:19:28
layout: post
link: >
  https://xsses.rocks/finding-s3-buckets-by-accident/
published: true
tags:
  - aws
  - bugbounty
  - burp
  - cloudstorage
  - s3
categories:
  - bugbounty
  - Tips
---
<p style="text-align: center;"><strong>Finding Random S3 Buckets... with bad permissions the lazy way...</strong></p>
&nbsp;

&nbsp;

<img class="aligncenter size-full wp-image-6105" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.23.36.png" alt="s3buckets" width="420" height="34" />
Ok so for those who have a nice full burp pro license here is an easy way to find s3 buckets with out browsing any websites.

Cloud Storage Tester

[caption id="attachment_6106" align="aligncenter" width="570"]<img class=" wp-image-6106" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.29.47.png" alt="" width="570" height="155" /> Cloud Storage Tester[/caption]

Install it and then get the settings sorted!

<img class="aligncenter size-full wp-image-6107" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.32.44.png" alt="" width="2474" height="1174" />
ok so once you have put your keys in from https://www.amazonaws.com you are nearly ready to go.

Time to install adblock plus... i can see you are thinking why the feck am i installing this adblocker!?!?!

<img class="aligncenter size-full wp-image-6108" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.35.12.png" alt="" width="2558" height="1010" />

well the answer is simple! because it has a massive list of domains inside it's updates!

<img class="aligncenter size-full wp-image-6109" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.37.36.png" alt="" width="2874" height="694" />
so after leaving burp alone with firefox and adblock i get this....

<img class="aligncenter size-full wp-image-6110" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.41.28.png" alt="" width="1068" height="396" />
Now the ones you really really want are the ones that have the following....

<img class="aligncenter size-full wp-image-6111" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.42.48.png" alt="" width="380" height="90" />

the plugin uploads a blank file called text.txt to the bucket as part of it's testing so this helps you confirm it's vulnerable to public uploads.

Now to upload a file yourself as part of a POC for a bounty it's simple.

Fire up a shell and type in

<img class="aligncenter size-full wp-image-6112" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.45.20.png" alt="" width="700" height="40" />
once installed type in aws configure and put in your details.

create a file called poc.txt and then put in your details.

[caption id="attachment_6115" align="aligncenter" width="1088"]<img class="size-full wp-image-6115" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.52.48-1.png" alt="" width="1088" height="94" /> poc[/caption]
<blockquote>aws s3 poc.txt s3://bucketname --acl public-read</blockquote>
<img class="aligncenter size-full wp-image-6116" src="https://xsses.rocks/wp-content/uploads/2017/12/Screen-Shot-2017-12-03-at-21.55.07.png" alt="" width="928" height="226" />and there we go!

this is a random bucket they do not have a bounty program!!

Catch me on twitter if you have any questions @random_robbie.

Remember for some bug bounty scans already done <a href="https://bugbounty.xsses.rocks">https://bugbounty.xsses.rocks</a>