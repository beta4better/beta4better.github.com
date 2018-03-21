---
layout: post
title: How to enable PHP SQLite support in Gentoo
date: '2015-08-22 02:44:07'
tags:
- php
- sqlite
- mediawiki
- gentoo
---

> SQLite is a lightweight database system that is very well supported. (How to compile PHP with SQLite support, uses PDO)

Use the follow USE set for php and mediawiki package.

	# required by www-apps/mediawiki-1.23.8::gentoo[-imagemagick]
	# required by www-apps/mediawiki (argument)
	>=dev-lang/php-5.6.12 gd xmlreader odbc

	# required by www-apps/mediawiki-1.23.8::gentoo
	# required by mediawiki (argument)
	>=dev-lang/php-5.6.12 pdo sqlite mysql

	>=www-apps/mediawiki-1.23.8 imagemagick mysql sqlite


