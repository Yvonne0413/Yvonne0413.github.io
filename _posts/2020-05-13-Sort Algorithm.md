---
layout: mypost
title: Sort Algorithm
categories: [algorithm]
---

> 动画演示：[十大排序算法](https://www.cnblogs.com/onepixel/p/7674659.html)

算法分类：
![SortAlgorithm1](./SortAlgorithm1.png)

算法概念：
 - 稳定：如果a原本在b前面，而a=b，排序之后a仍然在b的前面。
 - 不稳定：如果a原本在b的前面，而a=b，排序之后 a 可能会出现在 b 的后面。
 - 时间复杂度：对排序数据的总的操作次数。反映当n变化时，操作次数呈现什么规律。
 - 空间复杂度：是指算法在计算机内执行时所需存储空间的度量，它也是数据规模n的函数。

算法复杂度整理：
![SortAlgorithm2](./SortAlgorithm2.png)


 - [冒泡排序](#1)
 - [选择排序](#2)
 - [插入排序](#3)
 - [希尔排序](#4)
 - [归并排序](#5)
 - [快速排序](#6)
 - [堆排序](#7)
 - [计数排序](#8)
 - [桶排序](#9)
 - [基数排序](#10)
 

#### 生成随机数组
```python
import random
def random_int_list(start, stop, length):
    start, stop = (int(start), int(stop)) if start <= stop else (int(stop), int(start))
    length = int(abs(length)) if length else 0
    random_list = []
    for i in range(length):
        random_list.append(random.randint(start, stop))
    return random_list
```

#### 代码实现：

<h5 id="1"> 1. 冒泡排序：</h5>

```python
def bubble_sort(l):
    length = len(l)
    for i in range(0, length-1): # 遍历次数为length-1次
        for j in range(0, length-1-i): # 每遍历一次，最大的一个值已经到最后了，因此只交换前面的
            if l[j]>l[j+1]:  # 为了保证j+1<=length-1-i, i<lenth-1-i
                l[j], l[j+1] = l[j+1], l[j]
    return l
```
<h5 id="2"> 2. 选择排序：</h5>
选择排序是给每个位置选择当前元素最小的，比如给第一个位置选择最小的，在剩余元素里面给第二个元素选择第二小的，依次类推，直到第n -1个元素，第n个元素不用选择了，因为只剩下它一个最大的元素了。那么，在一趟选择，如果当前元素比一个元素小，而该小的元素又出现在一个和当前元素相等的元素后面，那么交换后稳定性就被破坏了。比较拗口，举个例子，序列5 8 5 2 9，我们知道第一遍选择第1个元素5会和2交换，那么原序列中2个5的相对前后顺序就被破坏了，所以选择排序不是一个稳定的排序算法。

```python
def select_sort(l):
    length = len(l)
    for i in range(0, length-1):
        minindex = i #初始化为最小
        for j in range(i+1, length):
            if (l[j]<l[minindex]):
                minindex = j
        l[i], l[minindex] = l[minindex], l[i]
    return l
```
<h5 id="3"> 3. 插入排序：</h5>

```python
def insert_sort(l):
    length = len(l)
    for i in range(0, length-1): #除了第一个已经排好序的，取后面所有length-1个数据
        cur_index = i+1
        for j in range(i, -1, -1):
            if l[cur_index]>l[j]:
                l[j+1] = l[cur_index]
                break
            else:
                l[j+1] = l[j]
    return l
```
<h5 id="3"> 3. 希尔排序：</h5>

```python
def shell_sort(l):
    length = len(l)
    gap = length//2
    while gap > 0:
        for i in range(gap, length):
            j = i
            cur = l[i]
            while (j-gap >=0 & cur<l[j-gap]):
                l[j] = l[j-gap]
                j = j-gap
            l[j] = cur
    return l
```

