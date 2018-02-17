---
title: '1.6 View初步 '
date: 2014-02-14 12:52:38
tags:
---

一、主要内容

1. View的基本概念
2. 在Activity当中获取代表View的对象
3. 设置View的属性
4. **4. 为View设置监听器**
   二、什么是View：在Activity显示的所有控件都是用对象来表示的，这些类都是View类的子类

三、代表控件的对象

布局文件的xml文件生成相应的对象

使用findviewbyid得到对象

对象是由布局文件生成的

Findviewbyid返回类型：view类型

Orientation:设置为vertical：使控件纵向排列

四、监听器

监听器：监控控件的操作，控件和监听器之间是绑定关系

为控件绑定监听器

1） 获取代表控件的对象

2） 定义一个类，实现监听器接口

3） 生成监听器对象

4） 为控件绑定监听器对象

导入快捷键：Ctrl+shift+O