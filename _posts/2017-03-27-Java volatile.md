---
layout: post
title:  "volatile 关键字的作用（变量可见性、禁止重排序）"
date:   2017-03-27 09:13:00 +0800
categories: Java volatile
tag: Java
---

## Java volatile

Java语言提供乐一种稍弱的同步机制，volatile变量，用来确保将变量的更新操作通知到其他线程，volatile变量具备两种特性，volatile变量不会被缓存在寄存器或者对其他处理器不可见的地方，
因此在读取volatile类型的变量总是会返回最新的写入值。

变量可见性

保证该变量对所有线程可见，这里的可见性是指当一个线程修改乐变量的值，那么新的值对于其他的线程可以立即获取。

禁止重排序

volatile禁止了指令重排，比synchronized更轻量级的同步锁。

在访问volatile变量时不会执行加锁操作，因此也就不会使执行线程阻塞，因此volatile变量是一种比synchronized关键字更轻量级的同步机制。
volatile适合这种场景，一个变量被多个线程共享，线程之间给这个变量赋值。

当对非volatile变量进行读写的时候，每个线程先从内存拷贝变量到CPU缓存中，如果计算机有多个CPU，每个线程可能在不同CPU上被处理，这意味着每个线程可以拷贝到不同的CPU
cache中，而声名变量是volatile的，JVM保证了每次读变量都从内存中读，跳过CPU cache这一步。

适用场景

volatile变量的单次读写操作可以保证原子性，如long和double类型变量，但是并不能保证i++这种操作的原子性，本质上i++是读写两次操作。
某些场景下可以代替synchronized，但是volatile并不能完全替代Synchronized的位置，只有在一些特殊场景下，才能使用volatile。
总的来说必须同时满足两个条件下才能保证在并发环境的线程安全

- 对于变量的写操作不依赖当前值，比如i++，或者说是单纯的变量赋值 boolean flag = true
- 该变量没有包含在具有其他变量的不变式中，也就是说，不同volatile变量之间，不能相互依赖。只有在状态真正独立于程序内其他内容时才能使用volatile。

