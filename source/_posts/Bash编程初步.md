---
title: Bash编程初步
date: 2014-12-16 13:13:40
tags:
---

明天linux要进行考试，我也连夜准备复习linux，linux很有用的一个功能就是linux的shell编程。

linux管理文件的过程中，和windows不同的是，linux管理文件是通过文件扩展名进行管理，例如科执行文件就是.exe，对于linux来说，文件名仅仅是一个识别的标识，意义并不大。而更重要的，是文件的属性，即r-w-x三个属性。对于一个编写的shell脚本程序，我们必须要求它具有可执行，也就是x的权限，即在文件执行之前需要加上chmod +x script_file

#### 运行shell脚本的三种方式

- 脚本加上可执行权限

  ​

  ```
  chmod +x script_file
  ```

  ​

  以当前shell的子进程执行，此方法仅能在bash中顺利执行

- 运行/bin/bash把脚本作为他的参数

  ```
  /bin bash script_file
  ```

- 强制当前shell使用bash执行脚本，为此在脚本开头加

  ```
  #!/bin/bash
  ```

  ​

  当前shell遇到#!，会把其后内容作为绝对路径，使用此路径名制定的程序解析其后脚本

  ​

#### 一些重要的只读Bash环境变量

- $0 程序的名称
- 1−1−9 变量1-9的值
- ∗∗@ 所有的参数
- $#命令参数的个数
- $$进程的PID
- $?最近执行进程的状态
- $!最近执行的后台进程的PID

#### 使用read命令读取数据

```
#!/bin/bash
echo –n “Enter input:”
read line
echo “You entered:$line“
echo –n “Enter another line:”
read word1 word2 word3
echo “The first word is:$word1”
echo “The second word is:$word2”
echo “The rest of the line is:$word3”
exit 0

```

#### 给shell脚本传递参数

1 1 9
\# 参数个数# 参数个数* 所有参数,整个作为字符串
@所有参数,每个参数值作为一个字符串@所有参数,每个参数值作为一个字符串0 脚本文件名

```
#!/bin/bash
echo “The command name is: $0.”
echo “The number of command line arguments passed as
parameters are $#“
echo “The value of the command line arguments are: $1 $2 $3
$4 $5 $6 $7 $8 $9“
echo “Another way to display values of all of the arguments:
$@“
echo “Yet another way is:$*“
exit 0

```

#### 使用shift[n]命令将命令行参数进行平移

```
#!/bin/bash
echo “The program name is: $0.”
echo “The arguments are: $@“
echo “The first three arguments are : $1 $2 $3“
shift
echo “The program name is: $0.”
echo “The arguments are: $@“
echo “The first three arguments are : $1 $2 $3“
shift 3
echo “The program name is: $0.”
echo “The arguments are: $@“
echo “The first three arguments are : $1 $2 $3“
exit 0

```

## 循环以及选择控制条件

#### if-then-elsif-fi

语法结构：

```
if expression
then
        [elif expression
        then
                then-command-list]
        [else
                else-command-list]
fi

```

```
if expression
   then
      then-commands
   else
      else-commands
fi

```

#### 多路跳转语句

```
if expression1
   then
      then-commands
   elif expression2
      elif1-commands
   elif expression3
      elif2-commands
   ...
else
   else-commands
fi

```

#### for语句

语法：

```
for variable [in argument-list]
do
command-list
done

```

```
#!/bin/bash
for people in Debbie Jamie Jhon Kitty Kuhn Shah
do
      echo “$people”
done
exit 0

```

#### while 语句

语法：

```
while expression
do
      commandlist
done

```

#### until语句

语法：

```
until expression
do
     command-list
done

```

```
case test-string in
pattern1)command-list1
;;
pattern2)command-list2
;;
...
patternN)command-list1
;;
esac

```

```
#!/bin/bash
a=1
b=2
c=$a+$b
echo $c

```

```
dream@dream-Inspiron-5520:~/test$ let "a=8" "b=13"
dream@dream-Inspiron-5520:~/test$ let c=a+b
dream@dream-Inspiron-5520:~/test$ echo $c
21

```

#### 使用exprssion命令

```
dream@dream-Inspiron-5520:~/test$ a=8 b=13
dream@dream-Inspiron-5520:~/test$ echo "$((a+b))"
21

```

