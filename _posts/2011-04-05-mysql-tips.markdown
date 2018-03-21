---
layout: post
title: MYSQL TIPS
date: '2011-04-05 06:17:00'
---

<p>MySQL创建数据库的方法：</p>

<blockquote>
<p>create database database-name default character set utf8 default collate utf8_general_ci;</p>
</blockquote>

<p>MySQL修改用户密码的方法：</p>

<blockquote>
<p>use mysql</p>
<p>update user set password=password(&#8216;password here&#8217;) where user=&#8217;root&#8217;;</p>
<p>flush privileges; </p>
</blockquote>