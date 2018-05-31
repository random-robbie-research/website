---
ID: 6073
post_title: Adding Swap to 512mb VPS
post_name: adding-swap-to-512mb-vps
author: Robbie
post_date: 2017-11-02 11:10:42
layout: post
link: >
  https://xsses.rocks/adding-swap-to-512mb-vps/
published: true
tags:
  - gist
  - swap
  - vps
categories:
  - Tips
---
If you are like me and love to use <a href="https://dply.co">https://dply.co</a> for deploying a quick VPS to test a few things you will sometimes run into issues due to the limited amount of ram.

I found running two docker containers was killing the VPS and needed to run both containers to ensure something worked.

Then I remembered if you add swap it will use that for additional ram.

so here is a nice little gist to add 2GB of swap.

https://gist.github.com/random-robbie/01a85161ac83244aff7f3747bbe79dfc