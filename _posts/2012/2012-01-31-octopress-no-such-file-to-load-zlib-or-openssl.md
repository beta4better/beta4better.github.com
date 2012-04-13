---
layout: post
title: "Octopress: no such file to load: zlib, openssl"
categories: [thinkpad, octopress, zlib, openssl]
tags: [thinkpad, octopress, zlib, openssl]
---

Thinkpad X201i 3249-MUC, this is the model of my laptop,
also the right computer building this site. It has been a long time for 
using this laptop for me making a great effort for me.

But the memory for X201i is just 2GB, I plan to upgrade it to 8GB.
But 2 from [taobao](http://www.taobao.com/), will be arrived the day after 
tomorrow maybe.

First time upgrade the memory of laptop, a little exciting.

Last night I reinstall the system from [LinuxMint](http://localhost:4000/2012/01/20120124.html) to Debian Squeeze using 
encryped lvm, feeling greatly now.

## cotopress install problem

While I install octopress on my laptop, there comes will two problems:

- **no such file to load -- zlib**

install zlib1g and zlib1g-dev, and then come to the source directory of ruby `/ext/zlib`, run the following command:

    ruby extconf.rb && make && make install 

- **no such file to load -- openssl**

install libssl-dev, and then come to the source directory of ruby 
`/ext/openssl`, run the following command:

    ruby extconf.rb && make && make install
