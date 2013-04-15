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

#### 线程同步的基本方法

##### 运用Synchronized关键字进行同步
##### 运用Java提供的锁机制(Lock Mechanism)




