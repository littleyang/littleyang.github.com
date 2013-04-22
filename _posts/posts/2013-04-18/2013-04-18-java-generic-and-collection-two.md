---
uri: /cs/program/java/generic
permalink: /cs/program/java/generic/index.html
layout: post
title: "Java 泛型与集合(泛型,Generic)"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 前言介绍

我们也可以叫做编译期间的类型安全检查机制(compile-time type safety mechenism)</br>
你可以想象一下，世界上各种货币之间的转换问题，你在美国，不可能直接用人民币吧？你在俄罗斯直接用人民币买东西么？那么我们有
没有一种机制可以实现这种在不同地区(不同的情况)下的"货币"的自动结算呢(当然，现实不是那么简单的)？Java 里面的泛型就是为了
解决这个问题而"出生"的,各种数据类型(Integer,int,Booleanboolean,boolean……)就是我们"程序"里面的货币。Java 泛型的引入就是
为了实现数据参数类型的检查转换等，以前是人为的徒手进行，现在可以在编译期间虚拟机通过传递过来的数据判断是什么类型的然后再
创建什么类型的数据执行执行程序(自动打包解包技术,Boxing and Unboxing).下面可以通过这个文字的介绍来了解一下泛型是什么？
这个的主要参考来源于官方的文档，


### 简单的创建一个泛型

在java语法中，可以用<E>申明泛型。如下面的代码所示:

```java
public interface list<E>{
  void add(E x);
  .......
}
```

这种带有参数的类的申明，方法的申明，变量的申明，实例的创建等，我们都叫做泛型。

### 数据的打包与解包(Boxing And Unboxing)

1. 对应的原始数据类型转化为引用类型，叫做打包。
2. 对应的引用类型转化为原始类型叫做解包。
3. 基本数据类型与对应的引用类型。

>
> byte----------Byte
> short----------Short
> int -----------Integer
> long ----------Long
> float --------- Float
> double --------- Double
> boolean --------- Boolean
> char ------- Character
>


### 泛型和子类型,通配符

#### 两个原则

1. 交换原则(Subsitution principle):给定类型的变量可以赋值给他的子类型;给定参数类型的方法可以被它的子类型参数调用。下面是
引文原文

>
>Substitution Principle: a variable of a given type may be assigned a value of any subtype
of that type, and a method with a parameter of a given type may be invoked with an
argument of any subtype of that type.
>
>

2. 获取和推送原则:当只需要获得某个值时，使用? extends E;当需要推送某个值时,使用? supe E;既需要推送也需要获取时，不使用
任何扩展;一下是原文:

>
>The Get and Put Principle: use an extends wildcard when you only get values out of a
structure, use a super wildcard when you only put values into a structure, and don’t use
a wildcard when you both get and put.
>
>

#### 类型与子类型之间的问题

首先看看下面这个代码有什么问题:

```java
// 定义一个list，用string为泛型参数
List<String> list = new ArrayList<String>();
// 定义个obs list,用Object作为泛型参数
List<Object> obs = list;
```

上面的代码有什么问题么？问题在于第二行，list赋值给obs,是会出现编译错误的。为什么呢？问题String不是Object的子类么？那么list
也是obs的子类么？第一个问题是肯定的，第二个问题是否定的。那他们之间有什么关系么？答案是他们之间没什么关系。
</br>

通常的，如果Foo是Bar的子类型(subclass or subinterface),G是泛型类型申明,那么G<Foo>并不是G<Bar>的子类，他们之间没什么关系。
怎么理解呢？你可以想象一下，苹果是水果，橘子也是水果，但是水果是橘子是苹果么？就这么简单。

#### 通配符(Wildcard)

先看看下面的这段代码:

```java
/*
 * 没有泛型之前我们写一个循环
 */

void printCollection(Collection c) {
  Iterator i = c.iterator();
  for (k = 0; k < c.size(); k++) {
      System.out.println(i.next());
  }
}

/*
 * 泛型之中的新的循环方式
 */

void printCollection(Collection<Object> c) {
  for (Object e : c) {
    System.out.println(e);
  }
}

```

第一个，我们可以对任何的集合进行循环输出，第二个我们只能对Obejct类型的集合进行输出，似乎第一个比第一个有用多了，虽然第二个
简单明了。那么我们能不能修改一下让第二个也可以对任意的集合类进行迭代输出呢？来看看下面的代码:

```java

void printCollection(Collection<?> c) {
  for (Object e : c) {
    System.out.println(e);
  }
}
```
这次可以了，我们可以对任何的集合类型进行输出了。与上面相比我们把Obejct用?代替了，也就是说？作为一个通配符使用了。在java
泛型中我们使用？来作为通配符,"通行证"。

#### 绑定一个通配符

假如你有一个画图的程序，你想画圆，又想画长方形，那么我们怎么识别这个形状呢？来看看下面的代码结构。

```java
/**
 * define shape class
 */
public abstract class Shape{
  public abstract void draw();
  ……
}
/**
 * define the circle class
 */
public class Circle extends Shape{
  ……
  public void draw();
  ……
}
/**
 * define the rectangle class
 */

public class Rectangle class {
  ……
  public void draw();
  ……
}
/**
 * the main test class
 */
public class Main{
  // define a main drawmethod
  drawAll(List<? extends shape> shapes){
    for(Shape s:shapes){
      s.draw();
    }
  }
}

```

通过这个代码可以清楚的看到，我们可以通过extends 关键之将通配符绑定为某个类型，但是这个是不适合把元素添加进去通配符的。因为
一个类的子类有可能是其他的什么类，无法确定类型。如果需要添加元素，那么我们可以用下面这种语法

```java

public class AddClass{

  public void addAll(List<? super Shape> shapes,list<Circle> cirlcs ){
    for(Circle c:cirlcs){
      shapes.add(c);
    }
  }
}
```

### 泛型方法

从上面的两个原则中，我们可以明白泛型的子类型是可以调用泛型方法的。泛型方法的定义如下:

```java
public <T> boolean containAll(Collection<T> c);

public <T extends E> boolean addAll(Collection<T> x);

```


