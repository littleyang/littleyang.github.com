---
uri: /cs/program/java/pattern/facade
permalink: /cs/program/java/pattern/facade/index.html
layout: post
title: "Java模式-Facade Pattern"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 什么是Java-Facade模式

表面模式，从字面上先看看，表面就是不接触内部，嗯，就是这样。不管内部如何只与表面是有关系的。就是我们抽象出一个层，这个层
就是表面，用来与外部接触。好吧，来点官方的描述:

>
>A facade is an object that provides a simplified interface to a larger body of code, such as a class library.
>
>

上面的意思呢很简单吧。它(Facade)有哪些好处呢？

1. 可以在一个软件系统中的类库(library)更容易的用，理解，因为它有一个统一的接口
2. 可读性更佳的增强。
3. 减少内部API或者library与外部的耦合度。

好吧，扯了这么多，上个图吧。

![Imgur](http://i.imgur.com/c7oOAw7.png)

好吧，到这里看懂了吧，那就来点干货，上代码.

--------

### Facade 示例代码:

```java
/**
 * Facade pattern of Java Design Pattern
 * suppose that,you have Camera,Light,Sensor, but your client how to control them?
 * so we can provide a uniform methods of an interface to control them.
 * the main intend of the facade pattern is: make client easily to use your sub-system
 * so think it should be called remote pattern would much more appropriate.
 * Ordinarily, the methods in the facade are static method, which would not be override.
 * @author jenny
 *
 */
 public class Facade {

     private  static Camara camera;
     private  static Lights lights;
     private  static Sensor sensor;
     /*
      * implements the constructor method or we can use a static method to create instances
      */
     static  {
        // TODO Auto-generated constructor stub
        camera = new Camara();
        lights = new Lights();
        sensor = new Sensor();

     }

     public  void turnOn(){
        camera.turnOn();
        lights.turnOn();
        sensor.turnOn();
     }

     public  void turnOff(){
        camera.turnOff();
        lights.turnOff();
        sensor.turnOff();
     }

}


/**
 * this is camera class which have two method: turnOn(),turnOff()
 * @author jenny
 *
 */
 public class Camara {

    public void turnOn(){
         System.out.println("This is the camera method turn on!");
    }

    public void turnOff(){
        System.out.println("This is the camera method turn off!");
    }

}

/**
 * this is the Lights class which has two method: turnOn() and turnOff();
 * @author jenny
 *
 */
 public class Lights {

     public void turnOn(){
         System.out.println("This is the light turn on method !");
     }

     public void turnOff(){
          System.out.println("This is the light turn off method !");
     }

}

/**
 * this is sensor class which has two methods: turnOn() and turnOff();
 * @author jenny
 *
 */
public class Sensor {

   public void turnOn(){
       System.out.println("This is the sensor turn on method !");
   }
   public void turnOff(){
       System.out.println("This is the sensor turn off method !");
   }

}

/**
 * this is the main test method of this pattern
 * @author jenny
 *
 */
public class MainTest {
   public static void main(String[] args){

       Facade facade = new Facade();
       facade.turnOn();
       facade.turnOff();
   }

}

```

很简单吧。

