---
layout: post
title: How to Extend a FreeBSD zpool
date: '2016-02-21 12:47:11'
tags:
- zfs
- zpool
- freebsd-2
---

写这篇文章的目的是为了记录下在 FreeBSD 下如何扩充一个 zpool 的存储池（或者或是 ZFS 的文件系统）。个人对 zpool/ZFS 的理解目前还不是那么的完全，关键在于平时很少接触到，已经配置好的如果不出什么问题也不会做什么深入的了解，够用、能用了就基本差不多了，目前还涉及到任何性能的问题。 

就目前我个人了解到的知识体系来说，我想到的一种比较优化的使用场景：四块乃更多快同样容量的机械硬盘组成一个 raidz2 的阵列，然后那额外一块 SSD 硬盘做一个高速缓存，我记得在 zpool 的 manpage 里看到过类似这样的配置。如果将来有机会可以尝试下，不过对普通个人电脑来说小机箱很难找到这样合适的机箱。 目前看来 HP 的 Micro Server [Gen8]() （暂时保留一个链接，以后补上一个对Gen8的介绍。个人在京东买了一台） 貌似是个不错的选择。

从网上搜到了一个介绍 RAID 信息的一些问题，FreeBSD 的 raidz2 应该是等同于 RAID5 的，容错量应该是两块硬盘---也就是说允许同一时间有两块硬盘坏掉。不过没做过这样的尝试，但是前两天遇到了系统启动时突然找不到跟文件系统的情况，多重启两次就好了，不知是何原因。启动后发现 zpool 在修复一块硬盘上的数据。

- RAID0：N块盘组成，逻辑容量为N块盘容量之和；
- RAID1：两块盘组成，逻辑容量为一块盘容量；
- RAID3：N+1块盘组成，逻辑容量为N块盘容量之和；
- RAID5：N块盘组成，逻辑容量为N-1块盘容量之和；
- RAID6：N块盘组成，逻辑容量为N-2块盘容量之和；
- RAID10：2N块盘组成，逻辑容量为N块盘容量之和；
- RAID50：假每个RAID5由N块盘组成，共有M个RAID5组成该RAID50，则逻辑容量为(N-1)*M块盘容量之和。

首先介绍一些基本的信息。我这台机器是富士通的入门级服务器（）。原配有 Xeon E1245 的 CPU，两条 4GB 的 ECC 内存，外加一块西部数据的 500G 硬盘。我有外加了3块硬盘组了 raidz2 阵列。安装了 FreeBSD 10.2 的系统，选择安装向导里的 ZFS 安装，未选择硬盘加密。

在做扩充之前机器上已经有了很多数据，为了不出意外先在虚拟机上做了实验。虚拟机上的系统信息如下：

    FreeBSD 10.2-RELEASE (GENERIC) #0 r286666: Wed Aug 12 15:26:37 UTC 2015

    Welcome to FreeBSD!

    Release Notes, Errata: https://www.FreeBSD.org/releases/
    Security Advisories:   https://www.FreeBSD.org/security/
    FreeBSD Handbook:      https://www.FreeBSD.org/handbook/
    FreeBSD FAQ:           https://www.FreeBSD.org/faq/
    Questions List: https://lists.FreeBSD.org/mailman/listinfo/freebsd-questions/
    FreeBSD Forums:        https://forums.FreeBSD.org/

    Documents installed with the system are in the /usr/local/share/doc/freebsd/
    directory, or can be installed later with:  pkg install en-freebsd-doc
    For other languages, replace "en" with a language code like de or fr.

    Show the version of FreeBSD installed:  freebsd-version ; uname -a
    Please include that output and any error messages when posting questions.
    Introduction to manual pages:  man man
    FreeBSD directory layout:      man hier

    Edit /etc/motd to change this login announcement.
    Ever wonder what those numbers after command names were, as in cat(1)?  It's
    the section of the manual the man page is in.  "man man" will tell you more.
                    -- David Scheidt <dscheidt@tumbolia.com>

上面是 shell 登录后看到第一段文字，了解个基本的版本信息就好了。 **FreeBSD 10.2-RELEASE (GENERIC) #0 r286666**

默认的分区情况如下，使用了系统自带的安装向导，选择了 ZFS 安装，选择了数据加密，SWAP 分区未选择加密。

    $ df -h
    Filesystem            Size    Used   Avail Capacity  Mounted on
    zroot/ROOT/default     25G    2.6G     22G    10%    /
    devfs                 1.0K    1.0K      0B   100%    /dev
    bootpool              1.9G    509M    1.4G    26%    /bootpool
    zroot/tmp              22G     45M     22G     0%    /tmp
    zroot/usr/home         23G    271M     22G     1%    /usr/home
    zroot/usr/ports        23G    900M     22G     4%    /usr/ports
    zroot/usr/src          22G    140K     22G     0%    /usr/src
    zroot/var/audit        22G    140K     22G     0%    /var/audit
    zroot/var/crash        22G    140K     22G     0%    /var/crash
    zroot/var/log          22G    645K     22G     0%    /var/log
    zroot/var/mail         22G    192K     22G     0%    /var/mail
    zroot/var/tmp          22G    140K     22G     0%    /var/tmp
    zroot                  22G    140K     22G     0%    /zroot

通过 `zpool list` 命令可以看到系统创建了两个存储池，一个 **bootpool**，另一个是 **zroot**。坦白讲写这篇文章的时候我还是对这个磁盘的容量大小还是不很清楚。

    $ zpool list
    NAME       SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
    bootpool  1.98G   510M  1.49G         -    18%    25%  1.00x  DEGRADED  -
    zroot     55.5G  7.74G  47.8G         -     4%    13%  1.00x  DEGRADED  -

`zfs` 命令可以看到分区都是默认的，没有做任何调整。

    $ zfs list
    NAME                 USED  AVAIL  REFER  MOUNTPOINT
    bootpool             510M  1.42G   509M  /bootpool
    zroot               3.75G  22.3G   140K  /zroot
    zroot/ROOT          2.56G  22.3G   140K  none
    zroot/ROOT/default  2.56G  22.3G  2.56G  /
    zroot/tmp           44.7M  22.3G  44.7M  /tmp
    zroot/usr           1.14G  22.3G   140K  /usr
    zroot/usr/home       271M  22.3G   271M  /usr/home
    zroot/usr/ports      900M  22.3G   900M  /usr/ports
    zroot/usr/src        140K  22.3G   140K  /usr/src
    zroot/var           1.37M  22.3G   140K  /var
    zroot/var/audit      140K  22.3G   140K  /var/audit
    zroot/var/crash      140K  22.3G   140K  /var/crash
    zroot/var/log        651K  22.3G   651K  /var/log
    zroot/var/mail       192K  22.3G   192K  /var/mail
    zroot/var/tmp        140K  22.3G   140K  /var/tmp 

`ls` 命令可以看到有四块硬盘。分别是 da0，da1，da2 和 da3. 这里个人不是很明白的就是为什么 /dev/da0p4 之后还跟着一个 /dev/da0p4.eli
 
    $ ls /dev/da*
    /dev/da0        /dev/da0p4      /dev/da1p2      /dev/da2        /dev/da2p4
    /dev/da0p1      /dev/da0p4.eli  /dev/da1p3      /dev/da2p1      /dev/da2p4.eli
    /dev/da0p2      /dev/da1        /dev/da1p4      /dev/da2p2      
    /dev/da0p3      /dev/da1p1      /dev/da1p4.eli  /dev/da2p3 

`zpool status` 可以看到组成 **zroot** 的是 /dev/da0p4.eli，/dev/db0p4.eli，/dev/dc0b4.eli，/dev/dd0p4.eli，而不是  /dev/da0p4，/dev/db0p4，/dev/dc0b4，/dev/dd0p4，没想明白。已经可以看到有一个硬盘已经处于了 **UNAVAIL** 的状态，而且两个 pool 都是在降级 **DEGRADED** 运行。

    $ zpool status
      pool: bootpool
     state: DEGRADED
    status: One or more devices could not be opened.  Sufficient replicas exist for
            the pool to continue functioning in a degraded state.
    action: Attach the missing device and online it using 'zpool online'.
       see: http://illumos.org/msg/ZFS-8000-2Q
      scan: resilvered 172K in 0h0m with 0 errors on Wed Dec 23 23:27:09 2015
    config:

            NAME                      STATE     READ WRITE CKSUM
            bootpool                  DEGRADED     0     0     0
              mirror-0                DEGRADED     0     0     0
                14532417844132395237  UNAVAIL      0     0     0  was /dev/da0p2
                gpt/boot1             ONLINE       0     0     0
                gpt/boot2             ONLINE       0     0     0
                gpt/boot3             ONLINE       0     0     0

    errors: No known data errors

      pool: zroot
     state: DEGRADED
    status: One or more devices could not be opened.  Sufficient replicas exist for
            the pool to continue functioning in a degraded state.
    action: Attach the missing device and online it using 'zpool online'.
       see: http://illumos.org/msg/ZFS-8000-2Q
      scan: resilvered 600K in 0h0m with 0 errors on Wed Dec 23 23:27:06 2015
    config:

            NAME                      STATE     READ WRITE CKSUM
            zroot                     DEGRADED     0     0     0
              raidz2-0                DEGRADED     0     0     0
                13574931247595481435  UNAVAIL      0     0     0  was /dev/da0p4.eli
                da0p4.eli             ONLINE       0     0     0
                da1p4.eli             ONLINE       0     0     0
                da2p4.eli             ONLINE       0     0     0

    errors: No known data errors

从 `diskinfo` 的输出可以看出硬盘的大小是 20G。

    root@freebsd:~ # diskinfo /dev/da0
    /dev/da0        512     21474836480     41943040        0       0       2610    255     63
    root@freebsd:~ # diskinfo -v /dev/da0
    /dev/da0
            512             # sectorsize
            21474836480     # mediasize in bytes (20G)
            41943040        # mediasize in sectors
            0               # stripesize
            0               # stripeoffset
            2610            # Cylinders according to firmware.
            255             # Heads according to firmware.
            63              # Sectors according to firmware.
                            # Disk ident.

至于硬盘的分区，通过 gpart 的输出可以看到四个分区，一个是 freebsd-boot 格式，一个是 freebsd-swap，两个 freebsd-zfs，一个用给根目录，一个用给家目录。跟目录是不加密的，家目录是加密的，这是我后来才了解到的信息。貌似系统是不能从加密的根目录直接启动的。信息的准确性还有待于进一步研究。

    root@freebsd:~ # gpart show da0
    =>      34  41942973  da0  GPT  (20G)
            34         6       - free -  (3.0K)
            40      1024    1  freebsd-boot  (512K)
          1064       984       - free -  (492K)
          2048   4194304    2  freebsd-zfs  (2.0G)
       4196352   8388608    3  freebsd-swap  (4.0G)
      12584960  29356032    4  freebsd-zfs  (14G)
      41940992      2015       - free -  (1.0M)

每个硬盘上都分了一个 4GB 大小的交换分区，后来从 top 的输出信息来看，交换分区的大小是 16GB，也就是四个硬盘上的交换分区加起来计算的容量，这个不理解。

    root@freebsd:~ # cat /etc/fstab
    # Device                Mountpoint      FStype  Options         Dump    Pass#
    /dev/da0p3              none    swap    sw              0       0
    /dev/da1p3              none    swap    sw              0       0
    /dev/da2p3              none    swap    sw              0       0
    /dev/da3p3              none    swap    sw              0       0

接下来添加一块硬盘，然后通过 `gpart` 把一块没问题的硬盘的分区表原封不动的恢复到新硬盘上来，在这里它的标号是 **da3**.

    root@freebsd:~ # gpart backup da0 | gpart restore -F da3

可以看下新的硬盘分区情况，/dev/da3 已经按照 /dev/da0 的分区样式划分好了分区，但是奇怪的是 /devda3p4.eli 没有出来，不解！

    root@freebsd:~ # ls /dev/da*
    /dev/da0        /dev/da1        /dev/da2        /dev/da3
    /dev/da0p1      /dev/da1p1      /dev/da2p1      /dev/da3p1
    /dev/da0p2      /dev/da1p2      /dev/da2p2      /dev/da3p2
    /dev/da0p3      /dev/da1p3      /dev/da2p3      /dev/da3p3
    /dev/da0p4      /dev/da1p4      /dev/da2p4      /dev/da3p4
    /dev/da0p4.eli  /dev/da1p4.eli  /dev/da2p4.eli

我在这里重启了一次系统： `root@freebsd:~ # reboot`

`zpool status` 看一下最新的信息，方便下面替换。

    $ zpool status
      pool: bootpool
     state: DEGRADED
    status: One or more devices could not be opened.  Sufficient replicas exist for
            the pool to continue functioning in a degraded state.
    action: Attach the missing device and online it using 'zpool online'.
       see: http://illumos.org/msg/ZFS-8000-2Q
      scan: resilvered 172K in 0h0m with 0 errors on Wed Dec 23 23:27:09 2015
    config:

            NAME                      STATE     READ WRITE CKSUM
            bootpool                  DEGRADED     0     0     0
              mirror-0                DEGRADED     0     0     0
                14532417844132395237  UNAVAIL      0     0     0  was /dev/da0p2
                gpt/boot1             ONLINE       0     0     0
                gpt/boot2             ONLINE       0     0     0
                gpt/boot3             ONLINE       0     0     0

    errors: No known data errors

      pool: zroot
     state: DEGRADED
    status: One or more devices could not be opened.  Sufficient replicas exist for
            the pool to continue functioning in a degraded state.
    action: Attach the missing device and online it using 'zpool online'.
       see: http://illumos.org/msg/ZFS-8000-2Q
      scan: scrub repaired 0 in 0h18m with 0 errors on Thu Jan 28 03:50:46 2016
    config:

            NAME                      STATE     READ WRITE CKSUM
            zroot                     DEGRADED     0     0     0
              raidz2-0                DEGRADED     0     0     0
                13574931247595481435  UNAVAIL      0     0     0  was /dev/da0p4.eli
                da0p4.eli             ONLINE       0     0     0
                da1p4.eli             ONLINE       0     0     0
                da2p4.eli             ONLINE       0     0     0

    errors: No known data errors

首先替换 zroot 存储池： 

    root@freebsd:/usr/home/beta4better # zpool replace zroot 13574931247595481435 da3p4
    Make sure to wait until resilver is done before rebooting.

    If you boot from pool 'zroot', you may need to update
    boot code on newly attached disk 'da3p4'.

    Assuming you use GPT partitioning and 'da0' is your new boot disk
    you may use the following command:

            gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 1 da0

按照提示信息执行下 `gpart bootcode` 操作：

    root@freebsd:/usr/home/beta4better # gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 1 da3
    bootcode written to da3

打开 autoexpend 选项，为后面扩容做准备。这是后来才注意到的这个属性设置。

    root@freebsd:/usr/home/beta4better # zpool set autoexpand=on bootpool

`zpool status` 可以看到 zroot 存储池已经开始恢复数据了。

    root@freebsd:/usr/home/beta4better # zpool status
      pool: bootpool
     state: DEGRADED
    status: One or more devices could not be opened.  Sufficient replicas exist fo                   r
            the pool to continue functioning in a degraded state.
    action: Attach the missing device and online it using 'zpool online'.
       see: http://illumos.org/msg/ZFS-8000-2Q
      scan: resilvered 172K in 0h0m with 0 errors on Wed Dec 23 23:27:09 2015
    config:

            NAME                      STATE     READ WRITE CKSUM
            bootpool                  DEGRADED     0     0     0
              mirror-0                DEGRADED     0     0     0
                14532417844132395237  UNAVAIL      0     0     0  was /dev/da0p2
                gpt/boot1             ONLINE       0     0     0
                gpt/boot2             ONLINE       0     0     0
                gpt/boot3             ONLINE       0     0     0

    errors: No known data errors

      pool: zroot
     state: DEGRADED
    status: One or more devices is currently being resilvered.  The pool will
            continue to function, possibly in a degraded state.
    action: Wait for the resilver to complete.
      scan: resilver in progress since Thu Jan 28 04:03:52 2016
            199M scanned out of 7.79G at 3.16M/s, 0h41m to go
            48.9M resilvered, 2.49% done
    config:

            NAME                        STATE     READ WRITE CKSUM
            zroot                       DEGRADED     0     0     0
              raidz2-0                  DEGRADED     0     0     0
                replacing-0             UNAVAIL      0     0     0
                  13574931247595481435  UNAVAIL      0     0     0  was /dev/da0p4                   .eli
                  da3p4                 ONLINE       0     0     0  (resilvering)
                da0p4.eli               ONLINE       0     0     0
                da1p4.eli               ONLINE       0     0     0
                da2p4.eli               ONLINE       0     0     0

    errors: No known data errors

接下来把 bootpool 里的分区也替换下：

    root@freebsd:/usr/home/beta4better # zpool replace bootpool 14532417844132395237 da3p2

可以看到 zroot 和 bootpool 两个存储池都开始了数据恢复。

    root@freebsd:/usr/home/beta4better # zpool status
      pool: bootpool
     state: DEGRADED
    status: One or more devices is currently being resilvered.  The pool will
            continue to function, possibly in a degraded state.
    action: Wait for the resilver to complete.
      scan: resilver in progress since Thu Jan 28 04:06:17 2016
            62.0M scanned out of 510M at 3.10M/s, 0h2m to go
            59.7M resilvered, 12.16% done
    config:

            NAME                        STATE     READ WRITE CKSUM
            bootpool                    DEGRADED     0     0     0
              mirror-0                  DEGRADED     0     0     0
                replacing-0             UNAVAIL      0     0     0
                  14532417844132395237  UNAVAIL      0     0     0  was /dev/da0p2
                  da3p2                 ONLINE       0     0     0  (resilvering)
                gpt/boot1               ONLINE       0     0     0
                gpt/boot2               ONLINE       0     0     0
                gpt/boot3               ONLINE       0     0     0

    errors: No known data errors

      pool: zroot
     state: DEGRADED
    status: One or more devices is currently being resilvered.  The pool will
            continue to function, possibly in a degraded state.
    action: Wait for the resilver to complete.
      scan: resilver in progress since Thu Jan 28 04:03:52 2016
            581M scanned out of 7.79G at 3.52M/s, 0h34m to go
            144M resilvered, 7.29% done
    config:

            NAME                        STATE     READ WRITE CKSUM
            zroot                       DEGRADED     0     0     0
              raidz2-0                  DEGRADED     0     0     0
                replacing-0             UNAVAIL      0     0     0
                  13574931247595481435  UNAVAIL      0     0     0  was /dev/da0p4.eli
                  da3p4                 ONLINE       0     0     0  (resilvering)
                da0p4.eli               ONLINE       0     0     0
                da1p4.eli               ONLINE       0     0     0
                da2p4.eli               ONLINE       0     0     0

    errors: No known data errors

新旧磁盘的对比，可以看到两个的分区是完全一样。

    root@freebsd:/usr/home/beta4better # gpart show da0
    =>      34  41942973  da0  GPT  (20G)
            34         6       - free -  (3.0K)
            40      1024    1  freebsd-boot  (512K)
          1064       984       - free -  (492K)
          2048   4194304    2  freebsd-zfs  (2.0G)
       4196352   8388608    3  freebsd-swap  (4.0G)
      12584960  29356032    4  freebsd-zfs  (14G)
      41940992      2015       - free -  (1.0M)

    root@freebsd:/usr/home/beta4better # gpart show da3
    =>      34  41942973  da3  GPT  (20G)
            34         6       - free -  (3.0K)
            40      1024    1  freebsd-boot  (512K)
          1064       984       - free -  (492K)
          2048   4194304    2  freebsd-zfs  (2.0G)
       4196352   8388608    3  freebsd-swap  (4.0G)
      12584960  29356032    4  freebsd-zfs  (14G)
      41940992      2015       - free -  (1.0M)

放了几个小时后就可以看到数据恢复完了。1.87G 的数据花了两小时三分钟。

    root@freebsd:/usr/home/beta4better # zpool status
      pool: bootpool
     state: ONLINE
      scan: resilvered 510M in 0h1m with 0 errors on Thu Jan 28 04:08:11 2016
    config:

            NAME           STATE     READ WRITE CKSUM
            bootpool       ONLINE       0     0     0
              mirror-0     ONLINE       0     0     0
                da3p2      ONLINE       0     0     0
                gpt/boot1  ONLINE       0     0     0
                gpt/boot2  ONLINE       0     0     0
                gpt/boot3  ONLINE       0     0     0

    errors: No known data errors

      pool: zroot
     state: ONLINE
      scan: resilvered 1.87G in 2h3m with 0 errors on Thu Jan 28 06:07:20 2016
    config:

            NAME           STATE     READ WRITE CKSUM
            zroot          ONLINE       0     0     0
              raidz2-0     ONLINE       0     0     0
                da3p4      ONLINE       0     0     0
                da0p4.eli  ONLINE       0     0     0
                da1p4.eli  ONLINE       0     0     0
                da2p4.eli  ONLINE       0     0     0

    errors: No known data errors

至此硬盘替换完成。验证了我自己的一个思路是正确的。接下来是扩容的操作。把 da0 用一块容量为 40G 的硬盘替换掉。 同样的操作方式，只不过在硬盘的最后方会有一个 20G 的空余容量。如下所示：

    root@freebsd:~ # gpart show da0
    =>      34  83886013  da0  GPT  (40G)
            34         6       - free -  (3.0K)
            40      1024    1  freebsd-boot  (512K)
          1064       984       - free -  (492K)
          2048   4194304    2  freebsd-zfs  (2.0G)
       4196352   8388608    3  freebsd-swap  (4.0G)
      12584960  29356032    4  freebsd-zfs  (14G)
      41940992  41945055       - free -  (20G)

接下来通过 `gpart resize` 来扩容：

    root@freebsd:~ # gpart resize -i 4 da0
    da0p4 resized
    root@freebsd:~ # gpart show da0
    =>      34  83886013  da0  GPT  (40G)
            34         6       - free -  (3.0K)
            40      1024    1  freebsd-boot  (512K)
          1064       984       - free -  (492K)
          2048   4194304    2  freebsd-zfs  (2.0G)
       4196352   8388608    3  freebsd-swap  (4.0G)
      12584960  71301087    4  freebsd-zfs  (34G)

可以看到家目录大小变成了 34G。然后依次替换其他三个硬盘，一定要注意要等数据 **resilvered** 完之后再换另一块硬盘。随时通过 `zpool status` 来查看状态。

前后两次存储池的对比。更新前：

    $ zpool list
    NAME       SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
    bootpool  1.98G   510M  1.49G         -    18%    25%  1.00x  DEGRADED  -
    zroot     55.5G  7.74G  47.8G         -     4%    13%  1.00x  DEGRADED  -

更新后：

    zroot@freebsd:~ # zpool list
    NAME       SIZE  ALLOC   FREE  EXPANDSZ   FRAG    CAP  DEDUP  HEALTH  ALTROOT
    bootpool  1.98G   511M  1.49G         -    18%    25%  1.00x  ONLINE  -
    zroot      136G  7.52G   128G         -     2%     5%  1.00x  ONLINE  -

前后两次 df 的输出对比，扩容前：

    root@freebsd:~ # df -h
    Filesystem            Size    Used   Avail Capacity  Mounted on
    zroot/ROOT/default     25G    2.7G     22G    11%    /
    devfs                 1.0K    1.0K      0B   100%    /dev
    bootpool              1.9G    509M    1.4G    26%    /bootpool
    zroot/tmp              22G     45M     22G     0%    /tmp
    zroot/usr/home         22G    186K     22G     0%    /usr/home
    zroot/usr/ports        23G    900M     22G     4%    /usr/ports
    zroot/usr/src          22G    140K     22G     0%    /usr/src
    zroot/var/audit        22G    140K     22G     0%    /var/audit
    zroot/var/crash        22G    140K     22G     0%    /var/crash
    zroot/var/log          22G    680K     22G     0%    /var/log
    zroot/var/mail         22G    192K     22G     0%    /var/mail
    zroot/var/tmp          22G    140K     22G     0%    /var/tmp
    zroot                  22G    140K     22G     0%    /zroot

扩容后：

    root@freebsd:~ # df -h
    Filesystem            Size    Used   Avail Capacity  Mounted on
    zroot/ROOT/default     63G    2.7G     60G     4%    /
    devfs                 1.0K    1.0K      0B   100%    /dev
    bootpool              1.9G    509M    1.4G    26%    /bootpool
    zroot/tmp              60G     45M     60G     0%    /tmp
    zroot/usr/home         60G    186K     60G     0%    /usr/home
    zroot/usr/ports        61G    900M     60G     1%    /usr/ports
    zroot/usr/src          60G    140K     60G     0%    /usr/src
    zroot/var/audit        60G    140K     60G     0%    /var/audit
    zroot/var/crash        60G    140K     60G     0%    /var/crash
    zroot/var/log          60G    680K     60G     0%    /var/log
    zroot/var/mail         60G    192K     60G     0%    /var/mail
    zroot/var/tmp          60G    140K     60G     0%    /var/tmp
    zroot                  60G    140K     60G     0%    /zroot

还没有机会在物理机上实验，记录基本的方法和过程如上，首次做这样的操作，可能会有错误存在，请慎重。**涉及到硬盘分区操作的命令请慎重使用。**

**除非知道命令的真实效果，否则不要随便敲回车。**

Update：

- 2/20/2016 初稿