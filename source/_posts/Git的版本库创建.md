---
title: Git的版本库创建
date: 2014-12-11 13:03:29
tags:
---

版本库也就是仓库，也就是GitHub中的repositort，可以理解成为一个可以被Git管理的目录，Git可以跟踪得到每一个文件的修改、删除，可以追踪历史，或者将来进行还原

首先建立一个空的版本库

```
$ mkdir gittest
$ cd gittest
$ pwd

```

新建一个目录，输出结果为

```
/c/Users/dream/gittest
```

其中pwd是用来显示当前目录

然后需要利用Gitinit把gittest这个文件夹变成空的git仓库

```
$ git init
Initialized empty Git repository in c:/Users/dream/gittest/.git/

```

Git只能跟踪到文本文档的改动，无法跟踪得到二进制文档的改动，比如说是对于图片甚至是word文档的改动，因为存储的是二进制信息，所以Git只能跟踪得到字节的变化，如果使用版本控制系统，就需要用纯文本方式对文件进行编辑。

Note：不要用Windows的notebook对文件进行编辑，因为notebook在保存的时候在每个文件开头加入了0xefbbbf的字符，可能会导致程序编译错误等问题

这里我使用的是UltraEdit，首先在我所建立的gittest文件夹中建立了一个1.txt文件，在里面写入了

```
hello world
this is the test file

```

然后执行

```
$ git add 1.txt
```

表示已经将1.txt建立了索引，添加成功

之后使用git commit将文件提交到仓库

```
$ git commit -m “add a new file”
[master (root-commit) d091d3b] add a new file
 1 file changed, 2 insertions(+)
 create mode 100644 1.txt

```

git commit表示将文件提交到远程仓库，-m后面输入的是提交内容，1 files changed表示改动了一个文件

对于文件的提交，我们先需要执行git add添加到目录，然后使用commit提交

```
$ git add file1.txt
$ git add file2.txt
$ git add file3.txt
$ git commit -m “add 3 files.”

```

———————————这里是华丽丽的分割线—————————

1.使用git init初始化git仓库

2.使用git add 

将文件进行添加
3.使用git commit -m “descriptions”向仓库进行提交