---
ID: 6161
post_title: >
  How to tell if you have bad permissions
  on your S3 bucket
post_name: >
  how-to-tell-if-you-have-bad-permissions-on-your-s3-bucket
author: Robbie
post_date: 2018-02-26 08:58:07
layout: post
link: >
  https://xsses.rocks/how-to-tell-if-you-have-bad-permissions-on-your-s3-bucket/
published: true
tags:
  - bad permissions
  - s3
  - s3 bucket
categories:
  - Tips
---
I was recently asked how can I check a s3 bucket with out writing to it to see if it has bad permissions and the answer is a nice simple one.

You do need the AWS CLI installed which can be installed via pip.

In the command line type the following replacing the airpushmarketing with your bucket name.

https://gist.github.com/random-robbie/8acc2c39a275ddb11434787b3a3cd692

If you see the below it's time to shit the bed and fix that S3 bucket!

https://gist.github.com/random-robbie/98bda1341afae3aede8a81feb77c729c

Example response of a bucket with bad permissions


https://gist.github.com/random-robbie/5797c3f5593a06496c16ae2ea34b24d1

&nbsp;