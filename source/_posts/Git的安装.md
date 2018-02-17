---
title: Git的安装
date: 2014-12-11 13:02:45
tags:
---

Git的安装还是很简单的，曾经被学长三番五次的推荐说让我抛弃Windows，转入Linux的怀抱。因为Linux的性能相比于Windows实在是好太多，Windows臃肿的内核实在是让程序执行效率越来越差。这一段时间逐渐开始熟悉Linux环境，这学期也开了Linux的相关课程，逐步的去适应Linux的命令行环境。

电脑懒得重启，就直接在电脑上安装了一个Git Bash，目的其实也就是为了模拟Linux的环境。msysgit是windows版的Git，可以从[http://msysgit.github.io/上面下载。直接安装就行了。](http://msysgit.github.io/%E4%B8%8A%E9%9D%A2%E4%B8%8B%E8%BD%BD%E3%80%82%E7%9B%B4%E6%8E%A5%E5%AE%89%E8%A3%85%E5%B0%B1%E8%A1%8C%E4%BA%86%E3%80%82)

对于Linux版的，应该也是一样，直接sudo apt-get install git应该也可以，不过我还木有尝试。改天将自己的开发环境完全转移到Linux。

当git安装完[![QQ截图20141119215200](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141119215200.png)](http://wwdream-wordpress.stor.sinaapp.com/uploads/2014/12/QQ%E6%88%AA%E5%9B%BE20141119215200.png)成之后，还是需要对git进行配置。需要对git进行配置global，也就是全局的用户名和邮箱。

 

```
$ git config –global user.name “Your Name”
$ git config –global user.email “email@example.com”
```