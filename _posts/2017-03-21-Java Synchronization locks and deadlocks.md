---
layout: post
title:  "Java 同步锁与死锁"
date:   2017-03-21 15:59:00 +0800
categories: Java synchronization locks and deadlocks
tag: Java
---

## 同步锁

当多个线程同时访问同一个数据时，很容易出现问题。为了避免这种情况出现，我们要保证线程同步互斥，就是指并发执行的多个线程，同一时间内只允许一个线程访问共享数据。
Java中可以使用Synchronized关键字来取得一个对象的同步锁。


## 死锁

多个线程被同时阻塞，它们中的一个或者全部都在等待某个资源被释放。

