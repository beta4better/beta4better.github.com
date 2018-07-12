---
layout: default
title: Weblog for Charles
tagline: rebuild from 2016
---

{% for post in site.posts limit:9 %}
<div class="blog-post">
  <h2 class="blog-post-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p class="blog-post-meta">{{ post.date | date_to_long_string }} by {{ site.author.name }}</p>
  {{ post.content }}
</div><!-- /.blog-post -->
{% endfor %}



{% include JB/setup %}
