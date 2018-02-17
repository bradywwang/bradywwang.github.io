---
title: '1.5 Activity初步 '
date: 2014-02-14 12:48:41
tags:
---

一、主要内容

1.Activity启动流程

2.Activity与布局文件之间的关系

3.在Activity当中获取代表控件对象

二、Activity启动基本流程

 

MainActivity

Android操作系统

AndroidManifes.xml

（主配置文件）

Activity_main.xml

onCreate（）



R.layout.activity_main:显示布局文件的内容

回顾：

1. activity启动流程：首先访问mainifes文件，了解默认activity是哪个，生成activity对象，调用activity的oncreate方法，在oncreate中调用setcontentview方法，在setcontentview方法中接受布局文件id，通过布局文件决定在activity显示内容

2. 布局文件与activity的关系：布局文件指示activity显示内容

3. 代表控件的对象：每一个控件在activity中有一个与之对应的对象


```
package com.dream.s01e05activity;
import android.os.Bundle;
import android.app.Activity;
import android.view.Menu;

public class MainActivity extends Activity {
	@Override
	protected void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.activity_main);
	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
	    // Inflate the menu; this adds items to the action bar if it is present.
	    getMenuInflater().inflate(R.menu.main, menu);
	    return true;
	}
}
```