---
title: '通过URL对象下载文件 '
date: 2014-02-14 12:41:50
tags:
---

1.创建一个URL对象
2.通过URL对象，创建一个HttpURLConnection对象

```
URL url=new URL(“url”)
HttpURLConnection urlConn = (HttpURLConnection)url.connection();

```

访问网络权限：android:permission.INTERNET

访问SDCard：

1.得到当前设备SD卡的目录

Environment.getEXtraStorageDireCtory（）

2.访问SD卡的权限：

android.permisson.WRITE_EXTERNAL_STORAGE