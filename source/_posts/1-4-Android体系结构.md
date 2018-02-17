---
title: '1.4 Android体系结构 '
date: 2014-02-14 12:51:05
tags:
---

1.Android应用程序开发技术结构图

2.基于组件的应用程序开发

3.Android应用程序组件

 

[![计算机生成了可选文字:A，一‘.CAt.ON.、瓜于司君葫](https://note.wiz.cn/unzip/93596179-3a13-4d31-bbed-edb32bd00927/e0dccb8a-b953-4bbb-a507-df2fe988745c.18/index_files/8bbe4750-1267-436b-9f93-a8a72263d917.jpg)](https://note.wiz.cn/unzip/93596179-3a13-4d31-bbed-edb32bd00927/e0dccb8a-b953-4bbb-a507-df2fe988745c.18/index_files/8bbe4750-1267-436b-9f93-a8a72263d917.jpg)

最下方：Linux Kernel：Linux核心，针对手机进行专门优化，电源管理、进程调度（驱动程序），提供了操作系统所需要的最基本功能

Libraies：常见的类库，运行在linux核心之上，提供手机基本功能

Android runtime（针对于Android定制的虚拟机和sdk）：core livraies：核心包，类似于jdk中提供的核心包

Dalvik Virtual Machine:虚拟机，针对于android特别优化

Application Framework：基于别人搭好的架子填上代码，降低开发难度，坚固代码质量

Applications：用户编写的应用程序

学习重点：application framework

宏观把握android体系结构

应用程序组件进行组装（还没有实现）

Activity：界面，应用程序的门户，负责和用户进行交互

应用程序-网站（很多个）

Activity——网页（三四个，四五个）

Service：主要负责在Android耗时较长的一些工作，没有图形化界面，在后台工作

Content Provider:内容提供者，像其他应用程序暴露应用程序所包含数据

BroadcastReceiver:广播接收器，监听系统行为，接通系统发出广播（低电量，蓝牙关闭。。。。）