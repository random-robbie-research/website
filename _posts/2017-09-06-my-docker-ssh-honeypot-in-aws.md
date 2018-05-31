---
ID: 6036
post_title: 'My Docker SSH Honeypot in AWS&#8230;'
post_name: my-docker-ssh-honeypot-in-aws
author: Robbie
post_date: 2017-09-06 09:32:19
layout: post
link: >
  https://xsses.rocks/my-docker-ssh-honeypot-in-aws/
published: true
tags:
  - botnet
  - honeypot
  - ssh
categories:
  - Tips
---
<img class="aligncenter size-full wp-image-6037" src="https://xsses.rocks/wp-content/uploads/2017/09/botnet2_538023.jpg" alt="Botnet" width="350" height="310" />
So the other day I decided to try make a honeypot using docker and found a great little project <a href="https://github.com/droberson/ssh-honeypot">https://github.com/droberson/ssh-honeypot</a>

The final version of the SSH honeypot was this..
<a href="https://hub.docker.com/r/txt3rob/docker-ssh-honey/">https://hub.docker.com/r/txt3rob/docker-ssh-honey/</a>

So I fired it up in shipyard (nice web gui for docker) and put this in AWS on the free tier to test.

The results after 20 hours so far are!

<img class="aligncenter size-full wp-image-6038" src="https://xsses.rocks/wp-content/uploads/2017/09/capture.png" alt="" width="1792" height="51" />

[table id=1 /]

[table id=2 /]

I am happy to supply any one the logs of these containers if you wish to use them for your own research just message me on twitter @random_robbie.