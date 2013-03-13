---
uri: /cs/program/ruby-block-and-proc
permalink: /cs/program/ruby-block-and-proc/index.html
layout: post
title: "ruby的Proc对象"
description: ""
[[category:]]
tags: []
---

Block是ruby的一系列依附在方法上的代码块，执行于类或者方法的上下文之间，不是对象。Proc是代码块的对象。一下有四种方法可以创建一个Proc对象
下面是ruby program对这两者区别的一个描述:

>Ruby’s blocks are chunks of code attached to a method. They operate in the context in which
they were defined. Blocks are not objects, but they can be converted into objects of class
Proc.


###   通过&符号将一个代码块传递给一个方法，例如:

```ruby

def meth1(p1, p2, &block)
puts block.inspect
end
meth1(1,2) { "a block" }
meth1(3,4)

```

执行结果如下，此时{}里面的内容传递给&block。

      #<Proc:0x0a4f4c@/tmp/prog.rb:4>
      nil

### 通过调用内置方法 Proc.new{}，创建block对象。例如:

```ruby

block = Proc.new { "a block" }
block # => #<Proc:0x0a53c0@/tmp/prog.rb:1>

```

### 通过调用内置方法Kernel.lambda，例如：

``` ruby

block = lambda { "a block" }
block # => #<Proc:0x0a53e8@/tmp/prog.rb:1 (lambda)>

```


### 通过符号->生成block对象。

```ruby
lam = >(
p1, p2) { p1 + p2 }
lam.call(4, 3) # => 7
```


