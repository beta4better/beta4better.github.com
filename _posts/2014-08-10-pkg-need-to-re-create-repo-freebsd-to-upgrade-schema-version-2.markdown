---
layout: post
title: 'pkg: need to re-create repo FreeBSD to upgrade schema version'
date: '2014-08-10 00:32:30'
tags:
- pkg
- freebsd-2
---

如果你也遇到这样的问题，那么解决方法如下：

    # pkg upgrade
	Updating repository catalogue
	FreeBSD repository is up-to-date
	All repositories are up-to-date
	pkg: Repo FreeBSD needs schema upgrade from 2006 to 2010 but it is opened readonly
	pkg: need to re-create repo FreeBSD to upgrade schema version
	Checking for upgrades: 100%
	Checking integrity... done (0 conflicting)
	# pkg update -f
	Updating repository catalogue
	Fetching meta.txz: 100% of 944 B                                                                    
	Fetching digests.txz: 100% of 1 MB                                                                   
	Fetching packagesite.txz: 100% of 5 MB                                                               

	Adding new entries: 100%
	Incremental update completed, 23313 packages processed:
	0 packages updated, 0 removed and 23313 added.
