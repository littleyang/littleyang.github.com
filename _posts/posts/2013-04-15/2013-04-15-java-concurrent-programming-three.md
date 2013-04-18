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
粒度的任务执行，反之则直接执行，可以用下面这个图简单的介绍这个原理。Fork/Join Framework与Executor Framework的主要区别
在于Work-Stealing 算法的不同。下面是它的英文原文解释:

>
>Unlike the Executor framework, when a task is waiting for the finalization of the
subtasks it has created using the join operation, the thread that is executing that task (called
worker thread) looks for other tasks that have not been executed yet and begins its execution.
By this way, the threads take full advantage of their running time, thereby improving the
performance of the application.
>

![pivture](http://i.imgur.com/ZY4UOyw.png)

但是也有它自己不利的地方:

1. 线程任务只能使用fork(), join()方法作为同步机制，二不能使用其他的。
2. 如果应用在I/O上面，性能不好，如文件的读取等。
3. 不能抛出异常，需要自己定义异常的处理

Fork/Join Framework 主要包括以下两个类:

1. ForkJoinPool,是ExecutorService的一个实现类，因此它具有了executor的功能.同时还加入了work-stealing 算法。主要管理线程的
执行以及提供线程执行信息等。
2. ForkJoinTask,是执行在ForkJoinPool中的对象的一个基础类，它提供了fork()和join()的操作。通常你需要实现以下两个子类；
RecursieAction(无返回结果的)和RecursiceTask(有返回结果的)。

下面是一些简单的代码实现实现步骤:

1. 创建一个ForkJoinPool执行任务对象
2. 执行任务中：

```java
If (problem size > default size){
  tasks=divide(task);
  execute(tasks);
} else {
  resolve problem using another algorithm;
}
```

3. 用同步的方法来执行任务。
4. 更具是否需要返回结果来确定需要实现的接口或者继承类
5. 构建自己的异常处理类

在使用该功能的时候同样是具有Executor执行器的功能的。


#### Concurrent Collections


