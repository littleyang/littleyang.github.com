---
uri: /cs/program/ruby-singletons
permalink: /cs/program/ruby-singletons/index.html
layout: post
title: "ruby 对象的单例模式"
description: ""
category:
tags: []
---

## 什么是单例模式呢？(singleton)

单，就是孤单，唯一的！在Java里面，表示只有一个对象。当然，这个也是在其他的面向对象的语言里面也是完全能够通用的！在ruby当中，也可以这么理解，类是本身类的一个实例的实现。也就是说单例的类是来自于一个类的实例创建的对象。

### ruby中动态方法调用的路径

现在先来看看下面这段代码，代码其实很简单，主要是为了说明方法调用的路径问题。

```ruby
foo = Array.new
foo.class #=>Array
foo.size #=>0
```

以上，foo为方法class,size的接收者(receiver),首先解释器会(interpreter,Java中叫做虚拟机,JVM)找到foo的klass,指向Array,然后去寻找Class Array 中是否有size这个方法(method),如果有，则直接调用;如果没有则继续上溯寻找到期父类(father class),直到最终的Object,如果都没有找到，则直接调用NotFindMethod输出错误信息,那么这里就会有个问题，既然多继承可以存,ruby中有mixins的功能，因此如果其他模块有这个方法呢？这个问题叫diamond Problem。ruby是靠先来后到的原则，即是说先遇到谁就调用谁。可以参考以下图片:

![picture](http://i.imgur.com/NtsqR9I.png)

### 单例方法

顾名思义,单例方法那么就是说这个方法只能是属于这个具体的实例，别的具有相同类的实例(也就是从相同Class实例化而来的)不具有这个方法。可以看看下面这个代码:

```ruby
foobar = Array.new

def foobar.size
  "Hello World!"
end

foobar.size  # => "Hello World!"
foobar.class # => Array

bizbat = Array.new
bizbat.size  # => 0

```

其中foobar.size为单例方法。通过该形式定义单例方法。这是一个非常有意思的定义方法的形式，可以指定一个接受对象，非常的灵活。
这个size的方法值存在于foobar这个实例中，而其他的instance不具有这个方法只是从Array中带来的方法，这个就是一个singleton。
这个当中，有一个匿名类singleton class 被插入到 foobar这个实例化，然后再他的superclass 指向Array中,可以参考下面的图片来说明:

![picture](http://i.imgur.com/MyxKoHL.png)

### 实现singleton的一些方法

#### 1.从modules中实现sintleton,参考如下的代码:

```ruby
module Foo
  def foo
  "Hello World!"
  end
end

foobar = []
foobar.extend(Foo)
foobar.singleton_methods # => ["foo"]
```

#### 2.直接实现singleton class，代码如下:

```ruby
foobar = []

class << foobar
  def foo
    "Hello World!"
  end
end

foobar.singleton_methods # => ["foo"]

```
#### 我们也可以使用类方法来实现singleton.

```ruby
class Foo
  def self.one ()
    1
  end

  class << self
    def two ()
      2
    end
  end

  def three ()
    3
  end

  self.singleton_methods # => ["two", "one"]
  self.class             # => Class
  self                   # => Foo
end
```
singleton 模式来说，就是整个application中只有那么一个对象，很容易出现不知道的错误，因此如果没有特殊必要，最好少用singleton

