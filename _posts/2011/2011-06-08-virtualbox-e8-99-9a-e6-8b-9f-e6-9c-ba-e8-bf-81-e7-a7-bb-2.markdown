---
layout: post
title: VirtualBoxXu Ni Ji Qian Yi Hou Zhong Xin Qi Yong Wang Qia
date: '2011-06-08 18:46:00'
tags:
- debian
- uuid-2
---

<p>在一台机器上用VirtualBox安装Debian，如果把这个Deian转移到另一台装有VirtualBox的机器上会发现启动后不能链接网络了，只需要删除这个文件就可以：</p>

<p><code>/etc/udev/rules.d/70-persistent-net.rules</code></p>

<p>貌似是UUID的问题，不过没有仔细研究过。</p>