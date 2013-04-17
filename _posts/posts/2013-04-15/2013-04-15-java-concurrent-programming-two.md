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

在很多时候也许会遇到这样的情况，多个线程需要在某个公共点上来执行，这个就是我们的CyclicBarrier。这个乍看起来有点像是
CountDownLatch,但是又不是。CyclicBarrier 比 CountDownLatch 有更强大的功能。CyclicBarrier 初始化了一个需要等待线程的
整数，当线程到达这个点时候调用await()方法来等待其他线程的完成。只有最后一个(numbers)线程到达这个点的时候，才唤起其他
线程继续执行。并且这个类可以接受一个thread对象，当所有thread到来之后进行执行。

```java
public class OneClass implements Runnable{
  // 创建一个CyclicBarrier 对象
  private final CyclicBarrier barrier;
  // 通过构造器方法来实现barrier的初始化
  public ClassNameMethod(CyclicBarrier barrier){
    this.barrier = barrier;
  }
  /*
   *在线程的run方法中调用barrier的await()方法
   */
  public void run(){
    doSome();
    try{
      barrier.await();
    }catch(Exception e){
      // 异常处理
      e.printStackTrace();
    }
  }
}
/**
 * 同时构造另外一个可以执行的线程类
 */
public AnotherClass implements Runnable{

  // 重写run方法、
  public void run(){
    doSomeThing();
  }
}
/**
 * mainClass
 */
 public class MainClass{
    public static void main(String[] args){
      // 创建CyclicBarrier 对象
      // 创建一个需要执行的对象
      AnotherClass another = new AnotherClass();
      //表示在五个线程到来的时候同时执行another对象,当做线程来执行
      CyclicBarrier barrier = new (5,another);
      doSomeOtherTask();
    }
}

```

#### 相位(Phaser)

自Java7以后，引入了Phaser的类。Phaser 类提供了并发阶段性任务的功能。这样可以将某个线程任务分割为阶段性的步骤。这样的机制
中所有的线程都在等待第一步完成之后再进行第二步。在创建Phaser对象的时候要初始化需要同步的操作数,同时也可以动态的增加或者
减少这个值。

```java
/**
 *创建第一个对象
 */
 public class ClassOne{

    // 申明Phaser对象
    private Phaser phaser;
    // 通过构造器实现Phaser对象的初始化
    public ClassOne(Phaser phaser){
        this.phaser = phaser;
    }
    // 在方法中调用arriveAndRegister()方法来触发等待
    public void doSomeWork(){
      doSome();
      phaser.arriveAndRegister();
      // 或者调用arriveAndAwaitAdvanced()方法来等待某个第二阶段
      // phaser.arriveAndAwaitAdvanced();
      doSomeOtherTask();
    }
    // 重写run方法
    public void run(){
      // 调用arriveAndAwaitAdvanced();
      doSomeWork();
      phaser.arriveAndAwaitAdvanced();
    }
 }
```

#### 并发线程之间的数据交换

在Java API中提供了Exchanger类用于并发线程之间的数据交换功能。当两个线程到达某个临街面(critical section)的某个点
(commont point),他们可以实现数据间的内部交换(interchanger),第一个线程的是数据进入到第二个线程，第二个线程的数据进入到
第一个。具体用法可以去参考oracle 提供的Java API。

-----------

### 线程执行器(Thread Executor)和线程池(Thread pool)

通常的情况下，我们创建并发一般都是创建Runnable对象然后创建对应的Thread对象来执行，当有很多并发对象的时候，明显这样的机制
不实用了。那么这个时候我们可以使用线程执行器(Thread Executor)。自Java5以后，提供了Executor Framework完成这样的工作。
Executor 是一个接口，ExecutorService和ThreadPoolExecutor是它的一个子接口。这样的机制把线程的创建和执行分开了。这样你只
需要创建Runnable 对象(Object),然后传递给线程执行器(Thread Executor),而不必要创建对应的Thread 对象来执行这个线程对象。
而且Executor Framework 还提供了Callable()接口，与Runnable类似，在它的call()方法里面可以返回执行结果，来知道线程的执行。这
是一个有用机制和功能。

#### 创建一个线程执行器

下面这个简单的例子是简单的线程执行器的创建。

```java
/**
 *创建Runnable 类
 */
public class TestCase implements runnable{

    // override the run method
    public void run(){
      // do some work
      doSomeWork();
    }
}
/**
 *创建线程执行器
 */
public class TestMain{
  // main method
  public static void main(String[] args){
    // 创建线程执行器
    ThreadPoolExecutor executor = new (ThreadPoolExecutor)Executors.newChachedThreadPool();
    // 创建任务对象
    TestCase task = new TestCase();
    // 然后将task 传递给执行器
    executor.execute(task);
    // 其他代码
    doSomeOtherTask();

    // 关闭线程执行器
    executor.shutdown();
  }
}
```

#### 线程池的分类

创建的线程池主要有三种类型:

1. 动态增加的(fixedThreadPool),这个线程池的可执行的线程数量根据实际需要的线程对象多少来创建的。大小可变的。调用
newFixedThreadPool()方法来创建。
2. 固定大小的线程池对象,在创建的时候指定线程的数量.这个的特点是当所有线程已经使用的时候，其他新来的线程需要等待线程池释放
线程对象。
3. 单个的线程池对象,顾名思义，里面只有一个可以执行的线程对象，可以调用newSingleThreadPool()方法来创建.


