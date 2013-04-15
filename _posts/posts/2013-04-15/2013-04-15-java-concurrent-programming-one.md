---
uri: /cs/program/Java-currence/one
permalink: /cs/program/Java-currence/one/index.html
layout: post
title: "Java并发编程【一】"
description: ""
category:
tags: []
---

### 简要介绍

自从Java5以来，Java 提供了很多的机制来解决并发程序的需要。并且在java6和java7中引入了一系列的API来解决实际需要，增加了更多
的应用性和实际应用案例，如Concurrent Fork/Join framework,线程池(Thread Executor),线程集合类等接口或者基础类。提供了
一系列的方法，更加简便方便的达到编程应用的需要。</br>
这里主要是关于线程的基础管理(basic management),线程的基础同步(Basic Thread Synchronization)和Java提供的一些同步工具
(Thread Synchronization Utilities)

-------------

#### 基本线程的管理，创建，启动等

##### 创建和获得基本的线程信息

创建线程我们可以有两种基本的方法:

1. 我们可以实现 Runnable 的接口，Runnable Interface 是支持多继承的。
2. 同时我们也可以通过集成Thread 类来创建一个线程。但是Java是单继承的。

两种方式都是需要重写(Override)run 方法的。同时我们还可以调用线程的一些基本方法来获得线程的一些基本信息如ID，Status,Name
priority等信息。网上有很多的这样的简单示例。不多做叙述。



