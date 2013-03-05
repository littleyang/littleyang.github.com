---
uri: /cs/program/python-second
permalinkt: /cs/program/python-second/index.html
layout: post
title: "python学习【2】"
description: ""
category: ""
tags: []
---

前面开始，已经记录了一些基本的一些入门技巧，下面开始一些基本操作等学习

--------

## python的一些基本操作

任何语言都有对数据的基本操作，一下是python的一些基本操作，数据的加减乘除，字符串的操作等。可以看看一下的一些代码实例:

``` python
x = object()
y = object()

x_list = [x,x,x,x,x,x,x,x,x,x]
y_list = [y,y,y,y,y,y,y,y,y,y]

big_list = []

big_list = x_list + y_list

print "x_list contain %d object" % len(x_list)
print "y_list contain %d object" % len(y_list)

# testing code
if x_list.count(x) == 10 and y_list.count(y) == 10:
	print "Almost there..."
if big_list.count(x) == 10 and big_list.count(y) == 10:
	print "Great!"
```

代码执行如下:

```
  x_list contain 10 object
  y_list contain 10 object
  Almost there...
  Great!
```

## python 的文件基本操作

python 对文件的基本操作，实在是非常的方便，python语法通过严格的缩进已经冒号来控制代码的执行范围，如以下的一些代码示例，显示了同文件夹下面的list.py，按照一行读取一行打印的方式显示出来。

```python
f = open("list.py")
try:
  for line in f:
    print line,
finally:
  f.close()

```

执行结果如下:

```
numbers = []
strings = []
names = ["john","Eric","Jess"]
second_name = names[1]
numbers.append(1)
numbers.append(2)
strings.append("hello")
strings.append("name")
print numbers
print strings
print second_name

print ("the second name on names is %s" % second_name)

```


