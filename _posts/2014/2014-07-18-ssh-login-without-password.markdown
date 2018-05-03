---
layout: post
title: SSH login without password
date: '2014-07-18 04:11:33'
tags:
- ssh
---

坦白讲我不并了解这其中的原理，但是这样做的好处还是很不错的，至少方便，在频繁登录的时候不用输密码：

先运行 `ssh-keygen`，然后再执行 `ssh-copy-id user@host`，就可以了。以后登录就不需要再输密码了。

原理似乎这里有解，有时间再去看：

[http://en.wikipedia.org/wiki/Public_key_infrastructure]()


另外一个不错的网站可以多去看看： [http://linuxconfig.org/]()