---
title: Java 数据结构
date: 2019-02-12 13:47:29
categories: java
tags: java
---
# Java Data Structures

+ Queue(队列)
+ Set(无序集合)
+ List(有序集合)
+ Map(键值对集合)
+ Tree(树)

# Queue

## What is Queue ?

Queue 是一种线性结构，遵循执行操作的特定顺序。顺序是先进先出（First In Fiest Out,FIFO）,尾部添加、头部删除（先进队列的元素先出队列），跟我们生活中的排队类似。

### 队列操作

队列主要有以下四个操作:

+ Enqueue(入队) - 添加一项到队列中。如果队列已满，则称其为溢出条件。
+ Dequeue(出队) - 从队列中删除一项。剩余的这些项按顺序排列。如果队列为空，则称其为下溢条件。
+ Front - 从队列中获取最前面的项。
+ Rear - 从队列中获取最后一项。

### 队列应用

### 推荐文章

[Java 集合深入理解（9）：Queue 队列](https://blog.csdn.net/u011240877/article/details/52860924)

# Set

Set 继承于 Collection 接口，是一个不允许出现重复元素，并且无序的集合，主要 HashSet 和 TreeSet 两大实现类。

在判断重复元素的时候，Set 集合会调用 hashCode()和 equal()方法来实现。

补充：有序集合与无序集合说明

有序集合：集合里的元素可以根据 key 或 index 访问 (Map、List)

无序集合：集合里的元素只能遍历。（Set）