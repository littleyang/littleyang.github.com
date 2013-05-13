---
uri: /cs/program/java/pattern/proxy
permalink: /cs/program/java/pattern/proxy/index.html
layout: post
title: "Java的代理模式"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 代理模式简述

正如现实世界中一样，代理就是一种中介，我要买房(RealObject)，去找房屋代理商(proxyObject)，然后接触到房主，
然后进行房屋买卖(RealObject method call)。代理模式为其他对象提供一种代理以控制对这个对象的访问。在某些情况下，一个 客户不想或者不能直接引用另一个对象，而代理对象可以在客户端和目标对象之间 起到中介的作用。

一般代理模式涉及到三种对象角色:

1. 共同抽象接口(公共角色),声明真实对象和代理对象的共同接口；
2. 代理角色，代理对象角色内部含有对真实对象的引用，从而可以操作真实对象，同时代理对象提供与真实对象相同的接口
以便在任何时刻都能代替真实对象。同时，代理对象可以在执行真实对象操作时，附加其他的操作，相当于对真实对象迚行封装。
3. 真实角色：代理角色所代表的真实对象，是我们最终要引用的对象。

看看下面这个图就显而易见了的。

![Imgur](http://i.imgur.com/54xO3kU.png)



### 代理模式实例

```java

/**
 * the proxy pattern: provide an proxy or surrogate object to control other class object access.
 * but they share a common interface and methods
 * as real world proxy, it just as it!
 * @author jenny
 *
 */
 public interface Common {

      public void saveInfo();

}


public class RealObject implements Common {

    @Override
    public void saveInfo() {
        // TODO Auto-generated method stub
        System.out.println("This is the real object save method!");

    }

}


public class ProxyObejct implements Common {

    // create an proxy object
    private RealObject object;
    // constructor
    public ProxyObejct(RealObject object) {
         // TODO Auto-generated constructor stub
          this.object = object;
    }
    @Override
    public void saveInfo() {
         // TODO Auto-generated method stub
         System.out.println("Begin: This is the proxy obejct and begin to excute!");
        object.saveInfo();
         System.out.println("After: after the execute!");
    }

}

public class MainTest {

      public static void main(String[] args){
           // test
           RealObject rObject = new RealObject();
          // proxy
           ProxyObejct pObejct = new ProxyObejct(rObject);

          pObejct.saveInfo();
    }

}
```

### 动态代理(Dynamic proxy)


