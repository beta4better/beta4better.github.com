---
layout: page
title: Time will tell!
tagline: rebuild from 2016
---
{% include JB/setup %}

This is Charles, here is my latest web page served on [Github](http://www.github.com), thanks for the help from 
[Jekyll Bootstrap](http://jekyllbootstrap.com). For much more personal information, you may find it 
[here](http://charles.beta4better.com).

Here's a list for the recent posts.

<ul class="posts">
  {% for post in site.posts limit:10 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
