---
title: 一些基础的JAVA面试题总结
date: 2015-06-19 13:18:24
tags:
---

List,Set继承了Collection接口，而Map是一个单独的接口；

List的子类有ArrayList、LinedList和Vector：LinedList和Vector的底层都是基于链表，而ArrayList的底层是基于线性表。LinedList和ArrayList的共同点是线程是不安全的，不同点是ArrayList在做增删元素的时候，效率高，查询效率低；linedList恰好相反；这和它们的底层有关系。

Set的实现类HashSet,TreeSet。这俩个类都保存了元素的唯一性，但是hashSet的元素是无需的，而TreeSet的元素是有序的。

Map的实现类：HashMap,HashTable它们的区别是HashMap的key可以为null，而HashMap的key不能为Null;

当往Map集合中放入相同的key时，前者的key会覆盖后者的key。