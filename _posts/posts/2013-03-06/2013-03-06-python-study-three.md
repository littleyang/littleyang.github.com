---
uri: /cs/program/python-three
permalink: /cs/program/python-three/index.html
layout: post
title: "python 学习 【3】"
description: ""
category:
tags: []
---

python 是一个面向对象的语言，对于任何一个面向对象的语言而言，类和对象完全是一系列非常重要的概念。类就是包括了一些变量和方法的实体的一个概括。可以通过实例化来创建一个该类的实例个体。下面有一段关于类的概念和作用的比较到位的一个秒速:

>   Objects are an encapsulation of variables and functions into a single entity. Objects get their variables and functions from classes. Classes are essentially a template to create your objects.


-----

### 1、一个简单的python类实例以及代码示例,代码以及执行结果如下:

里面包含了类的定义，类的创建，类的变量使用函数调用等。

```python

1 class MyClass:
2   variable = "blah"
3
4   def function(self):
5     print "this is class function"
6
7 my_object = MyClass()
8
9 print my_object.variable
10 my_object.function()
```

```
blah
this is class function
```
