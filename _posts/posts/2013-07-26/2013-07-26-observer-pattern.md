---
uri: /cs/program/java/pattern/observer
permalink: /cs/program/java/pattern/observer/index.html
layout: post
title: "Java的观察者模式"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 胡说

最近看了一本关于设计模式的书----《漫谈设计模式》，也在思考到底设计模式为什么？什么是设计模式？我个人认为设计模式就是面向
面向对象程序里面，怎么样更好的去组织各种类之间的关系，让这些类在软件体系里面工作的更好更有效；更好的软件架构和设计；更好的代码文档组织规范；看起来更漂亮更容易理解和维护。设计模式本身是各种经验。

### 观察者模式

旁观者清。总的来说就是，我们有一系列的旁观者对象，去关注某个类执行某个动作和该类状态的改变，同时更新自己(观察者)的信息。
可以看看下面这个观察者模式的类图。
![Imgur](http://i.imgur.com/cSfuNDu.png)

可以简单的解释一下上面这个图：

1. 有个subject主题接口，里面定义了被观察者的规范，包括了通知观察者方法notifyObserver(),addObserver(),deleteObserver(),该
接口可以为一个抽象类里面的持有一个关于observer的list或者其他集合。
2. 具体的ConcretSubjecA和ConcretSubjectB都继承或者实现该Subject接口。具体实现各个方法
3. Observer接口定义了观察是的一些规范，定义了一个更新当前信息的方法notify()
4. 具体的观察者ConcretObserverA和ConcretObserverB都继承或者实现该接口。
5. 被观察者持有观察者的集合，并有通知观察者的方法。

#### 观察者模式的分类

观察者模式本身有可以成为发布订阅模式(Publish-Subscribe). 包含了两种类型，主动推送类型和自动拉取类型。

1. 推类型： 被观察者主动知道观察者需要什么样子的数据，继而发送消息给观察者，这个关系表面，观察者对被观察者对透明的。
2. 主动拉取模型: 被观察者将自身对象通过notify()传递给观察者,而观察者需要什么消息，则自动去获取。

观察者模式常用与银行等系统的监控，运维系统等内容。
