---
layout: post
title: CtdlLoginExistingUser
date: '2011-06-22 18:43:00'
tags:
- citserver
---

<p>今天服务器上突然出现了下面这个错误：</p>

<pre><code>2011 Jun 22 21:43:05 beta4better CtdlLoginExistingUser((null), jackie)
2011 Jun 22 21:43:06 beta4better CtdlLoginExistingUser((null), jackson)
</code></pre>

<p>不知到是什么问题，一直不停的出，重启了服务器也照旧是这样。将进程挨个停掉，发现是这个进程的问题/usr/sbin/citserver。真的是太奇怪了，莫名其妙的。</p>