---
layout: post
title: "Type Chinese in emacs under English locale"
date: 2012-03-05 19:29
categories: [chinese, emacs]
tags: [chinese, emacs]
---

In order to type Chinese in emacs under English locale, you have to launch emacs with LANG set to zh_CN.UTF8: 

    LANG=zh_CN.UTF8 emacs
    
But first you have generate the zh_CN.UTF8 locale:

    sudo dpkg-reconfigure locales
