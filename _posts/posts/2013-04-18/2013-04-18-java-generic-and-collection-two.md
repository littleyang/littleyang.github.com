---
uri: /cs/program/java/generic
permalink: /cs/program/java/generic/index.html
layout: post
title: "Java 泛型与集合(泛型,Generic)"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 前言介绍

我们也可以叫做编译期间的类型安全检查机制(compile-time type safety mechenism)</br>
你可以想象一下，世界上各种货币之间的转换问题，你在美国，不可能直接用人民币吧？你在俄罗斯直接用人民币买东西么？那么我们有
没有一种机制可以实现这种在不同地区(不同的情况)下的"货币"的自动结算呢(当然，现实不是那么简单的)？Java 里面的泛型就是为了
解决这个问题而"出生"的,各种数据类型(Integer,int,Booleanboolean,boolean……)就是我们"程序"里面的货币。Java 泛型的引入就是
为了实现数据参数类型的检查转换等，以前是人为的徒手进行，现在可以在编译期间虚拟机通过传递过来的数据判断是什么类型的然后再
创建什么类型的数据执行执行程序(自动打包解包技术,Boxing and Unboxing).下面可以通过这个文字的介绍来了解一下泛型是什么？
这个的主要参考来源于官方的文档，


### 简单的创建一个泛型

在java语法中，可以用<E>申明泛型。如下面的代码所示:

```java
public interface list<E>{
  void add(E x);
  .......
}
```

这种带有参数的类的申明，方法的申明，变量的申明，实例的创建等，我们都叫做泛型。

### 泛型和子类型之间的区别。

#### 两个原则

1. 交换原则(Subsitution principle):给定类型的变量可以赋值给他的子类型;给定参数类型的方法可以被它的子类型参数调用。下面是
引文原文

>
>Substitution Principle: a variable of a given type may be assigned a value of any subtype
of that type, and a method with a parameter of a given type may be invoked with an
argument of any subtype of that type.
>
>

2. 获取和推送原则:当只需要获得某个值时，使用? extends E;当需要推送某个值时,使用? supe E;既需要推送也需要获取时，不使用
任何扩展;一下是原文:

>
>The Get and Put Principle: use an extends wildcard when you only get values out of a
structure, use a super wildcard when you only put values into a structure, and don’t use
a wildcard when you both get and put.
>
>


