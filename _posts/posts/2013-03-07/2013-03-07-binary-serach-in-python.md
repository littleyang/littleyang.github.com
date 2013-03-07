---
layout: post
title: "python的二分查找算法"
description: ""
category:
tags: []
---

对于任意一个数组，查找其中的某个元素，简单的几个步骤如下

    1,通过对数组进行排序，形成有序数组。
    2,实现二分查找方法，调用方法

下面是一个简单的实例，代码已经执行效果如下：

```python

numbers = [1,25,4,6,7,8,9,12,34,63,87,46,23,16,43,37,65,68,78,88,96]
def binary_search(dest,source):
  start = 0
  end = len(source)
  index = 0
  while True:
    index = start + ((end - start)/2)
    if source[index] > dest:
      end = index
    if source[index] < dest:
      start = index
    if source[index] == dest:
      print " the num %d index is %d" % (dest,index)
      break

def quick_sort(source,low =0,high = None):
  if high == None:
    high = len(source)-1
  if low < high:
    s,i,j = source[low],low,high
    while i<j:
      while i<j and source[j] >= s:
        j = j -1
      if i < j:
        source[i] = source[j]
        i = i+1
      while i<j and source[i] <= s:
        i = i+1
      if i<j:
        source[j] = source[i]
        j = j - 1
      source[i] = s
      quick_sort(source, low, i - 1)
      quick_sort(source, i + 1, high)
  return source

def show_result():
  data = quick_sort(numbers)
  print data
  binary_search(37,data)

show_result()
```

运行结果如下:(这里有个小小的提示，计算机的数组计数从0开始，很多时候都忘记了以为程序出错了!汗)

    [1, 4, 6, 7, 8, 9, 12, 16, 23, 25, 34, 37, 43, 46, 63, 65, 68, 78, 87, 88, 96]
     the num 37 index is 11

-------

### 1、简单的介绍一下快速排序和二分查找算法

1.快速排序

快速排序又称分治排序，快速排序的几个基本步骤，其主要思想是：分而处理，合而用之。即是说：先把数组分为两个部分，以某一个参考为支点，左边的数据均小于该支点，右边的数据均大于该支点，然后分别对两端进行递归调用。

    其主要步骤包括以下:</br>
      1.找出支点，分割数据
      2.递归调用
      3.组合数据

2.二分查找

这个同样是将已经有序的数据分为两部分，一般以中间位分割，然后再比较两端与目标数据的大小。






