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

信号量是对一组竞争资源保护作用的计数器。当一个线程需要获得该资源时必须要获得对应的信号量。如果信号量的计数大于0，则可以
使用该资源，信号量减少1。当信号量为0的时候，线程进入等待状态。当某个线程完成之后，需要释放对应的信号量，以便其他线程使用
一下是简单的代码实现片段:

```java
// 申请一个信号量变量
private final Semaphores semaphore;
// 通过构造器初始化信号量
public className(){
  semaphore = new Semaphores(3);
}

// 在方法中通过Semaphores 的 acquire() 方法获得信号量
public void doSomeWork(){
  try{
      // 获得信号量
      semaphore.acquire();
      // 其他的事情
      doSome();
    }catch(Exeception e){
        // 异常处理
        e.printStackTrace();
    }finally{
      // 释放信号量
      semaphore.release();
    }
}
```

------

#### 门闩。(CountDownLatch)

所谓的门闩就是:让某个线程等待多个操作事件的结束。就像门闩那样，当把所有的门闩都给锁上的时候，门就被上锁了。具体实现是
为某个线程初始化一个操作数(integer operation numbers)，当等待的事件达到这个操作数之后再执行线程。一下是简单的代码实现：
调用wait()方法让线程进入等待状态，当某个事件(Event)完成之后调用countDown()方法来计数。最后当counter为0的时候调用await()
方唤醒线程,这样的情况如一个视频电话会议系统等，当所有人都进入到会议室了才进行开会。

```java
// 创建一个CountDownLatch 对象
private finall CountDownLatch controller;
// 可以通过构造器来实现对controller的初始化
/*
 * 构造器方法
 */
 public constructorMethod(int num){
    controller = new CountDownLatch(num);
}

/*
 * 当某个方法调用这个类时候进行计数
 */
 public void arrived(){
    // 调用countDown()方法计数
    controller.countDown();

}

/*
 *在线程的run方法中调用await()方法唤醒线程
 */
 public void run(){

     try{
       controller.await();
    }catch(Exception e){
       e.printStackTrace();
    }
 }
```

#### 关卡(CyclicBarrier)

#### 相位(Phaser)




