---
uri: /cs/program/ruby-flip-flop
permalink: /cs/program/ruby-flip-flop/index.html
layout: post
title: "关于ruby语言中if或者while中的范围求值问题"
description: ""
category:
tags: []
---

ruby是一个非常有意思的编程语言，与python有很多相似之处，也有很多有特点的地方，非常的灵活。其中"触发器"就是一个非常有意思的概念。翻看和google很多中文资料博客都没有对这个进行详细的解读，现在来做一个比较详细的解读.<br/>

那么什么情况你会遇到这个呢？来看下面一个表达式:

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

![ruby-flip-flop](http://i.imgur.com/qFxbVYr.png)

初始的时候，这个"触发器"的状态时关闭的(unset),当第一个表达式为true的时候，这个状态变为set,原本是(unset 输出false，set输出true)之后两点形式(..)的会直接计算最后一个表达式的真假，如果为true则整个状态为unset，此时输出为true值(这是特例),二三点形式(...)的表达式(并不直接计算最后一个表达式去确定状态机的变化，而是根据表达式的左右顺序由左到右的计算，最后计算最后一个表达式)
<br/>
因此就不难理解上面的第一个表达式:

>1.当i = 11 时候，11%4==0为false,之后状态变为:unset,但是表达式并未计算11%3,因此整个表达式为false,所以最后值为:nil
>2.当i = 12时候 12%4==0 为true,此时(..)形式直接计算12%3==0为true，此时状态机由原来的unset变为set，再变为unset，但是任然表达式的值为true,因此结果为12。
>3.当i = 13 时候,此时的状态为unset，13%4==0 为false,因此不计算13%3==0,整个表达式为false,所以值为:nill
>4.当i = 14,15 时候，与13相似
>5.当i = 16的时候,16%4==0为true，此时状态机变化为set状态，计算16%3==0为false,状态机不变化,任然是set,所以值为true,输出为16.
>6.当i = 17时，状态机为set状态，计算17%3==0 为false，状态不变化,为set，输出为true，值为17.
>7.当i = 18时，状态机任然为set状态，此时计算18%3==0为true,状态由set变为unset此时输出任然为true与12相同，值为18.
>8.当i = 19时，状态机为unset状态，计算19%4==0 为false，状态不变，因此输出false，值为nil。
>9.当i = 20时，状态机为unset状态，计算20%4==0为true，状态变化为set,计算20%3==0为false，状态不变化，任然为set,输出true，值为20


以上说明完全解释了输出结果。同理可以理解第二个表达式的输出结果形式。到此，完整的介绍了ruby的if多值范围表达式的概念，"ruby 触发器"。参考阅读[ruby programing 1.9][1],当然这里面的描述并没有那么清楚。

[1]:http://pragprog.com/book/ruby3/programming-ruby-1-9
