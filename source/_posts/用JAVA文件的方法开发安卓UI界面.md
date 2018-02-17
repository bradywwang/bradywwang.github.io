---
title: 用JAVA文件的方法开发安卓UI界面
date: 2014-02-14 12:38:02
tags:
---

UI界面的开发分为两种，一种是通过XML文件，对ui界面添加相应的控件，然后在java文件当中用findViewById方法找到该控件，然后进行相应的操作。另外一种就是通过编程式的代码，直接通过Java文件创建相应的layout类，然后向其中添加对应的控件。

一般来说，可以通过XML文件设置的控件布局通常可以通过java文件来完成，但是其各有利弊。通过xml文件来对控件布局进行定义相对比较简单，但是有一定的缺点，就是不太灵活，而通过java文件对控件布局进行定义相对来说比较灵活，但是却相对来说比较麻烦，而且并不直观，不太适合定义全部的用户界面。

用java文件的方式定义布局输出内容

```
public class CodeView extends Activity{
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        LinearLayout layout = new LinearLayout(this);
        super.setContentView(layout);
        layout.setOrientation(LinearLayout.VERTICAL);
        TextView view = new TextView(this);
        layout.addView(view);
        view.setText("Hello World");
    }
}
```

用xml方式定义布局输出内容：

activie_main.xml: