---
title: 正则表达式的应用：Pattern和Matcher类
date: 2015-08-14 13:21:17
tags:
---

感谢 <http://blog.csdn.net/kofandlizi/article/details/7323863>

1.捕获组

捕获组通过从左到右计算开括号开编号。((A)(B(C)))可以分为以下四个组

1.((A)(B(C)))

2.(A)

3.(B(C))

4.(C)

捕获组具体知识参照<http://blog.csdn.net/lxcnn/article/details/4146148>

2.Pattern类

Pattern类用于创建一个正则表达式，它构造函数为私有构造函数，使用Pattern.complie(String regex)简单工厂方法创建正则表达式。

```
Pattern p=Pattern.compile(“\w+”);
p.pattern();//返回 \w+

```

p.pattern返回正则表达式的字符串形式

Pattern相关函数

- Pattern.split(CharSequence input)

Pattern有一个split(CharSequence input)方法,用于分隔字符串,并返回一个String[],我猜String.split(String regex)就是通过Pattern.split(CharSequence input)来实现的.
Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
String[] str=p.split(“我的QQ是:456456我的电话是:0532214我的邮箱是:aaa@aaa.com”);

```

结果:str[0]=”我的QQ是:” str[1]=”我的电话是:” str[2]=”我的邮箱是:aaa@aaa.com”* Pattern.matcher(String regex,CharSequence input)

Pattern.matcher(String regex,CharSequence input)是一个静态方法,用于快速匹配字符串,该方法适合用于只匹配一次,且匹配全部字符串.
Java代码示例:

```
Pattern.matches(“\d+”,”2223”);//返回true
Pattern.matches(“\d+”,”2223aa”);//返回false,需要匹配到所有字符串才能返回true,这里aa不能匹配到
Pattern.matches(“\d+”,”22bb23”);//返回false,需要匹配到所有字符串才能返回true,这里bb不能匹配到

```

\* 3.Pattern.matcher(CharSequence input)

3.Matcher类

- ​

- Matcher.matches()/ Matcher.lookingAt()/ Matcher.find()

Matcher类提供三个匹配操作方法,三个方法均返回boolean类型,当匹配到时返回true,没匹配到则返回false

matches()对整个字符串进行匹配,只有整个字符串都匹配了才返回true
Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
Matcher m=p.matcher(“22bb23”);
m.matches();//返回false,因为bb不能被\d+匹配,导致整个字符串匹配未成功.
Matcher m2=p.matcher(“2223”);
m2.matches();//返回true,因为\d+匹配到了整个字符串
lookingAt()对前面的字符串进行匹配,只有匹配到的字符串在最前面才返回true

```

lookingAt()对前面的字符串进行匹配,只有匹配到的字符串在最前面才返回true

Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
Matcher m=p.matcher(“22bb23”);
m.lookingAt();//返回true,因为\d+匹配到了前面的22
Matcher m2=p.matcher(“aa2223”);
m2.lookingAt();//返回false,因为\d+不能匹配前面的aa

```

find()对字符串进行匹配,匹配到的字符串可以在任何位置.

Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
Matcher m=p.matcher(“22bb23”);
m.find();//返回true
Matcher m2=p.matcher(“aa2223”);
m2.find();//返回true
Matcher m3=p.matcher(“aa2223bb”);
m3.find();//返回true
Matcher m4=p.matcher(“aabb”);
m4.find();//返回false

```

Mathcer.start()/ Matcher.end()/ Matcher.group()

当使用matches(),lookingAt(),find()执行匹配操作后,就可以利用以上三个方法得到更详细的信息.

start()返回匹配到的子字符串在字符串中的索引位置.

end()返回匹配到的子字符串的最后一个字符在字符串中的索引位置.

group()返回匹配到的子字符串

Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
Matcher m=p.matcher(“aaa2223bb”);
m.find();//匹配2223
m.start();//返回3
m.end();//返回7,返回的是2223后的索引号
m.group();//返回2223

```

```
Mathcer m2=m.matcher(“2223bb”);
m.lookingAt();   //匹配2223
m.start();   //返回0,由于lookingAt()只能匹配前面的字符串,所以当使用lookingAt()匹配时,start()方法总是返回0
m.end();   //返回4
m.group();   //返回2223

```

```
Matcher m3=m.matcher(“2223bb”);
m.matches();   //匹配整个字符串
m.start();   //返回0,原因相信大家也清楚了
m.end();   //返回6,原因相信大家也清楚了,因为matches()需要匹配所有字符串
m.group();   //返回2223bb

```

start(),end(),group()均有一个重载方法它们是start(int i),end(int i),group(int i)专用于分组操作,Mathcer类还有一个groupCount()用于返回有多少组.

Java代码示例:

```
Pattern p=Pattern.compile(“([a-z]+)(\d+)”);
Matcher m=p.matcher(“aaa2223bb”);
m.find();   //匹配aaa2223
m.groupCount();   //返回2,因为有2组
m.start(1);   //返回0 返回第一组匹配到的子字符串在字符串中的索引号
m.start(2);   //返回3
m.end(1);   //返回3 返回第一组匹配到的子字符串的最后一个字符在字符串中的索引位置.
m.end(2);   //返回7
m.group(1);   //返回aaa,返回第一组匹配到的子字符串
m.group(2);   //返回2223,返回第二组匹配到的子字符串

```

现在我们使用一下稍微高级点的正则匹配操作,例如有一段文本,里面有很多数字,而且这些数字是分开的,我们现在要将文本中所有数字都取出来,利用java的正则操作是那么的简单.

Java代码示例:

```
Pattern p=Pattern.compile(“\d+”);
Matcher m=p.matcher(“我的QQ是:456456 我的电话是:0532214 我的邮箱是:aaa123@aaa.com”);
while(m.find()) {
     System.out.println(m.group());
}

```

输出:

456456

0532214

123

如将以上while()循环替换成

```
while(m.find()) {
     System.out.println(m.group());
     System.out.print(“start:”+m.start());
     System.out.println(“ end:”+m.end());
}

```

则输出:

456456

start:6 end:12

0532214

start:19 end:26

123

start:36 end:39

现在大家应该知道,每次执行匹配操作后start(),end(),group()三个方法的值都会改变,改变成匹配到的子字符串的信息,以及它们的重载方法,也会改变成相应的信息.
注意:只有当匹配操作成功,才可以使用start(),end(),group()三个方法,否则会抛出java.lang.IllegalStateException,也就是当matches(),lookingAt(),find()其中任意一个方法返回true时,才可以使用.