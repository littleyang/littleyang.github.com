---
uri: /cs/program/software-development
permalink: /cs/program/software-development/index.html
layout: post
title: "软件开发中的各种模型的简介"
description: ""
category:
tags: []
---
{% include JB/setup %}

## 概述

如果你去实习，或者已经工作了的。那么你在工作中很多时候都可能回听到有人会说开发方法，开发流程什么的。那么我门通常所使用的开发流程到底有哪些呢？常用的。这些都是由那些经验丰富的工程师(俗称码农)的各种经验的总结。当然这些应用环境可能根据公司规模，项目参与人数多少都会有些变化，甚至你可能会遇到根本不使用的时候，好吧。不废话了。先来例举一下主要常用的模式吧:

1. RUP[(The Rational Unified Process)][RUP]
2. TDD[(Test Driven Development)][TDD]
3. Agile[(快速开发)][Agile]
4. Scrum[(温和开发同样也是快速开发的一种模型)][Scrum]
5. XP[(Extreme Programming,极限编程)][XP]
[XP]:http://en.wikipedia.org/wiki/Extreme_programming
[Scrum]:http://zh.wikipedia.org/wiki/Scrum
[Agile]:http://en.wikipedia.org/wiki/Agile_software_development
[TDD]:http://zh.wikipedia.org/wiki/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91
[RUP]:http://www.ambysoft.com/downloads/managersIntroToRUP.pdf

以上都是对软件开发过程模型的一个概要的总结，那么下面来分个介绍。

### RUP,统一开发过程理论

这是出自于IBM软件开发体系的一个理论模型，当然IBM也在使用这种开发模型。是一套以文为基础的开发模式。该模型中强调在开发过程中需要遵守一定的开发流程，为了按照需求开发出高质量的软件产品(大多数时候，需求都会由圆变为椭圆，这个待会再说)。为了适用各种开发场景，这种开发模型通常都是可定制性的，即是:任何的组织或者企业，个人都可以根据不同的需求开发出符合自己需求的流程。通常都会具有一下不分的内容:

> ***1. 角色***:定义了在开发过程中对项目负责的人或者开发小组。
>
> ***2. 活动***:在开发过程中，各种角色所从事的各种各种工作，行动等。
>
> ***3. 开发对象(工件)和开发对象资源(工件集):***
>
> > 1. 工件: 也就是你的客户需要的东西，直接操作对象就是工件，整个流程中的工作产品。角色(人)使用工件尽兴活动。并在执行活动中生产和完善工件，可以是文档，计划书等内容。
> > 2. 工件集:也就是上面所说的工件的一个集合，一组工件。
>
> ***4. 模板***:模板就是工件的模型。
>
> ***5. 工作流程***:是一系列有这一定顺序的活动组成。通常我们可以使用活动图来表示.
>     图中的每一步都详细的规定了每个角色的每个活动，进行生产什么样子的工件。

### AUP 最佳实践包括的内容以及模型在这个实践中是怎么工作的

所有的一切，包括快速开发模型(Aglie Modeling)按照工作流程主要分为迭代(Iterative)和增量式(Incremental)模式。

> #### 快速迭代开发(Aligle Unifiled Porgress)
> 在RUP，每一代软件产品都要经历四个阶段:起始，精细，架构构建，产品化。一下图片是整个迭代开发的生命周期(lifecycle):
> ![图片](http://i.imgur.com/PjphA1s.gif)
> #### 企业级的RUP(Enterprise Rational Unifiled Progress)
> 在整个开发流程中包括了两个阶段六个过程，Development(产品开发阶段)和Support(产品后期支持维护等)。Business Modeling(初期业务模型构建)，Requirement(需求建立)，Analysis & Design(分析与设计)，Model(产品模型化)，Enterprise Business Modeling(企业级业务建模)，Enterprise Architecture(产品迭代开发)。其整个生命周期可以参考如下图片:
> ![图片](http://i.imgur.com/GPjsTHR.png)
> #### RUP的核心流程
> 在RUP中详细的规定了一下的流程内容:业务建模,需求，设计分析，实施，测试，部署，配置和变更管理，项目管理和环境搭建。对于每一个流程都给出了详细的流程细图，详细的说明了每一个活动所需要参与的角色，所需要模型和生产工件。
>

### 极限编程(XP)

极限编程是一种过程化的编程，这是个很奇葩的理论。它没有对整个软件开发过程有着严格儿繁琐的规定，而是一套在实际开发中所需要遵守的原则。没有强调复杂儿繁琐的过程和文档，可以说XP是一个非常轻量级的开发理论，小巧而精悍 。适合小团队作战。但是XP非常强调客户的作用，其目的就是满足与需求。一下是其几个基本的简单的要求。

>
> 1. 提高团队的沟通
> 2. 以最简单的方法设计和编程
> 3. 从最终用户那里得到持续的反馈
> 4. 在整个开发过程中保持团队的士气和勇气。
>

现代的软件开发过程中任何都是保持这不断变化的。客户的需求随时都有可能更改，XP模型需要整个团队保持这种变化，以适应不断变化的需求。当然，这是个无底洞！以下的图片是XP模型的解释:
![图片](http://i.imgur.com/ZcWiFD2.png)
![图片](http://i.imgur.com/eKeiPEQ.png)

### 测试驱动开发(TDD,Test Driven Development)

TDD是另一种形式的极限编程开发方法。是在开发之前先写测试程序，然后在编码实现所需要的功能，测试驱动开发是戴两顶帽子思考的开发方式：先戴上实现功能的帽子，在测试的辅助下，快速实现其功能；再戴上重构的帽子，在测试的保护下，通过去除冗余的代码，提高代码质量。测试驱动着整个开发过程：首先，驱动代码的设计和功能的实现；其后，驱动代码的再设计和重构。其最为著名的就是Ruby on Rails 的测试,Rspec的测试模型。当然这些有利之处表现在哪里呢？

>
> 1. 可以有效的避免过度设计带来的浪费。但是也有人强调在开发前需要有完整的设计再实施可以有效的避免重构带来的浪费。
> 2. 可以让开发者在开发中拥有更全面的视角，避免过度实现带来的浪费。
>

当然有利就必有弊:

>
> 1.开发者可能只完成满足了测试的代码，而忽略了对实际需求的实现。有实践者认为用结对编程的方式可以有效的避免这个问题。
> 2.会放慢开发实际代码的速度，特别对于要求开发速度的原型开发造成不利。
> 3.对于GUI,资料库和Web应用而言。构造单元测试比较困难，如果强行构造单元测试，反而给维护带来额外的工作量。
> 4.使得开发更为关注用例和测试案例，而不是设计本身。
> 我个人观点也不太喜欢这种开发模式。
>

一下是一段关于TDD的网上调查结果已经分析:

>Test Driven Development (30%)
>TDD is actually a very popular methodology. It involves using testing to continually drive the next step in the agile development process. Each short development cycle involves the creation of automated unit tests that can be implemented over and over to ensure that the software continues to perform properly as it evolves.
>
>Benefits: QA and documentation are built into the development process. The concept is simple to understand and implement: Test until failure, make changes until the unit passes, remove redundancies in the code, repeat.
>
>Drawbacks: Could be bad for morale over the long term since it focuses on forcing failure and fixing what’s wrong. May lose focus on the big picture unless the end purpose of the code is kept in mind.
>
>Applications: Appropriate when you need software that’s loosely coupled and easy to maintain. Good for speedy development with fewer bugs. Works best for team members who have a perfectionist or “fixit” attitude and like dealing with details.
>
>
