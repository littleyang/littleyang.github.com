---
uri: /cs/program/rails/redis-in-rails
permalink: /cs/program/rails/redis-in-rails/index.html
layout: post
title: "redis在rails中的使用"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 简要介绍

在很多时候或者最初学习与数据库相关的内容的时候，大多数的人都是从关系型的数据库开始学习的，如mysql,oracle,MSsqlserver等为最
常见的了。时间的不断的前进，技术在不断的发展。在社交网络(facebook,google,alibaba)和云计算(could)时代我们逐渐的进入了NoSql.
费关系型数据库时代。redis就是其中一种典型的费关系型存储软件。主要有一下一些特点:

1. 它是一种键值对的存储软件，所有东西都是key-value方式存储。
2. 所有的内容都直接存储到内存中，所以说计算机内存多大，它最大就能存储多少内容。
3. 可以存储的数据类型为：字符的，基本数据类型的，数组的，键值对，hash，set等。
4. 它是开源的。
…………

更多的详细的可以去参考官方的文档，说明。![这个是网址](http://www.redis.io/)。接下来就看看实际的使用吧。


### 简单的说说它的应用场景吧

比如你有一个社交网络方面的应用，用户关系，用户表的数据量非常发大，他们之间的follow与friend关系，不再是直接把关系标志标记在表中，而是通过redis键值对存入内存中，然后直接中内存中读取，然后再根据所得ID直接去读取用户。这样就减少了直接对数据库的查询
次数，从而提高了性能。可以看看下面这个图。

![picture](http://i.imgur.com/e9ddkvv.png)

### redis的安装

1. 下载源码包，或者直接通过相应的包管理软件去自动安装(HomeBrew,apt-get等)，网址: http://www.redis.io/download
2. 执行以下的代码和步骤直接ok
3. 启动服务即可
```
$ wget http://redis.googlecode.com/files/redis-2.6.13.tar.gz
$ tar xzf redis-2.6.13.tar.gz
$ cd redis-2.6.13
$ make
$ src/redis-server
```

### redis在rails中的设置

这里会有很多的相关的信息可以再互联网上搜索到，
![这个](http://jimneath.org/2011/03/24/using-redis-with-ruby-on-rails.html)是一个一个老外写的，我想是非常详细的一个了。
国内有些程序员把它翻译过来了的，如![这个](http://www.jokry.com/articles/5a4fd1f6)。___ 需要说明的一点是___:
这个文字里面的内容已经非常老了，这里面的redis-rb版本问2.1.1,最新的应该是3以上的了，所以参考的时候请注意吧。可能会出现
一个叫做old argument syntax的一个错误(如果按照连接里面的参考).
一下是具体的时间步骤：

1. 安装redis的ruby客户端.在Gemfile中添加一下代码

```
gem 'redis'

```
2. 执行bundle install自动安装需要的gem包
3. 在整个rails app中需要有一个关于redis的全局变量来调用存储接口，因此可以再app/config/initializers/下面建立一个初始化
redis的文件，redis.rb.并加入一下代码解析reids的配置

````
## Location, config/initializers/redis.rb

config_file = File.join('config','redis.yml')

$redis = if File.exists?(config_file)
           conf = YAML.load(File.read(config_file))
           conf[Rails.env.to_s].blank? ? Redis.new : Redis.new(conf[Rails.env.to_s])
         else
           Redis.new
         end
```

简单的说明一下上面的代码,上面读取了一个redis的配置文件，配置文件的内容与其他数据库配置文件一样。初始化一个$redis的全局变量
这样就可以直接使用在rails中调用$redis变量来存储。

4. 测试如下:

```
rails c

Loading development environment (Rails 3.2.8)
1.9.3-p194 :001 > $redis
=> #<Redis client v3.0.4 for redis://127.0.0.1:6379/0>
1.9.3-p194 :002 >

```

### 下面通过具体的rails model的Contact类来说明rails中redis的使用

1. 在rails中新建一个model Contacter

```
rails g model contacter name:string
```

2. 执行数据迁移任务,创建必要的数据表

```
rake db:migrate

```

3. 分别创建两个Contacter对象，存入到数据库中。在rails console中执行一下代码:

```
%w[Alfred Bob].each{|name| Contacter.create(:name => name)}

Loading development environment (Rails 3.2.8)
1.9.3-p194 :001 > %w[Alfred Bob].each{|name| Contacter.create(:name => name)}
   (0.1ms)  begin transaction
SQL (47.8ms)  INSERT INTO "contacters" ("created_at", "name", "updated_at") VALUES (?, ?, ?)  [["created_at", Thu, 20
   Jun 2013 06:22:17 UTC +00:00], ["name", "Alfred"], ["updated_at", Thu, 20 Jun 2013 06:22:17 UTC +00:00]](11.7ms)
   commit transaction(0.1ms)  begin transaction
SQL (0.4ms)  INSERT INTO "contacters" ("created_at", "name", "updated_at") VALUES (?, ?, ?)  [["created_at", Thu, 20
      Jun 2013 06:22:17 UTC +00:00], ["name", "Bob"], ["updated_at", Thu, 20 Jun 2013 06:22:17 UTC +00:00]](5.7ms)
      commit transaction => ["Alfred", "Bob"]
```

4. 在contacter model加入一下的代码:

```
def contact!(user)
  $redis.multi do
    $redis.sadd(self.redis_key(:following),user.id)
      $redis.sadd(user.redis_key(:followers),self.id)
  end
end

def uncontact!(user)
  $redis.multi do
     $redis.srem(self.redis_key(:following),user.id)
     $redis.srem(user.redis_key(:followers),self.id)
  end
end

def redis_key(str)
   "user:#{self.id}:#{str}"
end
```

4. 相关的操作，让他们通过redis关联起来。结果如下:

```
Loading development environment (Rails 3.2.8)
1.9.3-p194 :001 > a,b = Contacter.all
  Contacter Load (0.1ms)  SELECT "contacters".* FROM "contacters"
=> [#<Contacter id: 1, name: "Alfred", created_at: "2013-06-20 06:22:17", updated_at: "2013-06-20 06:22:17">,
    #<Contacterid: 2, name: "Bob", created_at: "2013-06-20 06:22:17", updated_at: "2013-06-20 06:22:17">]
1.9.3-p194 :002 > a.contact!(b)
=> [false, false]
1.9.3-p194 :003 >

```
以上就是整个简单的过程和配置





