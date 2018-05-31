---
ID: 6179
post_title: >
  Just how easy it is to do a domain or
  subdomain take over!?
post_name: >
  just-how-easy-it-is-to-do-a-domain-or-subdomain-take-over
author: Robbie
post_date: 2018-04-13 11:15:25
layout: post
link: >
  https://xsses.rocks/just-how-easy-it-is-to-do-a-domain-or-subdomain-take-over/
published: true
tags:
  - subdomain
  - takeover
categories:
  - bugbounty
  - Tips
---
<p style="text-align: center;">Just how easy is it to take over a domain or a subdomain?</p>
&nbsp;

I will tell you now it is really easy to do!

First part is recon if you want to do check a specific domain then you will need to check all their subdomains and use something like https://github.com/anshumanbh/tko-subs to check if anything can be hijacked.

If you want random websites here is a quick way to find them!

S3 buckets... <a href="https://publicwww.com/websites/NoSuchBucket/" target="_blank" rel="noopener">https://publicwww.com/websites/NoSuchBucket</a> all you have to do is check where the A name record is pointing and create a S3 bucket in the name of the domain.

Example: z4.net points to 54.231.168.35 and when you do a PTR record for this you will see it's s3-website-us-west-2.amazonaws.com so this means we just need to create a bucket in us-west-2 zone and it's all done.

https://gist.github.com/random-robbie/9207d0f293adb704b9a11486c7529a6e

Github pages

Another nice and easy one...

find a domain on the link below that does not have .github.io in the domain name.

<a href="https://publicwww.com/websites/&quot;There+isn%27t+a+Github+Pages+site+here&quot;/">https://publicwww.com/websites/"There+isn%27t+a+Github+Pages+site+here"/</a>

Then just create a repo on your github and go to the settings and then add a file called CNAME and then put in each domain on a new line.

Example: <a href="http://sgr-ksmt.org/">http://sgr-ksmt.org/</a>

for more information check out ed's github

<a href="https://github.com/EdOverflow/can-i-take-over-xyz">https://github.com/EdOverflow/can-i-take-over-xyz</a>

Big Thanks to <a href="https://twitter.com/olihough86">https://twitter.com/olihough86</a> for pointing this out.