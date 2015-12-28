---
layout: post
title: "Debian Squeeze Chinese Howto"
date: 2012-03-05 16:47
categories: [debian, squeeze, chinese, howto]
tags: [debian, squeeze, chinese, howto]
---

After install [Debian Squeeze on my ThinkPad](/2012/02/install-debian-squeeze-on-thinkpad-x201i.html), the first things I have to do is to install some chinese fonts, in order the chinese character display well.

    sudo aptitude install ttf-dejavu ttf-wqy-zenhei xfonts-wqy ttf-wqy-microhei ttf-arphic-ukai ttf-arphic-uming

And then the second is to install the chinese input method to write blog in Chinese, while not only English, as Chinese is my monther language.

    sudo aptitude install scim scim-tables-zh scim-pinyin

Now, the chinese character maybe display well, if you do want to use the fonts of Microsoft Windows, take a look at the following guide.

*   [http://edyfox.codecarver.org/html/debian_testing_chinese.html](http://edyfox.codecarver.org/html/debian_testing_chinese.html)

The final result comes here: 

<a href="/2012/02/thinkpad-x201i-upgrade.html"><img src="/assets/images/2012/03/thinkpad-x201i-upgrade-chromium.png" class="center" width="480px" /></a>