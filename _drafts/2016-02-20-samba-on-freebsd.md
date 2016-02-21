---
layout: post
title: "Samba on FreeBSD"
description: ""
category: "Linux/Unix"
tags: [FreeBSD,samba]
---
{% include JB/setup %}


    root@freebsd:~ # pkg search samba
    p5-Samba-LDAP-0.05_2           Manage a Samba PDC with an LDAP Backend
    p5-Samba-SIDhelper-0.0.0_3     Create SIDs based on G/UIDs
    samba-nsupdate-9.8.6_1         nsupdate utility with GSS-TSIG support
    samba-virusfilter-0.1.3_1      On-access anti-virus filter for Samba
    samba36-3.6.25_1               Free SMB and CIFS client and server for Unix
    samba36-libsmbclient-3.6.25_2  Shared lib from the samba package
    samba36-nmblookup-3.6.25       NetBIOS Name lookup tool
    samba36-smbclient-3.6.25       Samba "ftp-like" client
    samba4-4.0.26_3                Free SMB/CIFS and AD/DC server and client for Unix
    samba41-4.1.22                 Free SMB/CIFS and AD/DC server and client for Unix
    samba42-4.2.7                  Free SMB/CIFS and AD/DC server and client for Unix
    samba43-4.3.3                  Free SMB/CIFS and AD/DC server and client for Unix
    root@freebsd:~ # pkg install samba4
    Updating FreeBSD repository catalogue...
    FreeBSD repository is up-to-date.
    All repositories are up-to-date.
    New version of pkg detected; it needs to be installed first.
    The following 1 package(s) will be affected (of 0 checked):

    Installed packages to be UPGRADED:
            pkg: 1.6.1 -> 1.6.2

    The process will require 2 KiB more space.
    2 MiB to be downloaded.

    Proceed with this action? [y/N]: y
    Fetching pkg-1.6.2.txz: 100%    2 MiB  70.1kB/s    00:36
    Checking integrity... done (0 conflicting)
    [1/1] Upgrading pkg from 1.6.1 to 1.6.2...
    [1/1] Extracting pkg-1.6.2: 100%
    Message from pkg-1.6.2:
    If you are upgrading from the old package format, first run:

      # pkg2ng
    Updating FreeBSD repository catalogue...
    FreeBSD repository is up-to-date.
    All repositories are up-to-date.
    The following 6 package(s) will be affected (of 0 checked):

    New packages to be INSTALLED:
            samba4: 4.0.26_3
            cyrus-sasl: 2.1.26_12
            py27-dnspython: 1.12.0
            ldb: 1.1.24
            libinotify: 20150910
            gamin: 0.1.10_8

    The process will require 113 MiB more space.
    20 MiB to be downloaded.

    Proceed with this action? [y/N]: y
    Fetching samba4-4.0.26_3.txz: 100%   18 MiB  80.0kB/s    03:52
    pkg: http://pkg.FreeBSD.org/FreeBSD:10:amd64/quarterly/All/samba4-4.0.26_3.txz: Operation timed out
    root@freebsd:~ # pkg install samba4
    Updating FreeBSD repository catalogue...
    FreeBSD repository is up-to-date.
    All repositories are up-to-date.
    The following 6 package(s) will be affected (of 0 checked):

    New packages to be INSTALLED:
            samba4: 4.0.26_3
            cyrus-sasl: 2.1.26_12
            py27-dnspython: 1.12.0
            ldb: 1.1.24
            libinotify: 20150910
            gamin: 0.1.10_8

    The process will require 113 MiB more space.
    20 MiB to be downloaded.

    Proceed with this action? [y/N]: y
    Fetching samba4-4.0.26_3.txz: 100%    5 MiB 123.1kB/s    00:39
    pkg: http://pkg.FreeBSD.org/FreeBSD:10:amd64/quarterly/All/samba4-4.0.26_3.txz: Operation timed out
    root@freebsd:~ # pkg install samba4
    \Updating FreeBSD repository catalogue...
    FreeBSD repository is up-to-date.
    All repositories are up-to-date.
    The following 6 package(s) will be affected (of 0 checked):

    New packages to be INSTALLED:
            samba4: 4.0.26_3
            cyrus-sasl: 2.1.26_12
            py27-dnspython: 1.12.0
            ldb: 1.1.24
            libinotify: 20150910
            gamin: 0.1.10_8

    The process will require 113 MiB more space.
    20 MiB to be downloaded.

    Proceed with this action? [y/N]: y
    Please type 'Y[es]' or 'N[o]' to make selection

    Proceed with this action? [y/N]: y
    Fetching samba4-4.0.26_3.txz: 100%   19 MiB  73.8kB/s    04:33
    Fetching cyrus-sasl-2.1.26_12.txz: 100%  467 KiB 239.1kB/s    00:02
    Fetching py27-dnspython-1.12.0.txz: 100%  171 KiB 175.5kB/s    00:01
    Fetching ldb-1.1.24.txz: 100%  193 KiB  65.8kB/s    00:03
    Fetching libinotify-20150910.txz: 100%   17 KiB  17.4kB/s    00:01
    Fetching gamin-0.1.10_8.txz: 100%   49 KiB  50.3kB/s    00:01
    Checking integrity... done (1 conflicting)
    Checking integrity... done (0 conflicting)
    Conflicts with the existing packages have been found.
    One more solver iteration is needed to resolve them.
    The following 7 package(s) will be affected (of 0 checked):

    Installed packages to be REMOVED:
            samba36-3.6.25_1

    New packages to be INSTALLED:
            cyrus-sasl: 2.1.26_12
            py27-dnspython: 1.12.0
            ldb: 1.1.24
            libinotify: 20150910
            gamin: 0.1.10_8
            samba4: 4.0.26_3

    The process will require 2 MiB more space.

    Proceed with this action? [y/N]: y
    [1/7] Deinstalling samba36-3.6.25_1...
    [1/7] Deleting files for samba36-3.6.25_1: 100%
    [2/7] Installing cyrus-sasl-2.1.26_12...
    *** Added group `cyrus' (id 60)
    *** Added user `cyrus' (id 60)
    [2/7] Extracting cyrus-sasl-2.1.26_12: 100%
    [3/7] Installing py27-dnspython-1.12.0...
    [3/7] Extracting py27-dnspython-1.12.0: 100%
    [4/7] Installing ldb-1.1.24...
    [4/7] Extracting ldb-1.1.24: 100%
    [5/7] Installing libinotify-20150910...
    [5/7] Extracting libinotify-20150910: 100%
    [6/7] Installing gamin-0.1.10_8...
    [6/7] Extracting gamin-0.1.10_8: 100%
    [7/7] Installing samba4-4.0.26_3...
    [7/7] Extracting samba4-4.0.26_3: 100%
    Message from cyrus-sasl-2.1.26_12:
    You can use sasldb2 for authentication, to add users use:

            saslpasswd2 -c username

    If you want to enable SMTP AUTH with the system Sendmail, read
    Sendmail.README

    NOTE: This port has been compiled with a default pwcheck_method of
          auxprop.  If you want to authenticate your user by /etc/passwd,
          PAM or LDAP, install ports/security/cyrus-sasl2-saslauthd and
          set sasl_pwcheck_method to saslauthd after installing the
          Cyrus-IMAPd 2.X port.  You should also check the
          /usr/local/lib/sasl2/*.conf files for the correct
          pwcheck_method.
          If you want to use GSSAPI mechanism, install
          ports/security/cyrus-sasl2-gssapi.
          If you want to use LDAP auxprop plugin, install
          ports/security/cyrus-sasl2-ldapdb.
    Message from libinotify-20150910:
    ============================================================================

    Libinotify functionality on FreeBSD is missing support for

      - detecting a file being moved into or out of a directory within the
        same filesystem
      - certain modifications to a symbolic link (rather than the
        file it points to.)

    in addition to the known limitations on all platforms using kqueue(2)
    where various open and close notifications are unimplemented.

    This means the following regression tests will fail:

    Directory notifications:
       IN_MOVED_FROM
       IN_MOVED_TO

    Open/close notifications:
       IN_OPEN
       IN_CLOSE_NOWRITE
       IN_CLOSE_WRITE

    Symbolic Link notifications:
       IN_DONT_FOLLOW
       IN_ATTRIB
       IN_MOVE_SELF
       IN_DELETE_SELF

    Kernel patches to address the missing directory and symbolic link
    notifications are available from:

    https://github.com/dmatveev/libinotify-kqueue/tree/master/patches

    =============================================================================
    You might want to consider increasing the kern.maxfiles tunable if you plan
    to use this library for applications that need to monitor activity of a lot
    of files.

    If the default on your system is too low, add the following line to
    /boot/loader.conf, then reboot the system:

        kern.maxfiles="25000"
    =============================================================================
    Message from gamin-0.1.10_8:
    ===============================================================================

    Gamin will only provide realtime notification of changes for at most n files,
    where n is the minimum value between (kern.maxfiles * 0.7) and
    (kern.maxfilesperproc - 200). Beyond that limit, files will be polled.

    If you often open several large folders with Nautilus, you might want to
    increase the kern.maxfiles tunable (you do not need to set
    kern.maxfilesperproc, since it is computed at boot time from kern.maxfiles).

    For a typical desktop, add the following line to /boot/loader.conf, then
    reboot the system:

        kern.maxfiles="25000"

    The behavior of gamin can be controlled via the various gaminrc files.
    See http://www.gnome.org/~veillard/gamin/config.html on how to create
    these files.  In particular, if you find gam_server is taking up too much
    CPU time polling for changes, something like the following may help
    in one of the gaminrc files:

    # reduce polling frequency to once per 10 seconds
    # for UFS file systems in order to lower CPU load
    fsset ufs poll 10

    ===============================================================================
    Message from samba4-4.0.26_3:
    ===============================================================================

    How to start: http://wiki.samba.org/index.php/Samba4/HOWTO

    * Your configuration is: /usr/local/etc/smb4.conf

    * All the relevant databases are under: /var/db/samba4

    * All the logs are under: /var/log/samba4

    * Provisioning script is: /usr/local/bin/samba-tool

    %%NSUPDATE%%You will need to specify location of the 'nsupdate' command in the
    %%NSUPDATE%%smb4.conf file:
    %%NSUPDATE%%
    %%NSUPDATE%%      nsupdate command = /usr/local/bin/samba-nsupdate -g
    %%NSUPDATE%%
    For additional documentation check: http://wiki.samba.org/index.php/Samba4

    Bug reports should go to the: https://bugzilla.samba.org/

    ===============================================================================
