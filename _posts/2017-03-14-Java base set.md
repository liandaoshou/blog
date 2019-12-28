---
layout: post
title:  "Java基础-集合"
date:   2017-03-14 09:57:09 +0800
categories: Java Base Set
tag: Java
---

# Java集合

## 接口继承关系和实现
    
    集合类存放于Java.util包中，主要有3种：set（集）、list（列表包含Queue）和map（映射）。
    
    1. Collection : Collection 是集合List、Set、Queue的最基本的接口。
    2. Iterator： 迭代器，可以通过迭代器遍历集合中的数据。
    3. Map： 是映射表的基础接口

![Java基础-集合](/images/posts/20170314/01.png)<br>


## List

Java的List是常用的数据类型。List是有序的集合，Java List一共三个实现类，分别是ArrayList、Vector和LinkedList。

### ArrayList（数组）

ArrayList 是最常用的List实现类，内部通过数组实现，它允许对元素进行快速随机访问。数组的缺点是每个元素间不能有间隔，当数组大小不满足时需要增加存储能力，就要将已有的数据复制到新的存储空间中。
当ArrayList的中间位置插入或者删除元素时，需要对数组进行复制，移动。因此适合随机查找和变例，并不适合插入和删除。

### Vector (数组实现，线程同步)

Vector 和 ArrayList一样，通过数组实现的，不同的是它支持线程同步，即某一刻只有一个线程能够写Vector，避免多线程同时写引起的不一致性，但实现同步需要很高的花费，因此访问比ArrayList慢。

### LinkList （链表）

LinkedList 使用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和便利速度比较慢，另外提供List接口中没有定义的方法，专门用于操作表头和表尾，可以当作堆、栈、队列和双向队列使用。
