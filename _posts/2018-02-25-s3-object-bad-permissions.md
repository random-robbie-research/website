---
ID: 6157
post_title: S3 Object Bad Permissions
post_name: s3-object-bad-permissions
author: Robbie
post_date: 2018-02-25 07:58:16
layout: post
link: >
  https://xsses.rocks/s3-object-bad-permissions/
published: true
tags:
  - put object acl
  - s3
  - s3 bucket
categories:
  - bugbounty
  - Tips
---
<img class="aligncenter size-full wp-image-6158" src="https://xsses.rocks/wp-content/uploads/2018/02/Screen-Shot-2018-02-25-at-07.53.03.png" alt="" width="1748" height="860" />

I keep seeing something like this during some of my scans and i've come to find that you can hijack that file and do what you want with it despite the bucket not having the upload permissions.

I created a quck script to show you how you can do a POC for a bounty program with out altering the files it's self.

simply save it and then run object_poc.sh bucketname filetoaddpermissionsto yourawsemail@address.com

https://gist.github.com/random-robbie/9c49f5d6c92884feb7b366802566b41d

This will dump the json out showing you having full write permissions to that object.