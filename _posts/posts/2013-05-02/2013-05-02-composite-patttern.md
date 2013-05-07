---
uri: /cs/program/java/pattern/composite
permalink: /cs/program/java/pattern/composite/index.html
layout: post
title: "Java模式--符合模式(Composite Pattern)"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 先简单的说说概念吧

什么是复合模式呢？我觉得叫做组合模式更为贴切一点。先看看定义:

>
>The composite pattern describes that a group of objects are to be treated in the same way as a single instance of an object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies. Implementing the composite pattern lets clients treat individual objects and compositions uniformly
>
>

上面是说呢，我们可以把一大波的对象组合成为一个组，然后再迭代处理的时候把它当最最终处理的对象一样的。好，上图上真相:

![Imgur](http://i.imgur.com/c5OAzy5.png)

看看上面这个图，leaf 这个对象就是我们的最终对象，composite的处理就像是处理Leaf一样，当然composite里面都是Leaf的集合，他们
共同继承于component(这个可以是接口，可以是静态类)。可以用数据结构里面的树来描述一个复合模式的结构。

#### Component

1. 是最终处理类的抽象集合，其他的都继承于这个类。
2. 为最终处理对象定义了一系列的方法。

#### Leaf

1. 表示了最终叶子节点的对象。
2. 继承了所有的component方法。

#### composite

1. represents a composite Component (component having children)
2. implements methods to manipulate children
3. implements all Component methods, generally by delegating them to its children
4. 是leaf集合处理类，在调用的时候我们使用这个类就像使用leaf一样，里面包含了一些了的迭代方法处理一组Leaf

那我们经常在什么情况下使用这个模式呢？

>
>Composite can be used when clients should ignore the difference between compositions of objects and individual objects.[1] If programmers find that they are using multiple objects in the same way, and often have nearly identical code to handle each of them, then composite is a good choice; it is less complex in this situation to treat primitives and composites as homogeneous.
>
>自己去翻译这个英文吧。看客

#### 需要面对的问题

最主要的问题就是在composite中避免死循环的问题,无限循环的问题

#### 看个具体的代码实例：一个二级目录显示

```java

/**
 * component
 * @author jenny
 *
 */
public abstract class Moive {

     public String name;

     public ArrayList<Moive> list;

     public abstract void add(Moive moive);

     public abstract void remove(Moive moive);

     public abstract void display();


}

/**
 * Composite class
 * @author jenny
 *
 */
public class CompsiteMoive extends Moive {

    public CompsiteMoive(String name) {
        // TODO Auto-generated constructor stub
        this.name = name;
        this.list = new ArrayList<Moive>();
    }

    @Override
    public void add(Moive moive) {
        // TODO Auto-generated method stub
        list.add(moive);

   }

    @Override
    public void remove(Moive moive) {
        // TODO Auto-generated method stub
        if(list.contains(moive)){
             list.remove(moive);
        }
    }

    @Override
    public void display() {
         // TODO Auto-generated method stub
         for(Moive moive:list){
              moive.display();
          }

     }

}



/**
 * leaf class
 * @author jenny
 *
 */
 public class Program extends Moive {

     public Program(String name) {
       // TODO Auto-generated constructor stub
       this.name = name;
     }

     @Override
     public void add(Moive moive) {
        // TODO Auto-generated method stub
        System.out.println("you can't add component to a proagram object");

     }

     @Override
     public void remove(Moive moive) {
       // TODO Auto-generated method stub
       System.out.println("you can't remove component to a proagram object");

      }

     @Override
     public void display() {
        // TODO Auto-generated method stub
        System.out.println("----------"+name);

     }

}

/**
 * main test
 * @author jenny
 *
 */
public class MainTest {

    public static void main(String[] args){
         // 具体对象科幻
         Program one = new Program("钢铁侠1");
         Program two = new Program("钢铁侠2");
         Program three = new Program("钢铁侠3");
         // 具体对象神话
         Program  hone = new Program("倩女幽魂1");
         Program htwo = new Program("倩女幽魂2");
         Program hthree = new Program("倩女幽魂3");
         Program tone = new Program("变形金刚");
         Program ttwo = new Program("少林寺");

         //目录对象
         // 二级目录
         CompsiteMoive mone = new CompsiteMoive("国内");
         CompsiteMoive mtwo = new CompsiteMoive("国外");
         //一级目录
         CompsiteMoive mone1 = new CompsiteMoive("科幻");
         CompsiteMoive mtwo1 = new CompsiteMoive("神话");
         // 根目录
         CompsiteMoive root = new CompsiteMoive("root");
         // 一级目录添加内容
         mone1.add(ttwo);
         mtwo1.add(tone);
         // 二级目录添加内容
         mone.add(hone);
         mone.add(htwo);
         mone.add(hthree);
         mtwo.add(one);
         mtwo.add(two);
         mtwo.add(three);
         //二级目录分别添加到一级目录
         mone1.add(mone);
         mtwo1.add(mtwo);
         //根目录添加内容
         root.add(mone1);
         root.add(mtwo1);
         root.display();

     }

}

```

输出结果:

```
----------少林寺
----------倩女幽魂1
----------倩女幽魂2
----------倩女幽魂3
----------变形金刚
----------钢铁侠1
----------钢铁侠2
----------钢铁侠3
```

