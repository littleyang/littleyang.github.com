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


### 代理模式实例

### 动态代理(Dynamic proxy)


