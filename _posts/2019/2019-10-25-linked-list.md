---
layout: post
title: 数据结构与算法之美-链表
category: note
tags: [algorithm]
keywords: algorithm
no-post-nav: true
---

## 概念及常见种类

链表与数组不同，无需连续的内存空间，而是通过指针的方式将一组零散的内存串联起来使用。常用的链表有：单链表、单向循环链表、双向链表及双向循环链表。

## 优点
- 离散的内存空间，无需大块的连续内存空间，理论上无容量限制，添加新元素无需扩容操作。
- 插入和删除操作非常快速，只有O(1)的时间复杂度。

## 缺点
- 查找元素低效，得从头遍历链表，时间复杂度最好O(1)、最坏O(n)、平均O(n)。
- 对CPU缓存不友好，没办法有效预读。
- 节点需要额外的内存空间存储指向下一个节点的指针，所以内存消耗会翻倍。而且，对链表进行频繁的插入和删除操作还会导致频繁的内存申请和释放，容易造成内存碎片。如果使用的是Java语言，就有可能会导致频繁的GC。

## 双向链表为什么比单链表高效（空间换时间）
- 对于删除给定指针指向的节点，因为单链表并不支持直接获取到节点的前驱节点，为了找到前驱节点只能从头节点开始遍历，所以单链表的时间复杂度为O(n))。而双向链表能直接获取当前节点的前驱和后继节点，时间复杂度为O(1)。同理，在给定节点之前插入一个新节点的时间复杂度也是如此。
- 对于一个有序链表，双向链表的按值查询也要比单链表高些。因为，我们可以记录上次查找的位置p，每次查找时根据要查找的值与p的大小关系，决定是往前还是往后查找，所以平均只需要查找一半的数据。

## 如何基于链表实现LRU缓存淘汰算法
维护一个有序单链表，与靠近链表尾部的节点是越早之前访问的。当有一个新的节点被访问时，我们从头节点开始遍历链表。   
1. 如果此数据之前已经被缓存到链表中了，我们遍历得到这个数据对应的节点，并将其从原来的位置删除，然后再插入到链表的头部。
2. 如果此数据没有在缓存链表中，又可以分为两种情况：
- 如果此时缓存未满，则将此节点直接插入到链表的头部。
- 如果此时缓存已满，则删除链表的尾节点，然后将此节点插入到链表的头部。

## 写链表代码需要注意的几点
- 理解引用或指针的含义。
- 警惕指针丢失和内存泄露。
- 利用哨兵简化实现难度。
- 重点留意边界条件的处理，常见的边界条件包括：1、链表为空；2、链表只要含有一个节点；3、链表只含有两个节点；4、处理链表头或尾节点时是否都能正常工作。

## leetcode练习题
题号|代码实现
:-:|:-:
206|[单链表反转](https://github.com/wyc18556/algorithms/blob/master/src/leetcode/easy/ReverseList.java)
141|[链表中环的检测](https://github.com/wyc18556/algorithms/blob/master/src/leetcode/easy/CycleList.java)
21|[合并两个有序链表](https://github.com/wyc18556/algorithms/blob/master/src/leetcode/easy/MergeList.java)
19|[删除链表的倒数第N个节点](https://github.com/wyc18556/algorithms/blob/master/src/leetcode/easy/RemoveEndOfList.java)
876|[链表的中间节点](https://github.com/wyc18556/algorithms/blob/master/src/leetcode/easy/MiddleOfList.java)