---
title: findViewById中返回值为null的几种情况
date: 2015-07-13 13:19:21
tags:
---

这两天遇到了调用findviewById返回值为null的情况，始终没有解决怎么回事，网上查询之后最终找到了解决方案

1.在一个View中访问另一个View中的控件返回值一定为空，哪怕是Fregment和View的关系也不行。

2.findViewById的调用一定在setContentView之前，如果在setContentView之后，返回值也会为空

3.可能是IDE的问题，需要将工程clean重新生成一下就OK