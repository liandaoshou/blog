---
layout: post
title:  "Java 公平锁和非公平锁"
date:   2017-03-18 10:05:01 +0800
categories: Java Fair Lock
tag: Java
---

## Java非公平锁

JVM 按随机就近原则分配锁的机制称为不公平锁，ReentrantLock 在构造函数中提供了是否公平锁初始化的方式，默认为非公平锁。
非公平锁执行效率远远超于公平锁，除非程序又特殊需要，否则最常用非公平锁的分配机制。

## Java公平锁

公平锁指定锁分配机制是公平的，通常先对锁提出获取请求的线程会先被分配到锁，ReentrantLock在构造函数中提供了是否公平锁的初始化方法来定义公平锁。


## ReentrantLock 与 synchronized

1. ReentrantLock 通过方法lock()与unlock()来进行加锁与解锁操作，与synchronized会被JVM自动解锁机制不同，ReentrantLock加锁后需要手动进行解锁。
为了避免程序出现异常无法正常解锁的情况，使用ReentrantLock必须在finally控制模块中进行解锁操作。

2. ReentrantLock相比synchronized优势是可以中断，公平锁，多个锁。

