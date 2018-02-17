---
title: Linux当中的用户和用户组
date: 2014-12-12 13:07:56
tags: linux
---

Linux对文件管理可能说是做的比较多了，对于用户来说，分为文件的所有者、组用户还有其他人。文件的所有者，顾名思义，就是所有文件的人，也就是创建或者拥有这个文件的人。对于组用户来说，一个用户可以隶属于一个或者多个用户组，文件可以针对于文件所隶属于的用户组设定相应的权限，其他人，也就顾名思义，是既不是用户本人，也不是用户所属的用户组里面的任何人。这里面要特别留意root用户可以访问任何内容

对于Linux当中的文件权限，也分为了RWX三种，分别也就是可读、可写、可执行的意思，我们先执行一下ls -al命令，对文件系统进行查看

```
 $ls -al
drwxrwxr-x  2 dream dream 4096 12月 12 20:06 .
drwxr-xr-x 43 dream dream 4096 12月 12 20:06 ..
-rwxrwxr-x  1 dream dream 9160 12月 12 20:00 2
-rw-rw-r–  1 dream dream   90 12月 12 20:00 2.cpp
-rw-rw-r–  1 dream dream 2648 12月 12 20:00 2.o
……………………………………………………………………
lrwxrwxrwx   1 root root       23 11月 29 00:51 vtrgb -> /etc/alternatives/vtrgb
-rw-r–r–   1 root root     4812  2月  8  2014 wgetrc
-rw-r–r–   1 root root     1343  1月 10  2007 wodim.conf
drwxr-xr-x   2 root root     4096 10月 23 03:10 wpa_supplicant
drwxr-xr-x  11 root root     4096 11月 28 18:48 X11
drwxr-xr-x   5 root root     4096 10月 23 03:14 xdg
drwxr-xr-x   3 root root     4096 12月 12 16:26 xml
drwxr-xr-x   2 xrdp xrdp     4096 12月  7 18:27 xrdp
drwxr-xr-x   2 root root     4096 10月 23 03:13 xul-ext
-rw-r–r–   1 root root      349  9月 11 22:18 zsh_command_not_found

```

我们通过 这些信息对对文件进行分析。

首先第一列代表的是文件类型以及文件权限，这一块我们下一步在进行介绍。

第二列代表文件的链接数，代表由多少各iNode结点链接到该文件上面

第三列表示文件所属的用户，第四列表示用户文件所属的用户组，第五列代表文件的修改日期，第六列表示文件名

第一列中第一个字符表示文件类型，其中

- 若是[d]则是目录

- 若是[-]则是文件

- 若是[l]则是链接文件

- 若是[b]表示设备文件里面可供存储的接口设备

- 若是[c]表示设备文件里面的穿行端口设备，例如鼠标、键盘
  然后接下来就是三组关于文件权限的描述。对于文件描述的都是rwx，分别代表可读、可写、可执行
  三组分别代表

- 表示文件的所有者

- 表示文件的用户组

- 表示其他人
  改变文件的属性和权限
  1.使用chgrp改变文件所属的组
  语法：

  ```
  chgrp +组名+文件名

  ```

  ​

  ```
  root@dream-Inspiron-5520:~# touch test
  root@dream-Inspiron-5520:~# ls -al test
  -rw-r–r– 1 root root 0 12月 12 20:51 test
  root@dream-Inspiron-5520:~# chgrp dream test
  root@dream-Inspiron-5520:~# ls -al test
  -rw-r–r– 1 root dream 0 12月 12 20:51 test

  ```

  ​

  2.chown：改变文件的所有者

  ​

  语法：

  ​

  ```
  chown+用户名+文件名

  ```

  ​

  ```
  root@dream-Inspiron-5520:~# touch test1
  root@dream-Inspiron-5520:~# ls -l test1
  -rw-r–r– 1 root root 0 12月 12 20:56 test1
  root@dream-Inspiron-5520:~# chown dream test1
  root@dream-Inspiron-5520:~# ls -l test1
  -rw-r–r– 1 dream root 0 12月 12 20:56 test1

  ```

  ​

  在使用cp命令的时候会默认复制文件的属性和权限，所以需要使用chgrp或者chown命令改变文件的所有者

  ​

  3.chmod

  ​

  这个命令是改变文件的权限时使用的，其中给rwx各分配了一个权值，其中r是4，w是2，x是1，通过权值可以计算出必要的权值。

  ​

  ```
  root@dream-Inspiron-5520:~# touch test2
  root@dream-Inspiron-5520:~# ls -l test2
  -rw-r–r– 1 root root 0 12月 12 21:00 test2
  root@dream-Inspiron-5520:~# chmod 775 test2
  root@dream-Inspiron-5520:~# ls -l test2
  -rwxrwxr-x 1 root root 0 12月 12 21:00 test2
  root@dream-Inspiron-5520:~#

  ```

  ​

  可以很容易发现，test2文件增加了可执行的权限

  ​

  其实，文件的权限也可以这么玩

  ​

  ```
  root@dream-Inspiron-5520:~# touch test3
  root@dream-Inspiron-5520:~# ls -l test3
  -rw-r–r– 1 root root 0 12月 12 21:03 test3
  root@dream-Inspiron-5520:~# chmod +x test3
  root@dream-Inspiron-5520:~# ls -l test3
  -rwxr-xr-x 1 root root 0 12月 12 21:03 test3
  root@dream-Inspiron-5520:~# chmod -r test3
  root@dream-Inspiron-5520:~# ls -l test3
  –wx–x–x 1 root root 0 12月 12 21:03 test3
  root@dream-Inspiron-5520:~# chmod u=rwx,g=rx,o=r test3
  root@dream-Inspiron-5520:~# ls -l test3
  -rwxr-xr– 1 root root 0 12月 12 21:03 test3

  ```

  ​

  下面来介绍一下文件中的各种权限的意义。顾名思义，rw指的是文件的可读可写，没有太多说得，x代表的是文件可以被执行，假如文件含有x属性，我们就可以用./filename来运行他啦。

  ​

  重点来看一看对文件夹的权限概念

  ​

  文件夹的r代表了可以对文件结构读出来，也就意味着我们可以通过ls命令读出文件夹当中的内容

  ​

  文件夹的w代表了文件夹可写，假设一个文件夹对某个用户来说是可以写入的，这里的写入代表创建或者修改文件，例如，一个文件的属性对该用户来说是不可写的，但是目录对该用户可写，用户还是可以直接对文件进行删除或者重命名操作

  ​

  文件夹的x代表了可以将一个目录设置为工作目录，例如我们可以利用cd命令进入一个文件夹并且将其设置为我们的工作目录。

  ​

  下面说一下几个目录的作用

  ​

  ```
  root@dream-Inspiron-5520:~# ls -l /
  总用量 104
  drwxr-xr-x   2 root root  4096 12月  8 11:21 bin
  drwxr-xr-x   4 root root  4096 12月  8 11:24 boot
  drwxrwxr-x   2 root root  4096 11月 29 00:54 cdrom
  drwxr-xr-x  16 root root  4300 12月 12 19:16 dev
  drwxr-xr-x 140 root root 12288 12月 12 19:56 etc
  drwxr-xr-x   3 root root  4096 11月 29 00:54 home
  lrwxrwxrwx   1 root root    33 12月  8 11:23 initrd.img -> boot/initrd.img-3.16.0-26-generic
  lrwxrwxrwx   1 root root    33 12月  6 22:21 initrd.img.old -> boot/initrd.img-3.16.0-25-generic
  drwxr-xr-x  24 root root  4096 12月 12 19:54 lib
  drwxr-xr-x   2 root root  4096 12月 12 19:54 lib32
  drwxr-xr-x   2 root root  4096 12月 12 11:53 lib64
  drwx——   2 root root 16384 11月 29 00:51 lost+found
  drwxr-xr-x   3 root root  4096 11月 29 01:00 media
  drwxr-xr-x   2 root root  4096 10月 16 08:42 mnt
  drwxr-xr-x   6 root root  4096 12月 12 12:04 opt
  dr-xr-xr-x 272 root root     0 12月 13  2014 proc
  drwx——   4 root root  4096 12月 12 21:03 root
  drwxr-xr-x  28 root root   880 12月 12 19:55 run
  drwxr-xr-x   2 root root 12288 12月 12 11:53 sbin
  drwxr-xr-x   2 root root  4096 10月 23 02:35 srv
  dr-xr-xr-x  13 root root     0 12月 13  2014 sys
  drwxrwxrwt  11 root root  4096 12月 12 20:52 tmp
  drwxr-xr-x   3 root root  4096 11月 28 19:58 u01
  drwxr-xr-x  11 root root  4096 12月 12 19:54 usr
  drwxr-xr-x  13 root root  4096 10月 23 03:20 var
  lrwxrwxrwx   1 root root    30 12月  8 11:23 vmlinuz -> boot/vmlinuz-3.16.0-26-generic
  lrwxrwxrwx   1 root root    30 12月  6 22:21 vmlinuz.old -> boot/vmlinuz-3.16.0-25-generic

  ```

  ​

  下面说一下几个目录的作用：

  ​

  ```
  /bin：放置很多可执行文件的目录，可以在单用户维护模式下还能够被使用
  /boot：放置开机会用到的文件，包括Linux内核以及开机所需的配置文件
  /dev：存放设备接口文件
  /etc：村范系统主要的配置文件，包括账号密码文件、各类服务的起始文件等
  /home：系统默认的主文件夹
  /lib：存放系统需要的函数库
  /media：存放各种可删除的设备
  /mnt：挂在某些额外的设备
  /opt：存放第三方软件的目录
  /root：root用户的主文件夹
  /sbin：只有root用户才能使用的命令一般放到这个目录
  /srv：web service 启动之后的根目录
  /tmp：放置系统的临时文件的目录
  /usr ：UNIX Software Resources ，
  /var：表示系统运行过程中逐渐变大的目录

  ```

  ​

  $PATH变量：

  ​

  ```
  dream@dream-Inspiron-5520:~$ echo $PATH
  /usr/local/jdk1.8.0_25/bin:/usr/local/jdk1.8.0_25/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games

  ```

  ​

  和windows的环境变量差不多，也就是搜索路径的意思，当Linux需要文件，会首先在当前目录搜索，然后在PATH目录下搜索。对PATH变量的修改也很简单，直接对变量进行赋值就可以了，不过要注意的是，PATH变量的修改只对当前shell有效

  ​

  ```
  dream@dream-Inspiron-5520:~$ echo $PATH
  /usr/local/jdk1.8.0_25/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
  dream@dream-Inspiron-5520:~$ bash
  dream@dream-Inspiron-5520:~$ PATH=$PATH:/root
  dream@dream-Inspiron-5520:~$ echo $PATH
  /usr/local/jdk1.8.0_25/bin:/usr/local/jdk1.8.0_25/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/root
  dream@dream-Inspiron-5520:~$ exit
  exit
  dream@dream-Inspiron-5520:~$ echo $PATH
  /usr/local/jdk1.8.0_25/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games

  ```

  ​

  umask:制定目前用户在新建文件或目录的时候权限默认值

  ​

  ```
  dream@dream-Inspiron-5520:~$ umask
  0002

  ```

  ​

  ```
  dream@dream-Inspiron-5520:~$ umask
  0002
  dream@dream-Inspiron-5520:~$ touch newfile
  dream@dream-Inspiron-5520:~$ ls -l newfile
  -rw-rw-r– 1 dream dream 0 12月 12 22:19 newfile
  dream@dream-Inspiron-5520:~$ umask 022
  dream@dream-Inspiron-5520:~$ touch newfile1
  -rw-rw-r– 1 dream dream 0 12月 12 22:19 newfile
  dream@dream-Inspiron-5520:~$ ls -l newfile1
  -rw-r–r– 1 dream dream 0 12月 12 22:19 newfile1
  dream@dream-Inspiron-5520:~$ umask
  0022

  ```

  ​

  从刚才的例子我们可以发现，用户新建文件的权限等于777-umask

  ​

  让用户能进入某目录成为“可工作目录”的基本权限是什么

  ​

- 可使用的命令：例如cd等切换工作目录的命令

- 目录所需权限：用户对这个目录至少需要x的权限

- 额外需求：如果用户想要在这个目录内利用ls查阅文件名，则用户对此目录还需要r的权限
  用户在某个目录读取一个文件的基本权限是什么：

- 可使用的命令：cat、more、less等

- 目录所需权限：用户对这个目录至少需要x权限

- 文件所需权限：用户对文件至少需要r的权限才行
  用户可以修改一个文件的基本权限是什么

- 可使用的命令：nano或者vi等

- 目录所需权限：用户在该文件的目录至少需要x权限

- 文件所需权限：用户对该文件至少需要r，w权限。
  一个用户可以创建一个文件的基本权限是什么

- 目录所需权限：用户在该目录药具有w，x权限

让用户进入某目录并执行该目录下的某个命令的基本权限是什么

- 目录所需权限：用户在该目录至少拥有x权限
- 文件所需权限：用户在该文件至少需要有x的权限