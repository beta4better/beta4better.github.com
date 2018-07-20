---
layout: default
title: Charles' Lab
tagline: rebuild from 2016
---

{% for post in site.posts limit:9 %}
<div class="blog-post">
  <h2 class="blog-post-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p class="blog-post-meta"><i class="far fa-calendar-alt"></i> {{ post.date | date_to_long_string }} by <i class="far fa-user"></i> {{ site.author.name }}</p>
  {{ post.content }}
</div><!-- /.blog-post -->
{% endfor %}



{% include JB/setup %}
