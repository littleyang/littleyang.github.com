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

### 2、关于类的一个简单的联系，问题秒速如下:

> 定义一个关于car的类，有两个实例MyCar1和MyCar2,输出两个实例的描述:MyCar1 to be a red convertible worth $60,000 with a name of Fer, and MyCar2 to be a blue van named Jump worth $10,000.

一下是代码的实现以及执行结果，总的来说，都是为了更加深入的理解python 类的概念以及使用，类与对象是一个通用的编程概念。

```python
class Car:
  name = ""
  kind = "car"
  color = ""
  value = 100.00
  def description(self):
    desc_string = "%s is a %s %s worth $%.2f." %(self.name,self.color,self.kind,self.value)
    return desc_string

MyCar1 = Car()
MyCar1.name ="Fer"
MyCar1.color="red"
MyCar1.value = 60000
print MyCar1.description()

MyCar2 = Car()
MyCar2.name = "Jump"
MyCar2.color = "blue"
MyCar2.value = 10000
print MyCar2.description()
```
执行结果如下:

    Fer is a red car worth $60000.00.
    Jump is a blue car worth $10000.00.


