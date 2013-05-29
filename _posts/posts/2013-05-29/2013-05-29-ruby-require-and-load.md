---
uri: /cs/program/ruby/require-and-load
permalink: /cs/program/ruby/require-and-load/index.html
layout: post
title: "【转载】如何山寨ruby require和load开看看他们的区别"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 酱油

要看看两者之间的区别，除了直接看源代码之外，那么我们还可以来模拟他们以加深理解

#### 假设我们有一个 person.rb 文件，内容如下:

```ruby
# -*- coding: utf-8 -*-
# person.rb
class Person
  attr_reader :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def to_s
    "My name is #{name} and I'm #{age} years old!"
  end

end

person = Person.new("金将军", 30)
puts person.to_s

```

#### 先来山寨 load

```ruby
# -*- coding: utf-8 -*-
# try_load_require.rb

load './person.rb'
load './person.rb'

```

结果为:

```
$ ruby try_load_require.rb
My name is 金将军 and I'm 30 years old!
My name is 金将军 and I'm 30 years old!

```

我们这里调用了 两次 load ，发现 person.rb 被调用了两次。这说明 load是不会判断文件是否已经加载，
只是简单的加载并运行了内容。换言之我们可以自己山寨一个 load 方法来达到同样的目的：

```ruby
# -*- coding: utf-8 -*-
# try_load_require.rb

def load(file_with_path)
  puts "这是山寨load()"
    eval File.read(file_with_path)
  end
load './person.rb'
load './person.rb'
```

```ruby
def load(file_with_path, warp = false)
  puts "这是山寨load()"
  if warp
    Module.new.module_eval(File.read(file_with_path))
  else
    eval File.read(file_with_path)
  end
  true
end
```

#### 接下来山寨 require

用同样的方法我们来测试一下 require

```ruby

# -*- coding: utf-8 -*-
# try_load_require.rb

require './person.rb' #=> true
require './person.rb' #=> false

```

而输出结果是：

```
$ ruby try_load_require.rb
My name is 金将军 and I'm 30 years old!

```

这说明 require 是会判断文件是否已经被加载，如果被加载的话是不会再进行重复加载的。并且第一次加载成功会返回true，
如果判断为重复加载会返回 false。知道这个简单的规则后，我们就可以做如下山寨了并且会用到我们刚刚的山寨 load 哟 :)

```ruby

$required_files = []

def require(file_with_path)
  puts "这是山寨require()"
  full_path = File.expand_path(file_with_path)
  if $required_files.include?(full_path)
    return false
  else
    $required_files << full_path
    load(full_path)
    return true
  end
end

```

那什么时候用 load 什么时候用 require 呢？在大多数情况下我们都是使用 require 的。但是有些时候需要多次加载一个变化的文件，
比如像 Rails 的 development 模式的 server 启起来以后，需要再次加载改变的源文件那么就需要用到 load (或者 autoload,
 以后会谈到)。


