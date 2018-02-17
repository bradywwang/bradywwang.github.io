---
title: Git的版本控制
date: 2014-12-11 13:04:31
tags:
---

在我的前一篇博客中我已经添加了1.txt这个文件，现在我要对该文件进行简单的修改，来看一下会发生什么样的变化。
我们将1.txt修改为

```
hello git
this is the test file

```

在git bash中运行一下git status命令，查看运行结果

```
$ git status
On branch master
Changes not staged for commit:
  (use “git add …” to update what will be committed)
  (use “git checkout – …” to discard changes in working directory)
```

```
modified:   1.txt

```

Untracked files:
(use “git add …” to include in what will be committed)

```
1.txt.bak

```

no changes added to commit (use “git add” and/or “git commit -a”)
由于我使用的是UltraEdit，对文件进行修改的过程中新生成了1.txt.bak这个文件，所以显示了有一个文件被修改，新增了一个文件。
如果想要查看该文件发生了怎样的改变可以使用git diff命令进行查看

```
$ git diff 1.txt
diff –git a/1.txt b/1.txt
index 773e70b..c82dfa7 100644
— a/1.txt
+++ b/1.txt
@@ -1,2 +1,2 @@
-<U+FEFF>hello world
+<U+FEFF>hello git
 this is the test file

```

从git diff的输出结果可以看到，我们通过git diff这个命令来对不同版本之间的改变进行查看。对文件修改之后同样需要使用git add命令对文件进行提交，即

```
$ git add  1.txt

```

使用一下git diff查看一下效果

```
$ git status
On branch master
Changes to be committed:
  (use “git reset HEAD …” to unstage)
```

```
modified:   1.txt

```

Untracked files:
(use “git add …” to include in what will be committed)

```
1.txt.bak

```

git add之后，我们就可以放心的进行提交了，执行git commit命令即可

```
$ git commit -m “change the file”
[master 7b57303] change the file
 1 file changed, 1 insertion(+), 1 deletion(-)

```

然后使用一下git status查看一下仓库的状态：

```
$ git status
On branch master
Untracked files:
  (use “git add …” to include in what will be committed)
```

```
1.txt.bak

```

nothing added to commit but untracked files present (use “git add” to track)
可以发现我们的1.txt已经被成功的提交了
如果所有文件都被提交，我们运行git status 会显示：

```
$ git status
On branch master
nothing to commit, working directory clean

```

对于git的版本回退，我们也可以做一个练习。

还是我们的1.txt文件吧。将文件修改为

```
hello git
Git is free software distributed under the GPL.

```

这一次，为了方便起见，我们可以删除UltraEdit自动生成的1.txt.bak文件，

然后执行

```
$ git add 1.txt
$ git commit -m “add the GPL”
[master b0588af] add the GPL
 1 file changed, 1 insertion(+), 1 deletion(-)

```

我们可以不断地对文件进行修改，并且将其保存到版本库当中。在每一次保存的过程中，会自动生成一个叫做Commit的快照，一旦改乱了或者删除了文件，可以从最近的一个commit进行恢复。

我们可以使用git log查看一下对仓库的修改情况

```
$ git log
commit b0588af04fee20769c5245c0fd1e45865a69c00b
Author: dream.wang <dreamsme@foxmail.com>
Date:   Thu Dec 11 14:54:50 2014 +0800
```

```
add the GPL

```

commit 7b573033d62a217de669b6d678d4d88e923abfa3
Author: dream.wang <dreamsme@foxmail.com>
Date: Thu Dec 11 14:48:36 2014 +0800

```
change the file

```

commit d091d3b560f2545721748b09a526a6f4d98ed84c
Author: dream.wang <dreamsme@foxmail.com>
Date: Thu Dec 11 14:20:41 2014 +0800

```
add a new file

```

如果嫌输出信息太复杂，也可以通过git log –pretty=oneline命令进行查看

```
$ git log –pretty=oneline
b0588af04fee20769c5245c0fd1e45865a69c00b add the GPL
7b573033d62a217de669b6d678d4d88e923abfa3 change the file
d091d3b560f2545721748b09a526a6f4d98ed84c add a new file

```

我们可以查看每一次提交的commit编号以及commit信息

在Git中，HEAD表示当前版本，上一个版本就是HEAD^，上上个版本就是HEAD^^，当然网上一百个版本就是后面跟上100个^，可以直接写成HEAD~100

我们现在的目的就是想把当前版本进行回退

使用git reset命令

```
$ git reset –hard HEAD^
HEAD is now at 7b57303 change the file

```

可以查看一下文件内容

```
hello git
this is the test file

```

我们很容易就可以发现文件已经被改变了

我们可以利用git log 看一下日志的改变

```
$ git log commit 7b573033d62a217de669b6d678d4d88e923abfa3 Author: dream.wang &lt;dreamsme@foxmail.com&gt; Date: Thu Dec 11 14:48:36 2014 +0800
```

change the file

commit d091d3b560f2545721748b09a526a6f4d98ed84c
Author: dream.wang <dreamsme@foxmail.com>
Date: Thu Dec 11 14:20:41 2014 +0800

add a new file

我们可以发现，最后面的一条已经消失了，如果我们还记得那一条的commit id，就可以直接使用git reset –hard **\**（只用写前几位就行了），然后Git找到对应的commit id

```
$ git reset –hard b0588
HEAD is now at b0588af add the GPL

```

这样就可以了。

git进行版本回退的原理可以理解为C语言之间的指针，通过改变当前HEAD指针的指向来确定当前版本。如果忘记了已经回退过得commit版本号我们可以使用git reflog进行查看

```
$ git reflog
b0588af HEAD@{0}: reset: moving to b0588
7b57303 HEAD@{1}: reset: moving to HEAD^
800cab1 HEAD@{2}: commit (amend): add the GPL
b0588af HEAD@{3}: commit: add the GPL
7b57303 HEAD@{4}: commit: change the file
d091d3b HEAD@{5}: commit (initial): add a new file

```

工作区：也就是working directory，也就是电脑内能看到的目录

版本库：工作区内的隐藏目录.git，里面包含了称为stage or index的暂存区，以及master分支和指向master的HEAD指针。

git add是将所有要提交的文件修改先存放到暂存区，然后通过git commit命令将暂存区的修改提交到分支。

———————————————这里是华丽丽的分割线———————————
我们可以用git status查看状态，使用git diff命令查看发生过修改的地方，发生修改后需要使用git add 以及git commit进行提交。commit是通过SHA1计算出的一个非常大的编号，避免多人协作的过程当中版本号出现冲突。
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset –hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本