---
layout: post
title: "Running Jekyll on Mac OS X"
date: 2012-03-01 20:11
categories: [lion, jekyll, ruby, rvm, 1.8.7]
tags: [lion, jekyll, ruby, rvm, 1.8.7]
---

自从Mac买回来到现在差不多快一周了，装了一些软件，这两天在配置Jekyll环境，因为现在我主要使用Jekyll写点东西。完全静态的方法，只需要专心地在电脑上开个编辑器敲敲键盘就可以了。

Mac还是第一次用，之前折腾过一整子黑苹果。因为是黑苹果，装完之后各种不完美。最好的情况是只有声卡没有驱动起来。当时用的Intel的平台，不过后来电脑送给我弟弟了，买了个浩鑫的准系统，把处理器、内存、硬盘啥的都放进去了。现在手头没有Intel平台的电脑了，没法折腾了。

不过总的说来，用Mac快一周了，感觉真的很不错。唯一感觉不太好的是Terminal下各种命令和Linux完全不一样，虽然据我了解Mac应该是基于Unix的，可是还是不太一样。比如说，在Linux下删除一个目录一条命令就可以： `rm dir_name -rf`。但是在Mac下这条命令丝毫不起作用。还是得以后慢慢熟悉Mac。

言归正传，接下来还是说说如何在Mac下配置Jekyll的环境。

首先，安装[RVM](https://rvm.beginrescueend.com/support/)（Ruby Version Manager）。我对Mac的文件系统丝毫不了解，还是将ruby全部安装在自己的用户目录下比较好，不会影响整个系统，如果后期出现什么问题，直接把 `.rvm` 这个目录删掉就好了。

    bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
    echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
    source ~/.bash_profile

然后安装ruby 1.8.7。

    CC=/usr/bin/gcc-4.2 rvm install 1.8.7

最后安装Jekyll。

    gem install jekyll

上面的几个命令完成了之后Jekyll基本就可以用了，在这之前我还安装了Xcode，从App Store上下载的。还安装了[Git](http://git-scm.com/),主要是安装RVM的时候用。不过装完了之后在安装RVM的时候出现了一个错误提示： `make not found`。解决方法是安装一个叫做[osx-gcc-installer](https://github.com/kennethreitz/osx-gcc-installer/downloads)的文件，从这里下载

-   [https://github.com/downloads/kennethreitz/osx-gcc-installer/GCC-10.7-v2.pkg](https://github.com/downloads/kennethreitz/osx-gcc-installer/GCC-10.7-v2.pkg)

上面的问题解决了之后还出现一个问题

    .rvm/rubies/ruby-1.8.7-p334/lib/ruby/1.8/timeout.rb:60: [BUG] Segmentation fault

解决方法如下

    rvm remove 1.8.7
    rvm remove 1.8.7 --gems
    rvm remove 1.8.7 --archive
    CC=/usr/bin/gcc-4.2 rvm install 1.8.7

具体原因请参考下面的两个网站

-    http://jalada.co.uk/2011/07/24/lion-rvm-and-ruby-1-8-7-woes.html
-    http://miclle.me/posts/90

差不多就这几个问题吧，解决了Jekyll就可以用了。现在这篇就是在Mac下写的，还是挺方便的。不过从此看来Mac和Linux还是差别挺大的，至少在Terminal下Linux要比Mac方便好多，或许是我对Mac的了解还比较少吧。多多用Mac，慢慢就会都了解了，毕竟Linux用了好多年了，还算是熟悉。

至此，本篇结束。今天是3月1号，春天了吧，不过还是觉得凉凉的，蛋说是“春寒料峭”，哈哈，有道理。今天下雨了，想起了一句话

> 春雨贵如油

希望今年有个好收成、好年景！