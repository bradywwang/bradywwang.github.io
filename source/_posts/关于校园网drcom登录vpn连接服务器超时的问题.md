---
title: 关于校园网drcom登录vpn连接服务器超时的问题
date: 2015-03-11 13:15:49
tags:
---

这两天用亚马逊的aws申请了个vps主机，并且用该vps搭建了vpn服务器，个人感觉速度很给力，Facebook，YouTube没有卡顿，一秒钟缓冲50%~但是美中不足的就是校园网登录需要drcom认证，如果登录vpn会导致链接不上登录服务器，登陆不成功，五分钟左右就会掉线，网上最终找到的解决方案就是将内网地址设置例外即可，新建一个bat文件，复制以下内容（以jlu的认证服务器为例）

```
@echo off
for /F “tokens=3” %% in (‘route print ^| findstr “\<0.0.0.0\>”‘) do set “gw=%%“
ipconfig /flushdns
route add 10.0.0.0 mask 255.0.0.0 %gw% metric 25
pause
```
保存右键以管理员权限运行即可，上脸书推特无压力，校园内网又不影响