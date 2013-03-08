---
uri: /cs/program/ruby-flip-flop
permalink: /cs/program/ruby-flip-flop/index.html
layout: post
title: "关于ruby语言中if或者while中的范围求值问题"
description: ""
category:
tags: []
---

ruby是一个非常有意思的编程语言，与python有很多相似之处，也有很多有特点的地方，非常的灵活。其中"触发器"就是一个非常有意思的概念。那么什么情况你会遇到这个呢？来看下面一个表达式:

```ruby
12%4==0..16%3==0?4:3
```

仔细观察一下这个表达式，就会很有意思:12对4模运算，16对3模运算，然后中间有一个范围表达式(..)，这个是不是很奇特呢？那么再来看一个表达式:

```ruby
12%4==0...16%3==0?4:3
```

这个表达式与前面的一个唯一的一点区别就是:模运算之后的结果在求值范围是三个点(...)。当然，其运算结果也是有所不同的。以上两个表达式输出的结果是一直的，都是:

    4


好，到此为止，也许就会有疑问:为什么会一样呢？不着急，再来看看下面的两个表达式的运算结果:

```ruby
a =(11..20).collect{|i| (i%4==0)..(i%3==0)?i:nil}
```

结果为:

    [nil, 12, nil, nil, nil, 16, 17, 18, nil, 20]

```ruby
a =(11..20).collect{|i| (i%4==0)...(i%3==0)?i:nil}
```

结果为:
    [nil, 12, 13, 14, 15, 16, 17, 18, nil, 20]

以上两个对比看出明显就有很大的差别。这里有一段关于这个问题的英文描述比较准确的:

>The flip-flop expression will evaluate to false until the first (left hand) expression is true. The flip-flop expression will then evaluate to true until the right-hand expression evaluates to true. It will then continue to evaluate to false until the left-hand expression evaluates to true again, and then it will flip the other way. It flips and flops between the true and false state, hence the name "flip-flop."

英文比较好的可以自己去理解，就不做翻译了。那么如何理解上面的结果了，先看看下面这个图:

![ruby-flip-flop][/~/image/flip-flop.png]


