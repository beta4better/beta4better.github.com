---
layout: default
title: Yuan
tagline: rebuild from 2016
---
{% include JB/setup %}

This is Charles, here is my latest web page served on [Github](http://www.github.com), thanks for the help from 
[Jekyll Bootstrap](http://jekyllbootstrap.com). For much more personal information, you may find it 
[here](http://charles.beta4better.com).

Here's a list for the recent posts.

  <div class="row">
    {% for post in site.posts limit:9 %}
    <div class="col-xs-6 col-lg-4">
      <h2>{{ post.title }}</h2>
      <p>{{ post.excerpt }} </p>
      <p><a class="btn btn-default" href="{{ BASE_PATH }}{{ post.url }}" role="button">View details &raquo;</a></p>
    </div><!--/.col-xs-6.col-lg-4-->
    {% endfor %}
  </div><!--/row-->