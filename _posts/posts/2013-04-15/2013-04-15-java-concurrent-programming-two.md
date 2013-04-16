---
uri: /cs/program/Java-currence/two
permalink: /cs/program/Java-currence/two/index.html
layout: post
title: "Java并发编程【二】"
description: ""
category:
tags: []
---

### 本文简单介绍

本文主要介绍的是Java Concurrent API 中的一些为并发编程提供的一些工具包和并发编程的实现机制。线程池的介绍，附带了部分
代码实例等。java7 自带的thread Synchronization Utilities 是非常方便而且齐全的。下面的类容主要讨论了一下的几个主要内容：

1. 信号量(Semaphores),信号量是一个控制竞争资源的控制权限的一个计数器(counter)。这个机制在很多的其他的并发编程语言中都
有应用。
2. 门闩机制(CountDownLatch),这个机制可以让一个线程等待其他的一个或者是多个线程执行完成(finalization)之后再执行,就像门闩
那样。
3. 关卡机制(CyclicBarrier),这个机制是让多个线程在某一个公共点(common piont)执行，就像等待过关的行人一样。当多人到达之后
在一起开关放行。
4. 相位(Phaser)机制,这个机制是将一个当前的多个任务分开为多个执行阶段。当上一个阶段完成之后才能执行下一个阶段。
5. 数据交换机制。 当在某个临界点上时候，线程之间的数据交换机制。

下面是详细介绍。

-----------

#### 信号量(Semaphores)。

#### 门闩。(CountDownLatch)

#### 关卡(CyclicBarrier)

#### 相位(Phaser)




