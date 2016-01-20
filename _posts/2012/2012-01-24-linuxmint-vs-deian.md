---
layout: post
title: "LinuxMint vs Debian"
categories : [debian, linuxmint]
tags : [debian, linuxmint]
---

已经晚上9点多了，我叔今天来了，住下了。已经在另一个屋的炕上和我奶奶睡了。

今天太阳还算暖和，风也小了些。

晚上没事把LinuxMint下的所有的配置文件都删掉了，结果xfce的桌面变成了默认的，
没有了原来的华丽，只得自己手工从头开始配置。
只添加了一个面板，加上了几个基本的工具，凑活着先用吧，加多了也是无用。

现在的系统用的是LinuxMint：

    Linux mint 3.0.0-1-amd64

默认的源是：

    deb http://packages.linuxmint.com/ debian main upstream import
    deb http://debian.linuxmint.com/latest testing main contrib non-free
    deb http://security.debian.org/ testing/updates main contrib non-free
    deb http://www.debian-multimedia.org testing main non-free

里面大多数都是testing的东西，感觉不怎么放心，有在考虑是不是有必要换回到Debian的stable源，
因为现在的vps上用的全都是Debian stable，如果换成一样的本地测试OK的就可以直接迁移到服务器上去了。

我也有在考虑是不是有必要给笔记本再加一条内存，现在感觉2GB的貌似不太够用。
