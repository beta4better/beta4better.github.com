---
layout: post
title: 在 ESXi 安装镜像中集成 RealTek 网卡驱动
date: '2014-08-14 08:58:43'
tags:
- realtek
- esxi-2
---

如果你用的是那种标准的服务器来安装 ESXi，那么可能不会遇到这种问题。大的厂家，像戴尔、惠普一般会自己定制安装镜像。像个人用户一般自己组建 Home Lab 的话购买的主板一般都会是带 RealTek 的网卡，那么安装 ESXi 的时候就会遇到和我一样的问题了---网卡没有驱动。

先解释一个名词：VIB 全称是 vSphere Installation Bundle

接下来介绍如果来集成网卡驱动。

## 资源准备 ##

  1. ESXi-Customizer，下载地址为 http://www.v-front.de/p/esxi-customizer.html 。
  
  2. ESXi 原始安装镜像： VMware-VMvisor-Installer-5.5.0-1331820.x86_64.iso，请自行从 VMWare 的网站上下载: https://my.vmware.com/group/vmware/home 。
  
  3. Offline Bundle：update-from-esxi5.1-5.1_update02.zip，下载地址为： https://my.vmware.com/group/vmware/patch ，请自行注册帐号。 

如果你的系统为 Windows 那么可能还要用到 UltraISO 和  Unetbootin 这两个工具。

Windows 下全部资源准备齐套后如下：

![](/content/images/2014/Aug/esxi-offline-bundle.png)

所有支持的网卡如下，这里我们需要用到 `net-r8168` 和 `net-r8168` 这两个。

![](/content/images/2014/Aug/esxi-realtek-driver.png)

## 驱动集成 ##

启动 ESXi-Customizer-v2.7.2\ESXi-Customizer.cmd 选择相应的文件，点击 `RUN` 就可以了。不过一次只能集成一个驱动，我们要运行两次。

![](/content/images/2014/Aug/esxi-customer.png)

![](/content/images/2014/Aug/esxi-customer-2.png)

然后就可以在带 RealTek 的机器上安装 ESXi 了。


## 参考链接 ##

  - [http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2005205]()
  - [http://www.tinkertry.com/use-esxi-customizer-gui-to-inject-multiple-driver-vibs-into-your-esxi-installer-iso/]()
  - [http://wiki.daveking.com/index.php?title=Adding_Third_Party_Drivers_To_A_VMware_vSphere/ESXi_5_Installation_ISO]()
  - [http://nolabnoparty.com/upgrade-esxi-5-5-update-1/]()
  - [http://alexander.walden.de/2012/01/18/making-your-own-esxi-5-installation-image/]()


