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


