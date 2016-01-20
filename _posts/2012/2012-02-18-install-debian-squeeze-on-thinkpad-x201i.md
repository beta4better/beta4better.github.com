---
layout: post
title: "Install Debian Squeeze on ThinPad X201i"
date: 2012-02-18 16:06
categories: [thinkpad, debian, squeeze]
tags: [thinkpad, debian, squeeze]
---

## Introduction ##

*ThinkPad X201i is a 12inch laptop without CD-ROM, so I have to use the USB disk to install the operating system.*

**ThinkPad X201i Spec:**

-   CPU: Intel(R) Celeron(R) CPU U3400 @ 1.07GHz
-   Memory: [2GB upgrade to 8GB](/2012/02/thinkpad-x201i-upgrade.html)
-   HD: WDC WD2500BEVT-08A23T1

I really want upgrade the HD to SSD, but not allowed yet.

**OS:**

-   Debian Squeeze:  *debian-6.0.3-amd64-businesscard.iso*

**Boot tool:**

-   UNetBoot: *unetbootin-windows-563.exe*
-   USB Disk

I use the windows version of UNetBoot, as the linux editon seems not work well. 

Write the *debian-6.0.3-amd64-businesscard.iso* to USB disk, boot the laptop with the USB disk, choose expert mode to install Debian using the stable edition: Squeeze. I also try the testing version, diff greatly, I used to Squeeze and Lenny.

Just install the base system, and then boot to the operating system, continous to install the other wares.

## Desktop Enviroment

The command line mode is OK for server, but not so convenient for daily use. So the desktop enviroment is necessary, I choose the xfce4, light and quick. Install xfce4 is easy, just type:

    sudo aptitude install xfce4
    
If you want to use some tools provided by xfce4, such as get the temp of HDD type:

    sudo aptitude install xfce4-goodies

Then you can get the temp of you disk using :

    sudo hddtemp /dev/sda
    /dev/sda: WDC WD2500BEVT-08A23T1: 34°C

If you do not want to type startx after you login, install the xdm:

    sudo aptitude install xdm

There are many display manager, such as gdm or slim, xdm is just simple enough for my use. 

Now you get a working linux desktop system. Help yourself!
