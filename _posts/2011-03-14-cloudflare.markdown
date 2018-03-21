---
layout: post
title: CLOUDFLARE
date: '2011-03-14 20:20:00'
---

<p>不知道再godaddy购买的域名是否可以使用cloudflare提供的服务，在godaddy的DNS Manager里修改不了DS。</p>

<p>2011-01-15：</p>

<p>godaddy可以使用的哦，昨天没有仔细去找修改域名服务的位置，现在已经用上了。记得要讲<strong>Basic Security Level</strong>关掉，不然会要求验证的。</p>

<p>而且有一个比较有意思的现象，DS修改成cloudflare的之后，ping域名时你会发现IP地址不是你服务器之前的IP了，变成了另一个。如果用的是vps就不能用域名来登录了，需要直接使用IP地址，或许这也是一种保护措施吧。还没仔细去看cloudflare的文档，暂时不明了。</p>