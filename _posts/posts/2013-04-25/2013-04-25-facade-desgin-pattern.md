---
uri: /cs/program/java/pattern/facade
permalink: /cs/program/java/pattern/facade/index.html
layout: post
title: "Java模式-Facade Pattern"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 什么是Java-Facade模式

表面模式，从字面上先看看，表面就是不接触内部，嗯，就是这样。不管内部如何只与表面是有关系的。就是我们抽象出一个层，这个层
就是表面，用来与外部接触。好吧，来点官方的描述:

>
>A facade is an object that provides a simplified interface to a larger body of code, such as a class library.
>
>

上面的意思呢很简单吧。它(Facade)有哪些好处呢？

1. 可以在一个软件系统中的类库(library)更容易的用，理解，因为它有一个统一的接口
2. 可读性更佳的增强。
3. 减少内部API或者library与外部的耦合度。

好吧，扯了这么多，上个图吧。

![Imgur](http://i.imgur.com/c7oOAw7.png)

