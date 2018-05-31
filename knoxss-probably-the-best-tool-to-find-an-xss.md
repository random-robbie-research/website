---
id: 33
title: 'Knoxss &#8230;. probably the best tool to find an XSS'
date: 2017-05-11T13:11:45+00:00
author: Robbie
layout: page
guid: http://xsses.rocks/?page_id=33
---
KNOXSS is an online XSS discovery service with demonstration of vulnerability (PoC &#8211; Proof of Concept). It&#8217;s still under development, being launched as beta. Currently it supports source and DOM based reflected XSS, although by chance a stored or a more complex DOM-based case may arise if there&#8217;s also a reflection in response. Except for demo plan (below), it also drops (in certain cases) a XSS payload designed to send an email report to KNOXSS user with info about the environment where it was triggered (in scenarios where such vulnerability exists) hence also being able to find blind and stored XSS cases in this way.

&nbsp;

It has 3 plans: Demo, Standard and Pro.

&nbsp;

**KNOXSS Demo**

<img class="aligncenter wp-image-404 size-large" src="https://i0.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-demo-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1" sizes="(max-width: 730px) 100vw, 730px" srcset="https://i0.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-demo-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1 1024w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-demo-1.1.1-300x169.png 300w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-demo-1.1.1-768x432.png 768w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-demo-1.1.1.png 1366w" alt="" width="730" height="411" data-recalc-dims="1" />

&nbsp;

&nbsp;

A completely free version to show the way KNOXSS works, with reflection finding and PoC generation using the most common and useful single XSS vector/payload. A lot of XSS flaws can be found with this simplest version, either using GET or POST HTTP methods.

&nbsp;

**KNOXSS Standard**

&nbsp;

<img class="aligncenter wp-image-405 size-large" src="https://i1.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-std-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1" sizes="(max-width: 730px) 100vw, 730px" srcset="https://i1.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-std-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1 1024w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-std-1.1.1-300x169.png 300w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-std-1.1.1-768x432.png 768w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-std-1.1.1.png 1366w" alt="" width="730" height="411" data-recalc-dims="1" />

&nbsp;

The core engine of KNOXSS with possibility to send authenticated GET or POST requests by means of HTTP headers provided by user. For PoC it uses a specially crafted XSS polyglot, designed to work in majority of XSS scenarios with basic filter bypass capabilities. It comes with a Mozilla Firefox extension that can scan for forms and send to main interface the target page where user currently is, for XSS tests. It performs very well against almost all targets.

&nbsp;

**KNOXSS Pro**

&nbsp;

<img class="aligncenter wp-image-406 size-large" src="https://i1.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-pro-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1" sizes="(max-width: 730px) 100vw, 730px" srcset="https://i1.wp.com/knoxss.me/wp-content/uploads/2016/10/knoxss-pro-1.1.1-1024x576.png?resize=730%2C411&#038;ssl=1 1024w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-pro-1.1.1-300x169.png 300w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-pro-1.1.1-768x432.png 768w, https://knoxss.me/wp-content/uploads/2016/10/knoxss-pro-1.1.1.png 1366w" alt="" width="730" height="411" data-recalc-dims="1" />

&nbsp;

With multiple vectors and decision-making capabilities, KNOXSS Pro is able to find a lot of edge XSS cases and bypass more filters. It also has an extension that makes all the job completely automatic: after setting a domain with one click, all URLs and forms navigated in all subdomains will be submitted to KNOXSS for testing.

&nbsp;

Standard and Pro comes with a Mozilla Firefox addon designed to send target info to KNOXSS service while user navigates. It also grabs all form fields of the current page for additional tests.

Because KNOXSS actually checks for vulnerabilities using Gecko engine and pops a window with PoC, we **strongly** recommend the use of <a href="https://www.mozilla.org/en-US/firefox/products/" target="_blank" rel="noopener noreferrer">Mozilla Firefox</a> browser for the intended experience.

&nbsp;

An old video with both Standard and Pro Firefox extensions in action is below.

&nbsp;

<div class="parallax-one-video-container">
</div>