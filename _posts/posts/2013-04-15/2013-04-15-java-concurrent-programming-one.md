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

----------------

##### 线程的中断控制和睡眠唤醒等

1. 我们可以调用thread的sleep()方法让一个正在执行的线程进入暂停状态。
2. 调用thread.interrupt()方法可以中断一个线程。
3. 当多个线程在执行的时候我们可以调用thread.join()的方法来加入线程的执行，知道线程执行完成。

##### 线程的局部变量，线程组，线程的工厂创建模式

1. 当你在创建某个线程任务对象，但是却有多个线程实例的时候，这些线程实例共享这个对象的所有属性。某一个线程实例对这个对象做出改变的时候，其他的线程对象得到的也就是修改过的对象。当然这个可能不是你需要的。这个时候你希望某个线程实例有自己的"私有属性"这个时候，线程的local 变量就很有意义了(thread-local-variable)。我们可以用ThreadLocal<?>这个接口俩创建一个thread-local-variable变量，如下面的代码所示:

```java
private static ThreadLocal<Date> startDate= new
ThreadLocal<Date>() {
  protected Date initialValue(){
    return new Date();
  }
};
```

2. Java Concurrence API 同时也还提供了其他的一个有趣的基本功能。就是你可以把多个线程当做一个线程组为一个执行单元来执行。ThreadGroup class 提供了这样的功能。如下面这个简单的代码片段:

```java
    ThreadGroup threadGroup = new ThreadGroup("Searcher");
    Result result = new Result();
    SearchTask searchTask = new SearchTask(result);
    for (int i = 0; i < 5; i++) {
       Thread thread = new Thread(threadGroup, searchTask);
       thread.start();
       try {
             TimeUnit.SECONDS.sleep(1);
       } catch (InterruptedException e) {
            e.printStackTrace();
          }
    }
```

3. Thread的工厂创建模式
工厂模式就是使用工厂类代替了额new的功能来创建对象。一下是一个简单的Thread 工厂类。

``` java

package thread.factory;

import java.util.ArrayList;
import java.util.Date;
import java.util.Iterator;
import java.util.List;
import java.util.concurrent.ThreadFactory;

public class MyThreadFactory implements ThreadFactory{

    //store the numbers of object have been created by factory
    private int counter;
    //store the name have been created
    private String name;
    //store the object status
    private List<String> status;

    //define the constructor
    public MyThreadFactory(String name){
        this.name = name;
        this.counter = 0;
        status = new ArrayList<String>();
    }
    //to override the create object method
    @Override
    public Thread newThread(Runnable r) {
        //TODO Auto-generated method stub
        Thread thread = new Thread(r,name+"-Thread_"+counter);
        counter++;  // when a new object created,counter = counter + 1
        status.add(String.format("Created thread %d with name %s on %s\n",thread.getId(),thread.getName(),new Date()));
        //return the created thread
        return thread;
    }
    /*
     * implement the get statistic method
     * @return a String object with the statistical data of all the Thread objects created
     */
    public String getStatus(){
        //return status string
        StringBuffer sb = new StringBuffer();
        //status iterator
        Iterator<String> it = status.iterator();
        //loop for get status
        while(it.hasNext()){
             sb.append(it.next());
             sb.append("\n");
        }
        //return the buffer to string
        return sb.toString();
    }
}
```

------

#### 线程同步的基本方法

在很多情况下，多个线程可以共享一个或者多个资源(resource),这样就会导致资源的竞争。比如说银行系统，你又存折也有卡，你可以用
两个人同时操作这个账户么？那银行不得亏死啊？(怎么可能！).现在必然面对这个问题。那么同步就是我们的解决方式。当一个线程占用
某个资源的时候，其他的如果需要用，对不起，请你排队等待。这个就是同步，意思就是，我在用的时候，资源跟着我跑。我跑完了，才
放开，让别人用。

##### 运用Synchronized关键字进行同步

1. 同步一个方法(Synchronization a method)

这个呢，也就是在声明方法的时候在权限(public,private,protected)之后synchronized 关键字标志这个方法是同步的。方法里面的
参数变量，资源等都是只能让一个线程使用。如果有static关键字修饰的话就是表示一次只能有一个对象可以调用该静态类方法。如:

```java
public synchronized void getName(){
  dosome();
}
```

2. synchronized 不能修饰变量(不能用于变量申请之前，如:private synchronized string name)。同步一个代码块
我们可以将需要同步的资源包括进synchronized关键字的代码块里面。也可以再代码块中同步一个变量，用于控制某些特殊的情况。
如下面的代码片段:

```java
public String returnName(user){
    synchronized(user){
        return user.getName();
    }
}

public void addBalance(int mount){}
    synchronized{
      int temp = this.balance;
      balance = temp+mount;
  }
}
```

3. 在synchronized 中使用条件判断(conditions),在同步中我们使用wait(),notify(),nootifyAll()方法来叫醒通知其他正在等待的线程
如下面的代码片段，其中最著名的一个问题就是producer-customer问题。

```java
/*
 * the producer set method
 */
public synchronized void set(){
    while(producer.store==Max){
       try{
            wait();
       }catch(Exeception e){
            e.PrintStakeTrace();
       }
    }
    // notify customer thread
    notify();
}

/*
 * the producer get method
 */
 public synchronized void get(){

    while(producer.size==0){
        try{
            wait();
        }catch(Exeception e){
          e.PrintStakeTrace();
        }
    }
    notify();
 }

```

##### 运用Java提供的锁机制(Lock Mechanism)

Java 提供了另外机制来实现对资源的同步，那就手锁的机制。锁(Lock)是Java Concurrent API里面的一个接口。是一个比synchronized
更为强大和更为灵活的机制(mechanism),这个机制拥有以下的几个优点。

1. 可以以一种更为灵活的方式来构建你的同步代码块(synchronized code block)。在使用synchronized时候，你必须要释放资源的控制
权限一边其他资源的使用，而锁有更多的灵活方法来实现。
2. Lock 提供了更多的函数方法来实现比synchronized 更多的功能。
3. Lock可以通过读写锁来分离对资源的读写。read lock 允许更多的读取而不能修改。write lock则允许一个线程来修改。
4. 锁提供了更好的性能。

------

##### 锁的使用

一般而言，锁都是申请为最终变量(final),在需要的地方调用锁的lock方法，在不使用的时候调用unlock()释放锁即可。

```java
private final Lock queueLock=new ReentrantLock();


public void printMessage(){
    queueLock.lock();
    try{
        dosome();
    }catch(Exeception e){
      e.PrintStakeTrace();
    }
    queueLock.unlock();
}
```

##### 读写锁

在java提供的并发编程API中，读写锁(ReadWriteLock Interface)是一个非常重要的改进。ReentrantReadWriteLock 类是一个实现，当然
也可以自己实现方法。读写锁将一个锁分成了两个锁，read和write thread，一个是用于读操作一个用于写操作。可以多读，不能多写，
但是当一个线程在写的时候，其他线程是不能读取这个资源的。使用读写锁的代码片段如下:

```java
// 定义一个读写锁
private ReadWriteLock lock;
// 在一个方法中使用读写锁
public void useReadWriteLockRead(){
  lock.readLock().lock();
  // do something
  doSome();
  lock.readLock().unlock();
}
// 使用写锁
public void useReadWriteLockWrite(){

  // 锁定资源，其他的读写锁则不能读
  lock.writeLock().lock();
  // do something
  doSome();
  // 释放锁
  lock.writeLock().unlock();
}
```

##### 修改锁的执行标准

在使用锁的时候可以带一个boolean参数构建锁(fair mode)。 true表示锁在执行的时候使用fair mode ，该模式表示当锁被释放以后，
被该锁锁定的资源会选择等待时间最多的线程去执行，反之则是随机选择需要该资源的线程。代码很简单：

```java
// 创建锁对象的时候使用fair mode
private Lock lock = new ReentrantLock(true);
```

##### 锁的多条件控制

我们可以通过 Java Concurrent API 的Condition 接口来实现锁的多条件控制。该机制可以让一个线程获得锁通过对Condition 的返回值
true or false


