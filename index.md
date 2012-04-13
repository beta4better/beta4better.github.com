---
layout: page
title: "Welcome!"
---

![我的那些花儿](/assets/images/start-2011-400x300.png "我的那些花儿 全家福")

首先，欢迎。

右边的图片是我养的[滴水观音][flower]，不过这是2011年的时候用我的手机：SAMSUNG SCH-S239照的，还算挺清楚的。

这里是我在网络上的一个据点，[域名][me]是在2010年9月10日的时候从[godaddy](https://www.godaddy.com/default.aspx)购买来的。当时就是想拿来搭建个博客什么的，用来随便写点什么东西，结果两年过去了却什么也没有保存下来。一开始的时候用的是[wordpress](http://wordpress.org/)，然后用了一段时间的[movabletype](http://www.movabletype.org/)，再接下来有一段时间在用[project picky](http://picky.olivida.com/picky)，现在换成了[jekyll](http://jekyllrb.com/)，就是现在的这个了。主题是我自己改的，使用了[mark reid](http://mark.reid.name/)和[all things distributed](http://www.allthingsdistributed.com/)的一些代码，CSS的框架使用的是[getskeleton](http://getskeleton.com/)。这是自己第一次写主题啥的，对于HTML和CSS有许多代码还是看不太懂，先这么用着吧，不能只顾大而全，框架搭起来，内容才是关键。

下面的这些是使用[jekyll]:[jekyll]后写的一些文章，或许是一些只言片语，或许是些长篇大论，如果你想通篇阅读，请点击[这里](/archives.html)。建议在午夜的时候进行，会很长的哦。

<ul class="square">
	{% for post in site.posts limit:10%}
	<!--<li><span class="two columns">{{ post.date | date: "%b %e, %Y"}}</span><span><a href="{{ post.url }}">{{ post.title }}</a></span></li>-->
	<!--<li><span>{{ post.date | date: "%B %e, %Y" }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>-->
	<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endfor %}
</ul>

关于我，如果你想了解更多的，细节轻前往[这里][about]，[这里][about]有一些比较完整的介绍。

我现在开始喜欢[养花][flower]了，偶尔也会玩玩[魔兽世界][wow]，有兴趣的话，轻看看[这里][flower]和[这里][wow]。

[about]: /about.html "About Me"
[me]: http://www.beta4better.me/ "beta4better.me"
[jekyll]: http://jekyllrb.com/ "Jekyll"
[flower]: /flower.html "我的那些花儿"
[wow]: /twow.html "魔兽世界 台服"
