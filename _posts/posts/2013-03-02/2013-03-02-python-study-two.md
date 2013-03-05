---
uri: /cs/program/python-second
permalink: /cs/program/python-second/index.html
layout: post
title: "python学习【2】"
description: ""
category: ""
tags: []
---

前面开始，已经记录了一些基本的一些入门技巧，下面开始一些基本操作等学习

--------

## 1、python的一些基本操作

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

## 2、python 的文件基本操作

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

## 3、python的循环操作

从数值中找出少于237的偶数并打印。代码已经执行结果如下:

```python
numbers = [951, 402, 984, 651, 360, 69, 408, 319, 601, 485, 980, 507, 725, 547, 544,
  615, 83, 165, 141, 501, 263, 617, 865, 575, 219, 390, 984, 592, 236, 105, 942, 941,
  386, 462, 47, 418, 907, 344, 236, 375, 823, 566, 597, 978, 328, 615, 953, 345,
  399, 162, 758, 219, 918, 237, 412, 566, 826, 248, 866, 950, 626, 949, 687, 217,
  815, 67, 104, 58, 512, 24, 892, 894, 767, 553, 81, 379, 843, 831, 445, 742, 717,
  958, 609, 842, 451, 688, 753, 854, 685, 93, 857, 440, 380, 126, 721, 328, 753, 470,
  743, 527
  ]
for i in numbers:
  if i%2==0 and i<237:
    print i
```

```
236
236
162
104
58
24
126
```


