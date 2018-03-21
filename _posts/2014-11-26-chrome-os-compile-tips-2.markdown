---
layout: post
title: Chrome OS compile tips
date: '2014-11-26 06:51:58'
---

	(cr) ((973d34b...)) beta4better@demo2014 ~/trunk/src/scripts $ ./image_to_vm.sh --from=../build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1 --board=veyron_mighty
	~/trunk/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1 ~/trunk/src/scripts
	~/trunk/src/scripts
	Resizing stateful partition to 3072MB
	STATE: recovering journal
	STATE: 22323/65536 files (0.0% non-contiguous), 68750/262144 blocks
	resize2fs 1.42 (29-Nov-2011)
	Resizing the filesystem on /tmp/tmp.aTaRJrItX9/stateful to 786432 (4k) blocks.
	The filesystem on /tmp/tmp.aTaRJrItX9/stateful is now 786432 blocks long.

	1+0 records in
	1+0 records out
	512 bytes (512 B) copied, 0.000261448 s, 2.0 MB/s
	1+0 records in
	1+0 records out
	512 bytes (512 B) copied, 0.00017299 s, 3.0 MB/s
	WARNING: Primary GPT header is invalid
	WARNING: Secondary GPT header is invalid
	5AE78A59-2B4B-D04A-8F8F-1ADE7B9C1B47
	       start        size    part  contents
		   0           1          PMBR (Boot GUID: 5AE78A59-2B4B-D04A-8F8F-1ADE7B9C1B47)
		   1           1          Pri GPT header
		   2          32          Pri GPT table
	     8671232     6291456       1  Label: "STATE"
		                          Type: Linux data
		                          UUID: 9459D09F-2F68-E74F-883D-5B73892A7B75
	       20480       32768       2  Label: "KERN-A"
		                          Type: ChromeOS kernel
		                          UUID: 5297CA9A-1F68-8946-8474-1FC395C2B73B
		                          Attr: priority=15 tries=15 successful=0
	     4476928     4194304       3  Label: "ROOT-A"
		                          Type: ChromeOS rootfs
		                          UUID: 1B8A5730-8494-DE4C-83CF-1FFD7A4C2510
	       53248       32768       4  Label: "KERN-B"
		                          Type: ChromeOS kernel
		                          UUID: 814F9BD2-8659-0A4F-8CD7-B7A30BF38418
		                          Attr: priority=0 tries=0 successful=0
	      282624     4194304       5  Label: "ROOT-B"
		                          Type: ChromeOS rootfs
		                          UUID: C80AF41B-9F0B-7E41-A3D1-34FB416049CD
	       16448           1       6  Label: "KERN-C"
		                          Type: ChromeOS kernel
		                          UUID: 2168E3A5-0D97-F848-B7C6-FF3365604157
		                          Attr: priority=0 tries=0 successful=0
	       16449           1       7  Label: "ROOT-C"
		                          Type: ChromeOS rootfs
		                          UUID: A883F751-FF6A-A646-BFF5-7C31F3585C98
	       86016       32768       8  Label: "OEM"
		                          Type: Linux data
		                          UUID: 14839477-6D28-4140-97BC-70C7120C0057
	       16450           1       9  Label: "reserved"
		                          Type: ChromeOS reserved
		                          UUID: EED20EBC-6EC1-1E4C-8297-0DFCAAB01EE9
	       16451           1      10  Label: "reserved"
		                          Type: ChromeOS reserved
		                          UUID: D979C7D9-8F35-B145-9DD8-7AD72222E0A3
		  64       16384      11  Label: "RWFW"
		                          Type: ChromeOS firmware
		                          UUID: F768E2DE-0366-F449-81D9-11A54F4CD6D1
	      249856       32768      12  Label: "EFI-SYSTEM"
		                          Type: EFI System Partition
		                          UUID: 5AE78A59-2B4B-D04A-8F8F-1ADE7B9C1B47
	    14995359          32          Sec GPT table
	    14995391           1          Sec GPT header
	1+0 records in
	1+0 records out
	1 byte (1 B) copied, 0.0104469 s, 0.1 kB/s
	INFO    : Boot-time configuration for /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1: 
	INFO    :   --board=veyron_mighty
	INFO    :   --image_type=usb
	INFO    :   --arch="arm"
	INFO    :   --keys_dir="/usr/share/vboot/devkeys"
	INFO    :   --boot_args="noinitrd"
	INFO    :   --nocleanup_dirs
	INFO    :   --verity_algorithm=sha1
	INFO    :   --enable_serial=""
	INFO    :   --loglevel="7"
	INFO    :   
	INFO    :   
	1+0 records in
	1+0 records out
	1 byte (1 B) copied, 8.1381e-05 s, 12.3 kB/s
	Setting up symlinks for /usr/local for /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/stateful_dir/dev_image
	INFO    : Image specified by /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1 mounted at /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/rootfs_dir successfully.
	INFO    : DEBUG: use recovery keyblock
	INFO    : rootfs is 313344 blocks of 4096 bytes
	INFO    : Generating root fs hash tree (salt '96889d2abe19dc125cc84cd3586880d5d3cfae55bdd7a830ef88a13650c330fa').
	dm:dm bht[DEBUG] Setting block_count 313344
	dm:dm bht[DEBUG] Setting depth to 3.
	dm:dm bht[DEBUG] depth: 0 entries: 1
	dm:dm bht[DEBUG] depth: 1 entries: 20
	dm:dm bht[DEBUG] depth: 2 entries: 2448
	INFO    : device mapper configuration: dm="1 vroot none ro 1,0 2506752 verity payload=ROOT_DEV hashtree=HASH_DEV hashstart=2506752 alg=sha1 root_hexdigest=a052963c7504fd91126fa4f1a3c116a8e706ab5d salt=96889d2abe19dc125cc84cd3586880d5d3cfae55bdd7a830ef88a13650c330fa"
	INFO    : Emitted cross-platform boot params to /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/boot.config
	1+0 records in
	1+0 records out
	512 bytes (512 B) copied, 0.000288379 s, 1.8 MB/s
	Key block:
	  Size:                0xcb8
	  Flags:               11  !DEV DEV REC
	  Data key algorithm:  11 RSA8192 SHA512
	  Data key version:    1
	  Data key sha1sum:    e78ce746a037837155388a1096212ded04fb86eb
	Preamble:
	  Size:                0xf348
	  Header version:      2.0
	  Kernel version:      1
	  Body load address:   0x100000
	  Body size:           0x3ea000
	  Bootloader address:  0x4e9000
	  Bootloader size:     0x1000
	Body verification succeeded.
	INFO    : Kernel partition image emitted: /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/vmlinuz.image
	INFO    : Root filesystem hash emitted: /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/rootfs.hash
	INFO    : rootfs is 313344 blocks of 4096 bytes
	INFO    : Generating root fs hash tree (salt '96889d2abe19dc125cc84cd3586880d5d3cfae55bdd7a830ef88a13650c330fa').
	dm:dm bht[DEBUG] Setting block_count 313344
	dm:dm bht[DEBUG] Setting depth to 3.
	dm:dm bht[DEBUG] depth: 0 entries: 1
	dm:dm bht[DEBUG] depth: 1 entries: 20
	dm:dm bht[DEBUG] depth: 2 entries: 2448
	INFO    : device mapper configuration: dm="1 vroot none ro 1,0 2506752 verity payload=ROOT_DEV hashtree=HASH_DEV hashstart=2506752 alg=sha1 root_hexdigest=a052963c7504fd91126fa4f1a3c116a8e706ab5d salt=96889d2abe19dc125cc84cd3586880d5d3cfae55bdd7a830ef88a13650c330fa"
	INFO    : Emitted cross-platform boot params to /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/boot.config
	1+0 records in
	1+0 records out
	512 bytes (512 B) copied, 0.00021673 s, 2.4 MB/s
	Key block:
	  Size:                0x4b8
	  Flags:               7  !DEV DEV !REC
	  Data key algorithm:  4 RSA2048 SHA256
	  Data key version:    1
	  Data key sha1sum:    d6170aa480136f1f29cf339a5ab1b960585fa444
	Preamble:
	  Size:                0xfb48
	  Header version:      2.0
	  Kernel version:      1
	  Body load address:   0x100000
	  Body size:           0x3ea000
	  Bootloader address:  0x4e9000
	  Bootloader size:     0x1000
	Body verification succeeded.
	1+0 records in
	1+0 records out
	65536 bytes (66 kB) copied, 0.000260453 s, 252 MB/s
	INFO    : Kernel partition image emitted: /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/hd_vmlinuz.image
	INFO    : Root filesystem hash emitted: /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/rootfs.hash
	INFO    : Kernel image A   size is 4169728 bytes.
	INFO    : Kernel image B   size is 4169728 bytes.
	INFO    : Kernel partition A size is 16777216 bytes.
	INFO    : Kernel partition B size is 16777216 bytes.
	INFO    : Appending rootfs.hash (10113024 bytes) to the root fs
	INFO    : Unmounting image from /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/stateful_dir and /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/rootfs_dir
	Cleaning up /usr/local symlinks for /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/stateful_dir/dev_image
	WARNING : umount failed, but devices were unmounted anyway
	WARNING : umount failed, but devices were unmounted anyway
	Creating final image
	Created image at /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1
	If you have qemu-kvm installed, you can start the image by:
	sudo kvm -m 1024 -vga cirrus -pidfile /tmp/kvm.pid -net nic,model=virtio -net user,hostfwd=tcp::9222-:22 \
	-hda /mnt/host/source/src/build/images/veyron_mighty/R41-6513.0.2014_11_26_1334-a1/chromiumos_qemu_image.bin