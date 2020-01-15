---
layout: post
title:  "Java CyclicBarrier（回环栅栏-等待至 barrier 状态再全部同时执行）"
date:   2017-03-25 15:08:00 +0800
categories: Java CyclicBarrier
tag: Java
---

##  CyclicBarrier（回环栅栏-等待至 barrier 状态再全部同时执行）

字面意思回环栅栏，可以实现让一组线程等待至某个状态之后再全部同步执行。当所有等待线程都被释放以后，CyclicBarrier可以被重用。
我们暂且把这个状态叫做barrier，当调用await()方法之后，线程就处于barrier了。

CyclicBarrier中最重要的方法就是await方法，它有2个重载版本：

1. public int await(); 用来挂起当前线程，直至所有线程都到达barrier再同时执行后续任务。

2. public int await(long timeout,TimeUnit unit); 让这些线程等待至一定的时间，如果还有线程没有到达barrier状态就直接让到达barrier的线程执行后续任务。




