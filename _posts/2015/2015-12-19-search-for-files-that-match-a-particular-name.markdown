---
layout: post
title: Search for files that match a particular name
date: '2015-12-19 02:34:38'
tags:
- find
- freebsd-2
---

To search for files that match a particular name, use find(1); for example

        find / -name "*GENERIC*" -ls

will search '/', and all subdirectories, for files with 'GENERIC' in the name.