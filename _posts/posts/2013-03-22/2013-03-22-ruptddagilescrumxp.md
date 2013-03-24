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

### 敏捷软件开发模型(Agile software development)

敏捷软件开发模式是一个基于迭代开发和增量式开发模型的软件开发模式。以下是维基百科关于它的定义:
>
>Agile software development is a group of software development methods based on iterative and incremental development, where requirements and solutions evolve through collaboration between self-organizing, cross-functional teams. It promotes adaptive planning, evolutionary development and delivery, a time-boxed iterative approach, and encourages rapid and flexible response to change. It is a conceptual framework that promotes foreseen interactions throughout the development cycle.

翻译自己去执行.简单介绍一下:

>
>它是一种使自身需求通过本身的组织和团队之间的不断交叉合作尔不断演进的开发方法，它呼吁促使需要自适应的计划，演进式开发和交货。一个定时迭代。鼓励迅速而灵活的应对变化。
>

下面是一张关于这个方法的图形模型:
![图片](http://i.imgur.com/yqJTDA8.png)

### Scrum

Scrum是一种迭代式增量软件开发过程，通常用于敏捷软件开发。Scrum在英语的意思是橄榄球里的争球。
虽然Scrum是为管理软件开发项目而开发的，它同样可以用于运行软件维护团队，或者作为计划管理方法。Scrum之间的合作称为“Scrum of Scrums”

#### Scrum 的特性

crum是一个包括了一系列实践和预定义角色的过程骨架。Scrum中的主要角色包括：

1. 'Scrum Master' 是Scrum教练和团队带头人，确保团队合理的运作Scrum，并帮助团队移除实施中的障碍；
2. 产品负责人（Product Owner），确定产品的方向和愿景，定义产品发布的内容、优先级及交付时间，为产品ROI负责；
3. 开发团队（Team），一个跨职能的小团队，人数5-9人，团队拥有交付可用软件需要的各种技能。

在每一次冲刺（一个15到30天的周期，其长度由开发团队决定）当中，开发团队创建可用的（可以随时推出）软件的一个增量。每一个冲刺所要实现的功能来自产品订单（product backlog）。产品订单是按照优先级排列的要完成的工作的概要的需求，哪些订单项会被加入一次冲刺将由冲刺计划会议决定。 在会议中，产品负责人告诉开发团队他需要完成产品订单中的哪些订单项。开发团队决定在下一次冲刺中他们能够承诺完成多少订单项。[4] 在冲刺的过程中，没有人能够变更冲刺订单（sprint backlog），这意味着在一个冲刺中需求是被冻结的。
管理Scrum过程有很多实施方法，从即时贴、白板，一直到软件包。Scrum最大的好处之一是它非常容易学习，而且启动Scrum应用并不需要太多的投入。

#### Scrum中的角色

Scrum当中定义了许多角色。按照对开发过程的参与情况，这些角色被分为两组，即猪组和鸡组。这个分组方法的由来是一个关于猪和鸡合伙开餐馆的笑话[4]：
一天，一头猪和一只鸡在路上散步。鸡对猪说：“嗨，我们合伙开一家餐馆怎么样？”猪回头看了一下鸡说：“好主意，那你准备给餐馆起什么名字呢？”鸡想了想说：“叫‘火腿和鸡蛋’怎么样？”“那可不行”，猪说：“我把自己全搭进去了，而你只是参与而已。”

##### 猪组

猪是在Scrum过程中全身投入项目的各种角色，他们在项目中承担实际工作。他们有些像上边那个笑话里的猪，要把自己身上的肉贡献出来。
1. 产品负责人。产品负责人代表了客户的意愿。这保证了Scrum团队在做从业务角度来说正确的事情。产品负责人编写 用户故事，排出优先级，并放入产品订单。
2. Scrum主管（或促进者）scrum主管促进 Scrum过程，他的主要工作是去除那些影响团队交付冲刺目标的障碍。Scrum主管并非团队的领导（因为团队是自我组织的），而是一个负责屏蔽外界对开发团队的干扰的角色。Scrum主管确保Scrum过程被按照初衷使用。Scrum主管是规则的执行者。
3. 开发团队
负责交付产品的团队。一个团队通常由5至9名具有跨职能技能的人（设计者，开发者等）组成，承担实际的开发工作。

##### 鸡组

鸡并不是实际Scrum过程的一部分，但是必须考虑他们。 敏捷 方法的一个重要方面是使得用户和利益相关者参与到过程中的时间。参与每一个冲刺的评审和计划，并提供反馈对于这些人来说是非常重要的。
1. 用户软件是为了人而开发的。有人说，“假如森林里有一棵树倒下了，但没有被人听到，那么它算是发出了声音吗？”同样地，人们可以说，“假如软件没有被使用，那么它算是被开发出来了么？”
2. 利益相关者（客户，提供商）影响项目成功的人，但只直接参与冲刺评审过程。
3. 经理：为产品开发团体搭建环境的人。

#### Scrum会议

在冲刺中，每一天都会举行项目状况会议，被称为“scrum”或“每日站立会议”。每日站立会议有一些具体的指导原则：
>
> * 会议准时开始。对于迟到者团队常常会制定惩罚措施（例如罚款，做俯卧撑，在脖子上挂橡胶鸡玩具）
> * 欢迎所有人参加，但只有"猪"可以发言。
> * 不论团队规模大小，会议被限制在15分钟。
> * 所有出席者都应站立。（有助于保持会议简短）
> * 会议应在固定地点和每天的同一时间举行。
>
在会议上，每个团队成员需要回答三个问题：[4]

>
> * 今天你完成了那些工作？
> * 明天你打算做什么？
> * 完成你的目标是否存在什么障碍？（Scrum主管需要记下这些障碍）
>
每一个冲刺完成后，都会举行一次冲刺回顾会议，在会议上所有团队成员都要反思这个冲刺。举行冲刺回顾会议是为了进行持续过程改进。会议的时间限制在4小时。
Scrum提倡所有团队成员坐在一起工作，进行口头交流，以及强调项目有关的规范（disciplines），这些有助于创造自我组织的团队。
Scrum的一个关键原则是承认客户可以在项目过程中改变主意，变更他们的需求，而预测式和计划式的方法并不能轻易地解决这种不可预见的需求变化。同样，Scrum采用了经验方法– 承认问题无法完全理解或定义，而是关注于如何使得开发团队快速推出和响应不断出现的需求的能力最大化。
Scrum会议一共包含以下四种： 1） Sprint计划会议； 2） 每日站立会议； 3） 评审会议； 4） 回顾会议；

#### 自适应的项目管理

以下是一些Scrum的通用实践：

>
> * 客户成为开发团队中的一部分。（例如客户肯定对开发的结果真正感兴趣。）
> * 和所有其他形式的敏捷软件过程一样，Scrum有频繁的包含可以工作的功能的中间可交付成果。这使得客户可以更早的得到可以工作的软件，同时使得项目可以变更项目需求以适应不断变化的需求。
> * 频繁的风险和缓解计划是由开发团队自己制定。– 在每一个阶段根据承诺进行风险缓解，监测和管理（风险分析）。
> * 计划和模块开发的透明 – 让每一个人知道谁负责什么，以及什么时候完成。
> * 频繁的利益所有人会议，以跟踪项目进展 – 平衡的（发布，客户，员工，过程）仪表板更新 – 利益所有者更新 – 你必须拥有预警机制，例如提前了解可能的延迟或偏差。
> * 没有问题会被藏在地毯下。认识到或说出任何没有预见到的问题并不会受到惩罚。
> * 在工作场所和工作时间内必须全身心投入。– 完成更多的工作并不意味着需要工作更长时间。
>

Scrum开发模式通常运用与一些互联网公司，如google，twitter等就比较推崇这个开发模式。

