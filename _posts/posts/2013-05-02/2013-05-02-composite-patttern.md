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

