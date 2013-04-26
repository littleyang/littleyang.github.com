---
uri: /cs/program/java/collection
permalink: /cs/program/java/collection/index.html
layout: post
title: "Java 泛型与集合(集合,Collection Framework)"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 简要概述

Java集合类是包含了一系列数据结构以及操作方法的集合，其很多的思想都来源于C++的部分。这个框架的引入极大的提高的工作效率。
非常的方便。collection framework主要包含了一下三种的数据结构集合:

1. List,继承于Collection 接口，可以包含重复的元素，按照插入顺序排序，无重新排序。
2. Sets,继承于Collection 接口，不允许重复，元素的顺序按照仪的规则排序。
3. Maps,Map是一组键值对对象，key不允许重复，值可以有重复的。

可以参考下面的两个图片，详细的介绍了集合的类的组成以及他们的层次结构。

![Imgur](http://i.imgur.com/93VBY1v)
![Imgur](http://i.imgur.com/oxtFMPd)

下面开始详细的介绍他们，一些简单的示例代码。

-----

### List和Sets的分析介绍。

#### List接口

List接口继承了Collection接口，是一个允许存在重复元素的容器。list有特点的顺序用于存储元素，每次取出来的数据操作之后返回的
结果有可能顺序不同。实现List的类有，ArrayList,LinkedList,Vector等.

1. List(interface),顺序作为list最重要的一个特点，List为Collection添加了很多操作元素的方法。包括插入，查找，删除，移动等
操作。
2. ArrayList作为List的一个具体实现类，其特点是:数据结构由数组实现，对于随机的元素访问，速度较快。但是向其中插入元素，稍微
显得缓慢。
3. LinkedList作为list的另外一个具体实现，其特点是: 数据结构为链表，每个元素都有一个后继和前驱(首尾除外)，这个使得向其中
插入元素，显得快速了很多。很多时候都当做一个队列来使用。


在“集合框架”中有两种常规的 List 实现：ArrayList 和 LinkedList。使用两种 List 实的哪一种取决于您特定的需要。如果要支持随机访问，而不必在除尾部的任何位置插入或除去元素，那么，ArrayList 提供了可选的集合。但如果，您要频繁的从列表的中间位置添加和除去元素，而只要顺序的访问列表元素，那么，LinkedList 实现更好。

#### Set接口

Set 接口也是继承于Collection的，但是不允许存在重复的元素。其具体实现有HashSet和TreeSet。HashSet并没有保障元素的顺序，对
元素的操作可以实现快速的存取。TreeSet中元素是具有一定顺序的，使用树来存储元素，保障元素的一定的顺序。LinkedHashSet,
从名字上看就知道其结构上有链表的影子，同时也具有hash的速度。Set需要维护元素的顺序，因此需要实现Comparable接口和CompareTo()
方法。

### Maps 的分析介绍

Map接口用于维护键/值对(key/value pairs)。该接口描述了从不重复的键到值的映射。

1. Map接口常用的实现类有：HashMap 和TreeMap。
2. HashMap类使用散列表实现Map接口。散列映射并不保证它的元素的顺序。因此，元素加入散列映射的顺序并不一定是它们被迭代函数
读出的顺序。
3. TreeMap类通过使用树实现Map接口。
TreeMap提供了按排序顺序存储关键字/值对的有效手段，同时允许快速检索。应该注意的是，不像散列映射，树映射保证它的元素按照关键字升序排序。
说明：Map用 put(k,v) / get(k)，还可以使用containsKey()/containsValue()来检查其中是否含有某个key/value。
HashMap用于快速查找。在Map接口中，HashMap用的比较多，如果需要对集合中的元素进行排序,
才可以用TreeMap，不需要排序就用HashMap。
4. 重写HashCode()方法。

### Iterator 介绍分析。

Collection 接口的iterator()方法返回一个 Iterator。
Iterator接口方法能以迭代方式逐个访问集合中各个元素，并安全的从Collection 中除去适当的元素。
迭代器是一种设计模式，它是一个对象，它可以遍历并选择序列中的对象，而开发人员不需要了解该序列的底层结构。迭代器通常被称为“轻量级”对象，因为创建它的代价小。
Java中的Iterator功能比较简单，并且只能单向移动:i

1. 使用方法iterator()要求容器返回一个Iterator。第一次调用Iterator的next()方法时，它返回序列的第一个元素。
2. 使用next()获得序列中的下一个元素。
3. 使用hasNext()检查序列中是否还有元素。
4. 使用remove()将迭代器新返回的元素删除。 Iterator是Java迭代器最简单的实现，
为List设计的ListIterator具有更多的功能， 它可以从两个方向遍历List，也可以从List中插入和删除元素。
“Iterator中删除操作对底层Collection也有影响。”迭代器是 故障快速修复 （fail-fast）的。
这意味着，当另一个线程修改底层集合的时候，如果您正在用 Iterator 遍历集合，那么，Iterator就会抛出 ConcurrentModificationException （另 一种 RuntimeException异常）异常并立刻失败

#### 下面是关于集合类的比较表

![picture](http://imgur.com/5AsWh7u)


