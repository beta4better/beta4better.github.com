---
layout: post
title: "Hosting Your Static Site at AWS S3"
date: 2012-02-20 22:22
categories: [aws, s3, jekyll, octopress]
tags: [aws, s3, jekyll, octopress]
---

## INTRUCTION ##

AWS - [amazon web services](http://aws.amazon.com/) launch the [AWS Free Uasge Tier](http://aws.amazon.com/free/), which be able to run a free Amazon EC2 Micro Instance for one year and also leverage a free usage tier for Amazon S3, Amazon elastic Block Store, Amazon Elastic Load Balancing, and AWS data transfer (except SimpleDB, SQS, and SNS which are free indefinitely).

## AWS Free Usage Tier SPEC ##

-   750 hours of Amazon EC2 Linux Micro Instance usage (613 MB of memory and 32-bit and 64-bit platform support) ¡V enough hours to run continuously each month
-   750 hours of Amazon EC2 Microsoft Windows Server Micro Instance usage (613 MB of memory and 32-bit and 64-bit platform support) ¡V enough hours to run continuously each month
-   750 hours of an Elastic Load Balancer plus 15 GB data processing
-   30 GB of Amazon Elastic Block Storage, plus 2 million I/Os and 1 GB of snapshot storage
-   5 GB of Amazon S3 standard storage, 20,000 Get Requests, and 2,000 Put Requests
-   100 MB of storage, 5 units of write capacity, and 10 units of read capacity for Amazon DynamoDB.
-   25 Amazon SimpleDB Machine Hours and 1 GB of Storage
-   100,000 Requests of Amazon Simple Queue Service
-   100,000 Requests, 100,000 HTTP notifications and 1,000 email notifications for Amazon Simple Notification Service
-   10 Amazon Cloudwatch metrics, 10 alarms, and 1,000,000 API requests
-   15 GB of bandwidth out aggregated across all AWS services

Maybe you know [All Things Distributed](http://www.allthingsdistributed.com/), a blog update by [Werner Vogels](http://www.twitter.com/werner), the CTO of [amazon.com](http://amazon.com/). He wrote a post: [No Server Required - Jekyll & Amazon S3](www.allthingsdistributed.com/2011/08/Jekyll-amazon-s3.html). If your site is static generate by [Jekyll](http://jekyllrb.com/) or the other [static site generator](/), you can host your site at AWS S3.

If you're interested at static site generator, please read my post: [Static Site Generator Intruction](/). And also this post: [Blogging like a Hacker](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html). I remember there is a dissucsion about blogging like a hacker at [Hacker News](http://news.ycombinator.com/), but cann't fund now. Some day I find, I will update it here.

Using AWS S3 to host your static site is simple:

## Register your AWS account ##


## Create a bucket for your site


## Enable the bucket for web access


## Generate your site using Jekyll and upload to your bucket


## Set the domain name for your site


*Enjoy yourself!*

