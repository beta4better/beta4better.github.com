---
layout: post
title: FreeBSD ZFS Root
date: '2013-07-04 20:39:12'
---

https://calomel.org/zfs-freebsd-root-install.html

http://www.aisecure.net/2012/01/16/rootzfs

<code>$ cat /etc/make.conf
WITH_PKGNG="YES"
WITH_NEW_XORG="YES"
WITH_PKGNG="YES"</code>

<code>$ cat /etc/rc.conf
hostname="shuttle"
ifconfig_re0="DHCP"
sshd_enable="YES"
moused_enable="YES"
ntpd_enable="YES"
powerd_enable="YES"
# Set dumpdev to "AUTO" to enable crash dumps, "NO" to disable
dumpdev="NO"
hald_enable="YES"
dbus_enable="YES"
sendmail_enable="NONE"
#kdm4_enable="YES"
# -- sysinstall generated deltas -- # Thu May 2 20:53:32 2013
#ifconfig_re0="inet 192.168.1.1 netmask 255.255.255.0"
#defaultrouter="192.168.1.105"
#hostname="shuttle"
gdm_enable="YES"
gnome_enable="YES"
vboxnet_enable="YES"
devfs_system_ruleset="system"</code>