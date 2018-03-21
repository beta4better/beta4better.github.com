---
layout: post
title: ZFS for Fedora 23
date: '2015-12-20 03:49:22'
tags:
- zfs
- fedora
---

````$ sudo dnf remove zfs-fuse
Dependencies resolved.
=========================================================================================================
 Package                 Arch                  Version                      Repository              Size
=========================================================================================================
Removing:
 zfs-fuse                x86_64                0.7.0-21.fc23                @fedora                4.2 M

Transaction Summary
=========================================================================================================
Remove  1 Package

Installed size: 4.2 M
Is this ok [y/N]: y
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Erasing     : zfs-fuse-0.7.0-21.fc23.x86_64                                                        1/1 
Removing files since we removed the last package
  Verifying   : zfs-fuse-0.7.0-21.fc23.x86_64                                                        1/1 

Removed:
  zfs-fuse.x86_64 0.7.0-21.fc23                                                                          

Complete!
[beta4better@localhost Downloads]$ sudo dnf install kernel-devel zfs 
Last metadata expiration check performed 0:02:06 ago on Sun Dec 20 11:38:40 2015.
Dependencies resolved.
=========================================================================================================
 Package                Arch             Version                                 Repository         Size
=========================================================================================================
Installing:
 dkms                   noarch           2.2.0.3-31.git.7c3e7c5.fc23             fedora             81 k
 kernel-devel           x86_64           4.2.7-300.fc23                          updates           9.8 M
 libnvpair1             x86_64           0.6.5.3-1.fc23                          zfs                33 k
 libuutil1              x86_64           0.6.5.3-1.fc23                          zfs                37 k
 libzfs2                x86_64           0.6.5.3-1.fc23                          zfs               119 k
 libzpool2              x86_64           0.6.5.3-1.fc23                          zfs               413 k
 spl                    x86_64           0.6.5.3-1.fc23                          zfs                31 k
 spl-dkms               noarch           0.6.5.3-1.fc23                          zfs               445 k
 zfs                    x86_64           0.6.5.3-1.fc23                          zfs               342 k
 zfs-dkms               noarch           0.6.5.3-1.fc23                          zfs               1.9 M

Transaction Summary
=========================================================================================================
Install  10 Packages

Total download size: 13 M
Installed size: 53 M
Is this ok [y/N]: y
Downloading Packages:
(1/10): libnvpair1-0.6.5.3-1.fc23.x86_64.rpm                              16 kB/s |  33 kB     00:02    
(2/10): libuutil1-0.6.5.3-1.fc23.x86_64.rpm                               25 kB/s |  37 kB     00:01    
(3/10): libzfs2-0.6.5.3-1.fc23.x86_64.rpm                                 31 kB/s | 119 kB     00:03    
(4/10): libzpool2-0.6.5.3-1.fc23.x86_64.rpm                               49 kB/s | 413 kB     00:08    
(5/10): spl-0.6.5.3-1.fc23.x86_64.rpm                                     20 kB/s |  31 kB     00:01    
(6/10): zfs-0.6.5.3-1.fc23.x86_64.rpm                                     19 kB/s | 342 kB     00:18    
(7/10): spl-dkms-0.6.5.3-1.fc23.noarch.rpm                                55 kB/s | 445 kB     00:08    
(8/10): dkms-2.2.0.3-31.git.7c3e7c5.fc23.noarch.rpm                       23 kB/s |  81 kB     00:03    
(9/10): zfs-dkms-0.6.5.3-1.fc23.noarch.rpm                                66 kB/s | 1.9 MB     00:29    
(10/10): kernel-devel-4.2.7-300.fc23.x86_64.rpm                          172 kB/s | 9.8 MB     00:58    
---------------------------------------------------------------------------------------------------------
Total                                                                    210 kB/s |  13 MB     01:04     
warning: /var/cache/dnf/zfs-d5f68c354cda2b42/packages/zfs-0.6.5.3-1.fc23.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID f14ab620: NOKEY
Importing GPG key 0xF14AB620:
 Userid     : "ZFS on Linux <zfs@zfsonlinux.org>"
 Fingerprint: C93A FFFD 9F3F 7B03 C310 CEB6 A9D5 A1C0 F14A B620
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux
Is this ok [y/N]: y
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Installing  : libuutil1-0.6.5.3-1.fc23.x86_64                                                     1/10 
  Installing  : libnvpair1-0.6.5.3-1.fc23.x86_64                                                    2/10 
  Installing  : kernel-devel-4.2.7-300.fc23.x86_64                                                  3/10 
  Installing  : dkms-2.2.0.3-31.git.7c3e7c5.fc23.noarch                                             4/10 
  Installing  : spl-dkms-0.6.5.3-1.fc23.noarch                                                      5/10 
Loading new spl-0.6.5.3 DKMS files...
Building for 4.2.6-301.fc23.x86_64
Module build for kernel 4.2.6-301.fc23.x86_64 was skipped since the
kernel source for this kernel does not seem to be installed.
  Installing  : libzpool2-0.6.5.3-1.fc23.x86_64                                                     6/10 
  Installing  : libzfs2-0.6.5.3-1.fc23.x86_64                                                       7/10 
  Installing  : spl-0.6.5.3-1.fc23.x86_64                                                           8/10 
  Installing  : zfs-dkms-0.6.5.3-1.fc23.noarch                                                      9/10 
Loading new zfs-0.6.5.3 DKMS files...
Building for 4.2.6-301.fc23.x86_64
Module build for kernel 4.2.6-301.fc23.x86_64 was skipped since the
kernel source for this kernel does not seem to be installed.
  Installing  : zfs-0.6.5.3-1.fc23.x86_64                                                          10/10 
  Verifying   : kernel-devel-4.2.7-300.fc23.x86_64                                                  1/10 
  Verifying   : zfs-0.6.5.3-1.fc23.x86_64                                                           2/10 
  Verifying   : libnvpair1-0.6.5.3-1.fc23.x86_64                                                    3/10 
  Verifying   : libuutil1-0.6.5.3-1.fc23.x86_64                                                     4/10 
  Verifying   : libzfs2-0.6.5.3-1.fc23.x86_64                                                       5/10 
  Verifying   : libzpool2-0.6.5.3-1.fc23.x86_64                                                     6/10 
  Verifying   : spl-0.6.5.3-1.fc23.x86_64                                                           7/10 
  Verifying   : zfs-dkms-0.6.5.3-1.fc23.noarch                                                      8/10 
  Verifying   : spl-dkms-0.6.5.3-1.fc23.noarch                                                      9/10 
  Verifying   : dkms-2.2.0.3-31.git.7c3e7c5.fc23.noarch                                            10/10 

Installed:
  dkms.noarch 2.2.0.3-31.git.7c3e7c5.fc23               kernel-devel.x86_64 4.2.7-300.fc23              
  libnvpair1.x86_64 0.6.5.3-1.fc23                      libuutil1.x86_64 0.6.5.3-1.fc23                 
  libzfs2.x86_64 0.6.5.3-1.fc23                         libzpool2.x86_64 0.6.5.3-1.fc23                 
  spl.x86_64 0.6.5.3-1.fc23                             spl-dkms.noarch 0.6.5.3-1.fc23                  
  zfs.x86_64 0.6.5.3-1.fc23                             zfs-dkms.noarch 0.6.5.3-1.fc23                  

Complete!
````
