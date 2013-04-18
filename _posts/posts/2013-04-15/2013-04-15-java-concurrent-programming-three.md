---
uri: /cs/program/Java-currence/three
permalink: /cs/program/Java-currence/three/index.html
layout: post
title: "Java并发编程【三】"
description: ""
category:
tags: []
---

### 简要介绍

这个文档主要介绍的是Java Concurrent API 中关于 Fork/Join Framework 一些内容和机制;还有就是Java Concurrent API 中集合类
的使用等一些内容。

------

#### Fork/Join Framework

自Java 5 以来引入了执行器的机制之后，就把线程的创建和执行分开来，你只需要创建Runnable 对象然后传递给执行器即可;自java 7
以后又引入了Fork/Join Framework 机制，更进一步的完善了执行器的功能。这个机制运用了分治技术(Divide And Conquer Technology)
主要目的是将线程分为细小的步骤执行。在这机制里面，某个任务的问题数量，是否多余指定的数量，如果多余指定的，那么就分为更小
粒度的任务执行，反之则直接执行，可以用下面这个图简单的介绍这个原理。
![pivture](http://i.imgur.com/ZY4UOyw.png)


#### Concurrent Collections


