---
title: 关于MyEclipse中Swing控件出现中文乱码的问题
date: 2014-12-17 13:14:35
tags:
---

这两天做Oracle课程设计，也开始逐渐接触到了GUI的编程，我在这里使用的是MyEclipse中自带的Swt Designer，Swt Designer入手很简单，直接进行拖拽就可以了。很快就设计好了一个界面，不过也遇到了一个问题，运行当中 JLabel中的英文显示正常，但是中文则显示为方框。如图。
[![QQ截图20141217115005](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217115005.png)](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217115005.png)

 

百度之后发现这个是因为中文编码的问题，需要在MyEclipse当中进行配置才可以。

具体的话参照了这个博客，并且得到了一些想法，具体原因可能就是MyEclipse自带的编译器的原因，需要进行配置解码器

<http://blog.sina.com.cn/s/blog_025270e90101b1db.html>

首先打开Run Configuration，选择Arguments选项，在VM Arguments选项中添加-Dfile.encoding=GB18030设置编码器即可正常，如图。[![QQ截图20141217120446](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217120446.png)](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217120446.png)

最终的结果就是这样，大功告成

[![QQ截图20141217120711](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217120711-300x173.png)](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141217120711-300x173.png)