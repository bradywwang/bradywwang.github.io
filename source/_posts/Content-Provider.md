---
title: Content Provider
date: 2014-02-14 12:40:46
tags:
---

一、Content Provider基本概念
1.Content Provider提供为存储和获取苏局提供了统一的接口
2.使用ContentProvider可以在不同的应用程序之间共享数据
3.Android为常见的一些数据提供了ContentProvider（包括音频、视频、图片和通讯录等等）
二、数据模型
Contentprovider使用表的形式来组织数据
三、URI(统一资源标识符）
1.每一个ContentProvider都拥有一个公共的URI，这个URI用于表示这个ContentProvider所提供的数据
2.Android所提供的ContentProvider都存放在android.provider包当中
四、ContentProvider所提供的函数
1.query（）查询
2.insert（）：插入
3.update（）：更新
4.getType（）：得到数据类型
5.OnCreate（）：创建时的回调函数
五、实现ContentProvider的过程
1.定义一个CONTENT_URI常量
2.定义一个类，继承Contentprovider
3.实现query，inset，update，delete，getTyper和OnCreate方法
4.在AndroidManifest.xml当中进行声明