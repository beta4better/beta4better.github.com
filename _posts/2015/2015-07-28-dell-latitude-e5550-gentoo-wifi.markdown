---
layout: post
title: Dell Latitude E5550 Gentoo WiFi
date: '2015-07-28 08:08:20'
tags:
- intel
- dell
- latitude
- gentoo
- e5550
---

参考下 [Gentoo Wiki](https://wiki.gentoo.org/wiki/Lenovo_Thinkpad_E550) 上的 Lenovo Thinkpad E550 的页面。

	Device Drivers  --->
	  SCSI device support  --->
		<*> SCSI disk support
	  <*> Serial ATA and Parallel ATA drivers  --->
		<*> AHCI SATA support
	  [*] Network device support  --->
		[*] Ethernet driver support  --->
		  [*] Intel devices
			<*> Intel(R) PRO/1000 PCI-Express Gigabit Ethernet support
		[*] Wireless LAN  --->
		  <M> Intel Wireless WiFi Next Gen AGN - Wireless-N/Advanced-N/Ultimate-N (iwlwifi)
		  <M> Intel Wireless WiFi MVM Firmware support

照着重新编译完内核重启后竟然能够看到无线网卡了。