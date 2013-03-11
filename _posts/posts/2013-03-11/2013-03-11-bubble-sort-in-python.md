---
uri: /cs/porgram/python-bubble-sort
permalink: /cs/program/python-bubble-sort/index.html
layout: post
title: "python实现冒泡排序算法"
description: ""
category:
tags: []
---

## 算法描述

该算法可以将一个无序的数组看作是一列按照序列的"重量"的数据，那么重量大的应该在下面，重量轻的应该在上面，否则则交换两者的位置，做法如下:

> 1. 第一次比较相邻两个数据的大小，若l[i]>l[i+1]，则交换，否则则保持不变。
> 2. 从第二个位置及L[2...n],重复上面的过程，最后经过n-1次得到有序数据列。
>

python 的代码实现如下:

```python

def bubble_sort(source):
  for j in xrange(len(source),-1,-1):
    for i in xrange(0,j-1,1):
      if source[i]>source[i+1]:
        source[i],source[i+1] = source[i+1],source[i]
    print source

def main():
  numbers = [5,2,34,23,14,56,25,17,48]
  bubble_sort(numbers)

if __name__ == "__main__":
    main()


#numbers = [5,2,34,23,14,56,25,17,48]

```

测试输出结果如下:

    [2, 5, 23, 14, 34, 25, 17, 48, 56]
    [2, 5, 14, 23, 25, 17, 34, 48, 56]
    [2, 5, 14, 23, 17, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]
    [2, 5, 14, 17, 23, 25, 34, 48, 56]



