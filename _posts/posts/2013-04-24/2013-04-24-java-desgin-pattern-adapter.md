---
uri: /cs/program/java/desginpatern/adapter
permalink: /cs/program/java/desginpatern/adapter/index.html
layout: post
title: "Java设计模式-适配器模式"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 什么是模式？

这个问题实在是太大了，每个人的理解也存在偏差和不同。在软件设计领域里面，模式是一种经验和方法的总结。把遇到的各种问题总结
为一类方法或者一种解决方案。具体定义请参考网上资料的各种解释，
[维基百科](http://en.wikipedia.org/wiki/Software_design_pattern)个人认为比较精准。
我们把它理解为一种方法论好了。

### 适配器模式(Adapter Pattern)

我更宁愿把叫做连接器模式。先来看下面几张类层次图，介绍了这个模式的结构。这个模式是面向接口的，比如你的手机充电是需要2V，
但是现在是220V，那么我们就需要一个适配器将220V的电压转换为10V的。这个描述为:客户端接口或者程序需要调用我们的目标接口或者
类，需要通过统一的接口对象去使用。我的目标接口需要具体的实现某个方法，但是但是这个方法在另外的类具有，那么我们就通过适配器
去调用这个方法实现。

![Imgur](http://i.imgur.com/n1XkRyq.png)
![Imgur](http://i.imgur.com/2ruaxpa.png)

--------

![Imgur](http://i.imgur.com/bCBGSih.png)
![Imgur](http://i.imgur.com/HZ1DrjS.png)

上面的图片第一组(1,2),我们叫做对象适配器(Object Adapter);第二组(3,4)我们叫做类适配器(Class Adapter),
其区分是在于适配器(Adapter)与被适配对象(adaptee)之间的实现关系，如果Adaptee 为一个成员，则是对象适配器；继承则是对象适配器
下面详细介绍一下和一些实例代码:

### 对象适配器(Obejct Adapter)

好吧，那什么样的适配器才是对象适配器呢？看看上面的图片，我们在适配器(Adapter)中创建一个Adaptee的对象，然后再相应的方法里面
调用该对象的方法就叫做对象适配器。下面用一个具体的实例看看:

```java

/**
 * this is the client want to use interface
 * @author jenny
 * 首先创建一个目标对象接口，我么需要调用这个不表对象作为测试
 *
 */
public interface Target {

    void printList(ArrayList<String> list);

}

/**
 *Adaptee对象实现类接口
 */
public interface AdapteeI {

      public void printString(String s);

}

/*
 *目标对象实现类实现
 */
public class Adaptee implements AdapteeI {

    public void printString(String s){

        System.out.println(s);
    }

}
/*
 * 适配器类，在适配器中创建一个被适配的兑现的具体实例
 */

public class Adapter implements Target {
    public void printList(ArrayList<String> list) {

      //Converting ArrayList<String> to String so that we can pass String to
      // adaptee class
      String listString = "";

      for (String s : list){
        listString += s + "\t";
      }

      // instantiating adaptee class
      Adaptee ps =new Adaptee();
      ps.printString(listString);
    }
}

/*
 * 主要测试函数
 */

public class Client {
    public static void main(String[] args){
        ArrayList<String> list=new  ArrayList<String>();
        list.add("one");
        list.add("two");
        list.add("three");
        Adapter pl = new Adapter();
        pl.printList(list);

    }

}

```

运行上面的程序结果如下:

```
one two three

```


### 对象适配器(Class Adapter)
