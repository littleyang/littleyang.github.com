---
uri: /cs/program/python-exercise
permalink: /cs/program/python-exercise/index.html
layout: post
title: "一个关于python的文件文字处理测试"
description: ""
category:
tags: []
---

问题描述如下:将下面这段文字中的注释已经空行去掉，并按照文字多少排序后输出到result文件中。

> #some words
  Sometimes in life,
  You find a special friend;
  Someone who changes your life just by being part of it.
  Someone who makes you laugh until you can't stop;
  Someone who makes you believe that there really is good in the world.
  Someone who convinces you that there really is an unlocked door just waiting for you to open it.

  This is Forever Friendship.
  when you're down,and the world seems dark and empty,
  Your forever friend lifts you up in spirits and makes that dark and empty world
  suddenly seem bright and full.
  Your forever friend gets you through the hard times,the sad times,and the confused times.
  If you turn and walk away,
  Your forever friend follows,
  If you lose you way,
  Your forever friend guides you and cheers you on.
  Your forever friend holds your hand and tells you that everything is going to be okay.

测试代码已经执行结果如下:

```python

read_file = open("test.txt")
file_list = []
try:
  for line in read_file.readlines():
    line = line.strip()
    if not len(line) or line.startswith('#'):
      continue
    file_list.append(line)
finally:
  read_file.close()
file_list.sort()
open('result_test.txt','w').write('%s' % '\n'.join(file_list))
#print file_list
```

执行结果如下:

```
If you lose you way,
If you turn and walk away,
Someone who changes your life just by being part of it.
Someone who convinces you that there really is an unlocked door just waiting for you to open it.
Someone who makes you believe that there really is good in the world.
Someone who makes you laugh until you can't stop;
Sometimes in life,
This is Forever Friendship.
You find a special friend;
Your forever friend follows,
Your forever friend gets you through the hard times,the sad times,and the confused times.
Your forever friend guides you and cheers you on.
Your forever friend holds your hand and tells you that everything is going to be okay.
Your forever friend lifts you up in spirits and makes that dark and empty world
suddenly seem bright and full.
when you're down,and the world seems dark and empty,
```
