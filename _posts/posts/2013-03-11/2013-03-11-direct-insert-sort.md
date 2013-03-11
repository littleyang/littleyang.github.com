---
layout: post
title: "direct insert sort"
description: ""
category:
tags: []
---

## 直接插入排序


直接插入排序作为对有一定有序数组的高效排序方式，其主要是思路如下:假设待排序的记录存放在数组R[1..n]中。初始时，R[1]自成1个有序区，无序区为R[2..n]。从i=2起直至i=n为止，依次将R[i]插入当前的有序区R[1..i-1]中，生成含n个记录的有序区。参考一下图片说明
![图片](http://i.imgur.com/VNXZNzt.png)

## 基本步骤如下:

>1.通常将一个记录R[i]{(i=2，3，…，n-1)}到当前的有序区，使得插入后仍保证该区间里的记录是按关键字有序的操作称第i-1趟直接插入排序。<br/>
>2.排序过程的某一中间时刻，R被划分成两个子区间R[1．．i-1]（已排好序的有序区）和R[i．．n]（当前未排序的部分，可称无序区）.<br/>
>3. 直接插入排序的基本操作是将当前无序区的第1个记录R[i]插人到有序区R[1．．i-1]中适当的位置上，使R[1．．i]变为新的有序区。因为这种方法每次使有序区增加1个记录，通常称增量法。<br/>
>
>

python 代码如下:

```python
def insert_sort(source):
  for i in xrange(1,len(source)):
    num = source[i]
    j = i
    while j>0 and source[j-1]>num:
      source[j] = source[j-1]
      j = j-1
    source[j] = num
  print source
  return source

def main():
  numbers = [3,21,45,34,25,27,38,12,43,86,95]
  print numbers
  print insert_sort(numbers)

if __name__ == "__main__":
  main()

```

执行结果如下:


    [3, 21, 45, 34, 25, 27, 38, 12, 43, 86, 95]
    [3, 12, 21, 25, 27, 34, 38, 43, 45, 86, 95]
    [3, 12, 21, 25, 27, 34, 38, 43, 45, 86, 95]
