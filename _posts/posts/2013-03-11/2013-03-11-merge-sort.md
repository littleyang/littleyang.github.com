---
uri: /cs/program/python-merge-sort
permalink : /cs/program/python-merge-sort/index.html
layout: post
title: "python 归并排序"
description: ""
category:
tags: []
---

## 算法描述

归并排序需要一个与原来数组相等的辅助数组，其主要思想就是：将数组(source)分割排序为一段段的有序数组，然后再合并到一起组成新的数组，从而达到排序的目的。其主要步骤如下：

>
> 1. 新建一个与source相同大小的参考数组L，设定一个索引index.
> 2. 分别比较source数组的划分为两个子序列，分别以i,j作为索引.
> 3.实现归并复制合并时依次比较R[i]和R[j]的关键字，取关键字较小的记录复制到R1[p]中，然后将被复制记录的指针i或j加1，以及指向复制位置的指针p加1。
> 4.重复这一过程直至两个输入的子文件有一个已全部复制完毕(不妨称其为空)，此时将另一非空的子文件中剩余记录依次复制到R1中即可。
>
>

```python
def mergesort(L):
  print "before: ", L
  if len(L)<2:
    return L[:]
  else:
    middle = len(L)/2

    left = mergesort(L[:middle])
    right = mergesort(L[middle:])
    together = merge(left,right)
    print "left: " , left
    print "right: ", right
    print "together: ",together
    return together


def merge(left,right):
  result = []
  i,j = 0,0
  while i<len(left) and j<len(right):
    if left[i]<=right[j]:
      result.append(left[i])
      i= i+1
    else:
      result.append(right[j])
      j= j+1

  while i<len(left):
    result.append(left[i])
    i=i+1

  while j<len(right):
    result.append(right[j])
    j=j+1
  return result

def main():
  numbers = [3,5,28,2,45,34,67,13,23]
  mergesort(numbers)

if __name__ == "__main__":
  main()

```

输出结果为:

    该结果详细的显示了执行过程:


    before:  [3, 5, 28, 2, 45, 34, 67, 13, 23]
    before:  [3, 5, 28, 2]
    before:  [3, 5]
    before:  [3]
    before:  [5]
    left:  [3]
    right:  [5]
    together:  [3, 5]
    before:  [28, 2]
    before:  [28]
    before:  [2]
    left:  [28]
    right:  [2]
    together:  [2, 28]
    left:  [3, 5]
    right:  [2, 28]
    together:  [2, 3, 5, 28]
    before:  [45, 34, 67, 13, 23]
    before:  [45, 34]
    before:  [45]
    before:  [34]
    left:  [45]
    right:  [34]
    together:  [34, 45]
    before:  [67, 13, 23]
    before:  [67]
    before:  [13, 23]
    before:  [13]
    before:  [23]
    left:  [13]
    right:  [23]
    together:  [13, 23]
    left:  [67]
    right:  [13, 23]
    together:  [13, 23, 67]
    left:  [34, 45]
    right:  [13, 23, 67]
    together:  [13, 23, 34, 45, 67]
    left:  [2, 3, 5, 28]
    right:  [13, 23, 34, 45, 67]
    together:  [2, 3, 5, 13, 23, 28, 34, 45, 67]


