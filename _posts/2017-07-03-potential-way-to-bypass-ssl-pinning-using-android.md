---
ID: 5993
post_title: 'Potential way to bypass SSL pinning using #Android'
post_name: >
  potential-way-to-bypass-ssl-pinning-using-android
author: Robbie
post_date: 2017-07-03 09:13:23
layout: post
link: >
  https://xsses.rocks/potential-way-to-bypass-ssl-pinning-using-android/
published: true
tags:
  - burp
  - ssl-pinning
categories:
  - Tips
---
I emailed burp support for some help one an app i wanted to see what it was doing traffic wise....

This was their response.

[embed]https://vimeo.com/137672482[/embed]

&nbsp;

Some native apps use their own certificate trust store, and some implement certificate pinning to only trust specific server-side certificates. In this situation, breaking the SSL tunnel is non-trivial and may entail jailbreaking the device or using some other advanced tools.

One of our users created a short video on the process:

<a href="https://vimeo.com/137672482" target="_blank" rel="noopener" data-saferedirecturl="https://www.google.com/url?hl=en-GB&amp;q=https://vimeo.com/137672482&amp;source=gmail&amp;ust=1499158884128000&amp;usg=AFQjCNEYgCaQ9a1H7TtZ0JVLY93mXQZYuQ">https://vimeo.com/137672482</a>

In the video they go over how to setup Android with ProxyDroid and FS Cert Installer to push HTTPS App traffic to Burp Suite.

They also provided these basic instructions.

Burp Suite Host:
• Reset burp suite
• Turn on listen to all interfaces

Android Host:
• Remove all User Certs
• Stop task and remove data for ProxyDroid and FS Cert installer ( you can just uninstall reinstall )
• Put the phone in airplane mode then turn on WIFI
• In FS Cert put in proxy IP and PORT then click the middle button Add CA and add it under WIFI Cert in the dropdown
• Then click test chain and it should all be green yes for <a href="http://www.google.com/" target="_blank" rel="noopener" data-saferedirecturl="https://www.google.com/url?hl=en-GB&amp;q=http://www.google.com&amp;source=gmail&amp;ust=1499158884128000&amp;usg=AFQjCNHuQBuTlg_gLs5ZqFLxSzFBlinXQQ">www.google.com</a>
• For Proxydroid just put in the IP and port and also tunnel DNS
• Kill or reinstall any apps before you start to make sure they go through the proxy properly