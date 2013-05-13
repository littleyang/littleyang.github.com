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

#### 什么是动态代理呢？

被代理的对象（真实主题（RealSubject））可以在运行时动态改变，需要控制的接口(抽象主题（Subject）)可以在运行时改变，控制的方式也可以动态改变，从而实现了非常灵活的动态代理关系。

#### 实现方法

在java.lang.reflect包中提供了以下的接口实现动态代理。

1. Proxy类，此类表示代理设置，通常为类型（http、socks）和套接字地址。Proxy 是不可变对象，是final类的
2. InvocationHadler(接口): 可以称为调用处理器，是代理实例的调用处理程序 实现的接口。 每个代理实例都具有一个关联的调用处理程序。对代理实例调用方法时，将对方法调用进行编码并将其指派到它的调用处理程序的 invoke 方法。
3. Method（类）: 提供关于类或接口上单独某个方法（以及如何访问该方法）的信息。
所反映的方法可能是类方法或实例方法（包括抽象方法）。

#### 具体怎么去实现一个动态代理呢？

1. 定义一个通用公用的接口(Common interface)
2. 实现一个真实的被代理对象(RealObject)
3. 实现InvocationHadler接口
4. 客户端的调用InvocationHadler接口

看看下面这个具体的代码实例吧:

```java
/**
 * 抽象主题（Subject）
 *
 * 汽车的销售商
 *
 */
public interface CarSeller {

      /*
       * 销售汽车
       */
      public Object sellCars(int type);

}

/**
 * 真实对象(Real Subject)角色
 * 被代理对象
 *
 */
public class AudiCarFactory implements CarSeller {

    /*
    * 实现了抽象主题（Subject）角色的方法
    */
     public Object sellCars(int type) {
         System.out.println("奥迪工厂出售汽车。");
         if(type == 1){
              return "AudiA6";
         }else{
              return "AudiA8";
         }
     }
}

/*
 * 实际提供代理商服务的一个类
 * （很多地方把这个类称为代理类，个人觉得不准确。
 * 它是一个会完成动态代理类的实际工作的类。）
 */
public class CarProxyInvocationHandler implements InvocationHandler {

     Object carSeller = null;

     public CarProxyInvocationHandler(Object carSeller){
           this.carSeller = carSeller;
     }

    /*
     * 代理角色提供服务的真正方法。
     * @see java.lang.reflect.InvocationHandler#invoke(java.lang.Object, java.lang.reflect.Method, java.lang.Object[])
     */
     public Object invoke(Object proxy, Method method, Object[] args){
         Object result = null;

         try {

              serveBeforeSell();
              result = method.invoke(carSeller,args);
              serveAfterSell();
          } catch (Exception e) {
               System.exit(1);
           }

         protected void serveBeforeSell(){

            System.out.println("汽车代理商为客户提供了一些售前服务");

         }
         protected void serveAfterSell(){
            System.out.println("汽车代理商为客户提供了一些售后服务");
         }
     }
}

/**
 * 客户端调用
    */
    public class Customer {

            public static void main(String[] args) {

                //      创建真实主题对象
                CarSeller carSeller = new AudiCarFactory();

                //      通过动态的方式，得到了真正的代理角色对象。
                //      在运行时，真实主题对象，代理角色以及实际完成代理操作的类被关联起来了

                CarSeller carProxy = (CarSeller) Proxy.newProxyInstance(carSeller.getClass()
                                .getClassLoader(), carSeller.getClass().getInterfaces(),
                                                new CarProxyInvocationHandler(carSeller));

                //      由代理商销售汽车
                Object car = carProxy.sellCars(2);
                System.out.println("顾客从代理商那里买了一辆" + car);
            }
    }

