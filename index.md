---
layout: default
title: Yuan
tagline: rebuild from 2016
---
{% include JB/setup %}

<p>This is Charles, here is my latest web page served on <a href="http://www.github.com">Github</a>, 
thanks for the help from <a href="http://jekyllbootstrap.com">Jekyll Bootstrap</a>. For much more personal information, 
you may find it <a href="http://charles.beta4better.com">here</a>.</p>

{% for post in site.posts limit:9 %}
  <div class="blog-post">
    <h2 class="blog-post-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p class="blog-post-meta">{{ post.date | date_to_long_string }} by {{ site.author.name }}</p>
    {{ post.content }}
  </div><!-- /.blog-post -->
{% endfor %}