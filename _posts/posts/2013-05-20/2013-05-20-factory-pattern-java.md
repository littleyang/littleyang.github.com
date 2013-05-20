---
layout: post
title: "factory pattern java"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 静态工厂模式和工厂方法模式

工厂是干嘛的呢？就是加工创造产品的。工厂模式就是管理对象的实例的创建销毁等工作的一种方法。最普通的工厂模式就是简单的将对象
的创建给抽象分层单独出来，来管理对象的创建实例化。下面主要是关于常用的一些工厂的方法。

### 工厂方法模式

工厂方法模式，普通的工厂模式把创建对象实例的工作给独立出来了，那么具体要创建什么类型的对象，这个怎么去确定呢？工厂方法模式
就是一种可以确定需要创建什么对象的实例的方法，具体的创建交给子类去实现，工厂本身没有具体的实现方法。

Factory Method Pattern在父类规定对象的创建方法，但并没有深入到较具体的类名。所有具体的完整内容都放在子类

#### 直接看看下面这个实例

``` java

public class Cup {

    private String shape;
    private String color;

    public String getColor() {
       return color;
    }

    public void setColor(String color) {
       this.color = color;
    }

    public String getShape() {
        return shape;
    }

    public void setShape(String shape) {
        this.shape = shape;
   }

}

/**
 * factory method pattern:
 * Factory Method Pattern在父类规定对象的创建方法，但并没有深入到较具体的类名。
 * 所有具体的完整内容都放在子类
 * @author jenny
 *
 */
public abstract class Factory {

   public final Cup make(String shape,String color){
       Cup cup = makeCup(shape);
       smearColor(cup,color);
       return cup;
   }
   //抽象方法，制作水杯，shape参数指定水杯的外形
   protected abstract Cup makeCup(String shape);
   //抽象方法，给水杯涂上颜色
   protected abstract void smearColor(Cup cup,String color);
}

public class FactoryMethod extends Factory {

    @Override
    protected Cup makeCup(String shape) {
        // TODO Auto-generated method stub
        Cup cup = new Cup();
        cup.setShape(shape);
        return cup;
    }

    @Override
    protected void smearColor(Cup cup, String color) {
        // TODO Auto-generated method stub
        cup.setColor(color);
    }

}

public class MainTest {

    public static void main(String[] args){

        // create an factory
        Factory factory = new FactoryMethod();

        Cup cup1 = factory.make("圆形", "红色");//我要一个圆形，红色的杯子
        System.out.println("杯子造好了");
        System.out.println("形状："+cup1.getShape());
        System.out.println("颜色："+cup1.getColor());

        Cup cup2 = factory.make("方形", "蓝色");//我要一个方形，蓝色的杯子
        System.out.println("杯子造好了");
        System.out.println("形状："+cup2.getShape());
        System.out.println("颜色："+cup2.getColor());

   }

}

```

### 静态工厂模式

先来看张UML图：




上面这个模式很简单也很清晰:







