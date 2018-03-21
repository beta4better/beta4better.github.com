---
layout: post
title: Enable Samba on Debian
date: '2016-02-02 04:16:54'
tags:
- debian
- samba
---

You may find a quite quick guide on the [Wiki of Debian](https://wiki.debian.org/SambaServerSimple). The most important thing we need to know is that, Samba used its own password system, so users need to be added by root first. And at the same time, the users have to exist in /etc/passwd already.

This is the first time for me to use [Samba](https://www.samba.org/), looks fine now. Just quote some words from its site to brief describe what is Samba.

> Samba is Free Software licensed under the GNU General Public License, the Samba project is a member of the Software Freedom Conservancy.

> Since 1992, Samba has provided secure, stable and fast file and print services for all clients using the SMB/CIFS protocol, such as all versions of DOS and Windows, OS/2, Linux and many others.

> Samba is an important component to seamlessly integrate Linux/Unix Servers and Desktops into Active Directory environments. It can function both as a domain controller or as a regular domain member.