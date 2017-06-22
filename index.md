---
layout: default
title: Weblog for Charles
tagline: rebuild from 2016
---
<p class="pull-right visible-xs"><button type="button" class="btn btn-primary btn-xs" data-toggle="offcanvas">Toggle nav</button></p>

<div class="jumbotron">
  <p>This is my latest web page served on <a href="http://www.github.com">Github</a>, build with <a href="http://jekyllrb.com/">Jekyll</a>, <a href="http://jekyllbootstrap.com">Jekyll Bootstrap</a> and <a href="http://getbootstrap.com/">Bootstrap</a>. Please look around, you may find something fun. Just <a href="mailto:beta4better@gmail.com">let me know</a> if you wish.</p>
</div>

<div class="row blog-main">
  {% for post in site.posts limit:9 %}
    <div class="col-xs-6 col-lg-4 blog-post">
      <h2 class="blog-post-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p class="blog-post-meta">{{ post.date | date_to_long_string }} by {{ site.author.name }}</p>
      {{ post.excerpt }}
      <!--<p><a class="btn btn-default" href="#" role="button">View details &raquo;</a></p>-->
    </div><!-- /.blog-post --><!--/.col-xs-6.col-lg-4-->
  {% endfor %}

</div><!--/row-->

{% include JB/setup %}
