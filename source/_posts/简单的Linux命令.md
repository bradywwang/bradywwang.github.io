---
title: 简单的Linux命令
date: 2014-12-12 13:05:37
tags: linux
---

date：查看当前时间

```
$ date
2014年 12月 12日 星期五 19:24:22 CST

```

```
$ cal
      十二月 2014        
日 一 二 三 四 五 六  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30 31           

```

```
$ cal 2012
                            2012
         一月                    二月                    三月           
日 一 二 三 四 五 六  日 一 二 三 四 五 六  日 一 二 三 四 五 六  
 1  2  3  4  5  6  7            1  2  3  4               1  2  3  
 8  9 10 11 12 13 14   5  6  7  8  9 10 11   4  5  6  7  8  9 10  
15 16 17 18 19 20 21  12 13 14 15 16 17 18  11 12 13 14 15 16 17  
22 23 24 25 26 27 28  19 20 21 22 23 24 25  18 19 20 21 22 23 24  
29 30 31              26 27 28 29           25 26 27 28 29 30 31  

         四月                    五月                    六月           
日 一 二 三 四 五 六  日 一 二 三 四 五 六  日 一 二 三 四 五 六  
 1  2  3  4  5  6  7         1  2  3  4  5                  1  2  
 8  9 10 11 12 13 14   6  7  8  9 10 11 12   3  4  5  6  7  8  9  
15 16 17 18 19 20 21  13 14 15 16 17 18 19  10 11 12 13 14 15 16  
22 23 24 25 26 27 28  20 21 22 23 24 25 26  17 18 19 20 21 22 23  
29 30                 27 28 29 30 31        24 25 26 27 28 29 30  

         七月                    八月                    九月           
日 一 二 三 四 五 六  日 一 二 三 四 五 六  日 一 二 三 四 五 六  
 1  2  3  4  5  6  7            1  2  3  4                     1  
 8  9 10 11 12 13 14   5  6  7  8  9 10 11   2  3  4  5  6  7  8  
15 16 17 18 19 20 21  12 13 14 15 16 17 18   9 10 11 12 13 14 15  
22 23 24 25 26 27 28  19 20 21 22 23 24 25  16 17 18 19 20 21 22  
29 30 31              26 27 28 29 30 31     23 24 25 26 27 28 29  
                                            30                    

         十月                   十一月                   十二月           
日 一 二 三 四 五 六  日 一 二 三 四 五 六  日 一 二 三 四 五 六  
    1  2  3  4  5  6               1  2  3                     1  
 7  8  9 10 11 12 13   4  5  6  7  8  9 10   2  3  4  5  6  7  8  
14 15 16 17 18 19 20  11 12 13 14 15 16 17   9 10 11 12 13 14 15  
21 22 23 24 25 26 27  18 19 20 21 22 23 24  16 17 18 19 20 21 22  
28 29 30 31           25 26 27 28 29 30     23 24 25 26 27 28 29  
                                            30 31                

```

```
cal 6 2012
      六月 2012         
日 一 二 三 四 五 六  
                1  2  
 3  4  5  6  7  8  9  
10 11 12 13 14 15 16  
17 18 19 20 21 22 23  
24 25 26 27 28 29 30  

```

```
File: *manpages*,  Node: man,  Up: (dir)

MAN(1)                         手册分页显示工具                         MAN(1)

NAME
       man - 在线参考手册的接口

概
       man  [-C  file]  [-d]  [-D]  [--warnings[=warnings]]  [-R encoding] [-L
       locale] [-m system[,...]] [-M path] [-S list]  [-e  extension]  [-i|-I]
       [--regex|--wildcard]   [--names-only]  [-a]  [-u]  [--no-subpages]  [-P
       pager]   [-r   prompt]   [-7]    [-E    encoding]    [--no-hyphenation]
       [--no-justification]   [-p   string]  [-t]  [-T[device]]  [-H[browser]]
       [-X[dpi]] [-Z] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [-w|-W] [-S list] [-i|-I] [--regex] [section] term ...
       man -f [whatis options] page ...
       man -l [-C file] [-d] [-D] [--warnings[=warnings]]  [-R  encoding]  [-L
       locale]  [-P  pager]  [-r  prompt]  [-7] [-E encoding] [-p string] [-t]
       [-T[device]] [-H[browser]] [-X[dpi]] [-Z] file ...
-----Info：(*manpages*)man，1619 行 --Top------------------------------------
欢迎使用 Info 5.2 版。输入 h 以获得帮助，m 将得到菜单。

```

```
root@dream-Inspiron-5520:~# whatis time date
time (1)             - run programs and summarize system resource usage
time (2)             - get time in seconds
time (7)             - overview of time and timers
date (1)             - print or set the system date and time
root@dream-Inspiron-5520:~# man -f time date
time (1)             - run programs and summarize system resource usage
time (2)             - get time in seconds
time (7)             - overview of time and timers
date (1)             - print or set the system date and time

```

```
NAME
       shutdown - bring the system down

SYNOPSIS
       shutdown [OPTION]...  TIME [MESSAGE]
OPTIONS
       -r     Requests  that  the system be rebooted after it has been brought
              down.

       -h     Requests that the system be either halted or powered  off  after
              it has been brought down, with the choice as to which left up to
              the system.

       -H     Requests that the system be halted after  it  has  been  brought
              down.

       -P     Requests  that  the  system  be  powered  off  after it has been
              brought down.

       -c     Cancels a running shutdown.  TIME is  not  specified  with  this
              option, the first argument is MESSAGE.

       -k     Only  send  out  the warning messages and disable logins, do not
              actually bring the system down.

```

```
#shutdown -h now
立即关机，其中now相当于时间为0
#shutdown -h 20:25
在今天的20:25分会关机，若在21:25分之后执行该命令，则隔天才会关机
#shutdwn -h +10
在十分钟之后关机
#shutdown -r +30 'The system will reboot'
过30min系统重启，并且将后面的消息给所有在线的用户

```

```
cd：切换目录
pwd：显示当前目录
mkdir：新建一个空的目录
rmdir：删除一个空的目录

```

```
dream@dream-Inspiron-5520:~$ pwd
/home/dream

```

```
dream@dream-Inspiron-5520:~$ mkdir test
dream@dream-Inspiron-5520:~$ mkdir test/test1/test2
mkdir: 无法创建目录"test/test1/test2": 没有那个文件或目录
dream@dream-Inspiron-5520:~$ mkdir -p test/test1/test2

```

```
dream@dream-Inspiron-5520:~$ basename /etc/sysconfig/network
network
dream@dream-Inspiron-5520:~$ dirname /etc/sysconfig/network
/etc/sysconfig

```

```
Space：向后翻一页
/字符串：向下查询该字符串
:f：立刻显示出文件名以及当前的行数
messagebus:x:101:105::/var/run/dbus:/bin/false
uuidd:x:102:107::/run/uuidd:/bin/false
dnsmasq:x:103:65534:dnsmasq,,,:/var/lib/misc:/bin/false
“/etc/passwd”第 22 行
q:立刻离开more，不再显示该文件内容
b或者ctrl+b，表示向回翻页，对文件有用，对管道无用

```

```
Space：向下翻动一页
【PageDown】向下翻动一页
【pageUp】向上翻动一页
/字符串：向下查询“字符串”
?字符串：向上查询“字符串”
n：重复上一个查询
N：反向重复前一个查询
q：离开less

```

```
head -n 20 

```

```
dream@dream-Inspiron-5520:~$ cat -n /etc/passwd |head -n 10 
     1    root:x:0:0:root:/root:/bin/bash
     2    daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
     3    bin:x:2:2:bin:/bin:/usr/sbin/nologin
     4    sys:x:3:3:sys:/dev:/usr/sbin/nologin
     5    sync:x:4:65534:sync:/bin:/bin/sync
     6    games:x:5:60:games:/usr/games:/usr/sbin/nologin
     7    man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
     8    lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
     9    mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
    10    news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

```

```
tail -n 20 

```

```
dream@dream-Inspiron-5520:~$ nl /etc/passwd|head -n 30|tail -n 6
    25    kernoops:x:106:65534:Kernel Oops Tracking Daemon,,,:/:/bin/false
    26    rtkit:x:107:115:RealtimeKit,,,:/proc:/bin/false
    27    saned:x:108:116::/home/saned:/bin/false
    28    usbmux:x:109:46:usbmux daemon,,,:/var/lib/usbmux:/bin/false
    29    whoopsie:x:110:117::/nonexistent:/bin/false
    30    avahi:x:111:118:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false

```

```
dream@dream-Inspiron-5520:~$ od /etc/issue
0000000 061125 067165 072564 030440 027064 030061 056040 020156
0000020 066134 005012
0000024

```

```
root@dream-Inspiron-5520:~# touch test
root@dream-Inspiron-5520:~# chattr +i test 
root@dream-Inspiron-5520:~# rm test
rm: 无法删除"test": 不允许的操作
root@dream-Inspiron-5520:~# chattr -i test 
root@dream-Inspiron-5520:~# rm test

```

```
root@dream-Inspiron-5520:~# touch test
root@dream-Inspiron-5520:~# chattr +aij
Usage: chattr [-RVf] [-+=AaCcDdeijsSu] [-v version] files...
root@dream-Inspiron-5520:~# chattr +aij test 
root@dream-Inspiron-5520:~# lsattr test 
----ia---j---e-- test

```

```
root@dream-Inspiron-5520:~# file /etc/passwd
/etc/passwd: ASCII text

```

```
root@dream-Inspiron-5520:~# which ifconfig 
/sbin/ifconfig

```

```
dream@dream-Inspiron-5520:~$ type dra
bash: type: dra: 未找到
dream@dream-Inspiron-5520:~$ type cd
cd 是 shell 内建
dream@dream-Inspiron-5520:~$ type date
date 是 /bin/date
dream@dream-Inspiron-5520:~$

```

```
root@dream-Inspiron-5520:~# whereis ifconfig
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz

```

```
root@dream-Inspiron-5520:~# locate passwd
/etc/passwd
/etc/passwd-
/etc/alternatives/vncpasswd
/etc/alternatives/vncpasswd.1.gz
/etc/cron.daily/passwd
/etc/init/passwd.conf
/etc/pam.d/chpasswd
/etc/pam.d/passwd
......

```

```
root@dream-Inspiron-5520:~# find /home -user dream
root@dream-Inspiron-5520:~# find /home -nouser
root@dream-Inspiron-5520:~# find / -name passwd
root@dream-Inspiron-5520:~# find /var -mtime+4
root@dream-Inspiron-5520:~# find / -type s
root@dream-Inspiron-5520:~# find / -size +1000k


```

```
dream@dream-Inspiron-5520:~$ uptime
 16:38:03 up  1:02,  4 users,  load average: 1.37, 1.14, 1.14

```

```
root@dream-Inspiron-5520:~# users
dream dream dream dream
root@dream-Inspiron-5520:~# who
dream    :0           2014-12-15 15:35 (:0)
dream    pts/0        2014-12-15 15:37 (:0)
dream    pts/8        2014-12-15 15:45 (:0)
dream    pts/18       2014-12-15 16:37 (:0)
root@dream-Inspiron-5520:~# w
 16:40:46 up  1:05,  4 users,  load average: 1.18, 1.24, 1.19
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
dream    :0       :0               15:35   ?xdm?   6:08   0.21s upstart --user
dream    pts/0    :0               15:37    1:03m  1.88s  1.80s python client.p
dream    pts/8    :0               15:45    3:26   0.23s  0.23s bash
dream    pts/18   :0               16:37    6.00s  0.11s  7.71s gnome-terminal


```

