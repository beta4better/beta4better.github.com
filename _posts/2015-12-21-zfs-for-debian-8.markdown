---
layout: post
title: ZFS for Debian 8
date: '2015-12-21 01:50:02'
tags:
- debian
- zfs
- jessie
---

````
root@debian:/home/beta4better# apt-cache search lsb-release
liblinux-distribution-perl - module for detecting the running Linux distribution
lsb-release - Linux Standard Base version reporting utility
root@debian:/home/beta4better# apt-get install lsb-release
Reading package lists... Done
Building dependency tree
Reading state information... Done
lsb-release is already the newest version.
lsb-release set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 67 not upgraded.
root@debian:/home/beta4better# wget http://archive.zfsonlinux.org/debian/pool/main/z/zfsonlinux/zfsonlinux_6_all.deb
--2015-12-21 09:47:07--  http://archive.zfsonlinux.org/debian/pool/main/z/zfsonlinux/zfsonlinux_6_all.deb
Resolving archive.zfsonlinux.org (archive.zfsonlinux.org)... 54.231.18.41
Connecting to archive.zfsonlinux.org (archive.zfsonlinux.org)|54.231.18.41|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2039658 (1.9M) [application/x-debian-package]
Saving to: ‘zfsonlinux_6_all.deb’

zfsonlinux_6_all.de 100%[===================>]   1.94M   108KB/s   in 18s

2015-12-21 09:47:30 (111 KB/s) - ‘zfsonlinux_6_all.deb’ saved [2039658/2039658]

root@debian:/home/beta4better# dpkg -i zfsonlinux_6_all.deb
Selecting previously unselected package zfsonlinux.
(Reading database ... 117929 files and directories currently installed.)
Preparing to unpack zfsonlinux_6_all.deb ...
Unpacking zfsonlinux (6) ...
Setting up zfsonlinux (6) ...

````