---
layout: post
title: ubuntu command lines
date: '2014-11-30 15:09:45'
---

 1. 递归式创建一些嵌套目录:  mkdir –p /tmp/xxs/dsd/efd
 2. vim 如何显示行号:  :set number
 3. 统计程序的内存耗用:  ps -eo fname,rss|awk '{arr[$1]+=$2} END {for (i in arr) {print i,arr[i]}}'|sort -k2 -nr
 4. 删除特殊文件名 --help.txt 的文件:  rm -- --help.txt 或 rm ./--help.txt
 5. 增加用户:  sudo adduser 用户名
 6. 增加系统最大打开文件个数:  ulimit -n 4096 或 echo 4096 > /proc/sys/fs/file-max
 7. PDF 文件乱码 :  sudo apt-get install xpdf-chinese-simplified xpdf-chinese-traditional poppler-data
 8. 查看当前所在目录的绝对路经:  pwd
 9. 强制中止一个进程:  kill -9 进程号 或 killall -9 进程名
 10. 批量将rmvb转为avi:  ``for i in *; do mencoder -oac mp3lame -lameopts vbr=3 -ovc xvid -xvidencopts fixed_quant=4 -of avi $i -o `echo $i | sed -e 's/rmvb$/avi/'`; done``
 11. 如何禁用某个帐户:  sudo usermod -L 用户名 或 sudo passwd -l 用户名
 12. 重新从服务器获得IP地址 :  sudo dhclient
 13. 查看CMOS时间 :  hwclock --show
 14. 