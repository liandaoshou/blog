---
layout: post
title:  "Java Semaphore（信号量-控制同时访问的线程个数）"
date:   2017-03-26 15:23:00 +0800
categories: Java Semaphore
tag: Java
---

## Semaphore（信号量-控制同时访问的线程个数）

信号量，Semaphore可以控制同时访问的线程个数，通过acquire()获取一个许可，如果没有就等待，而release()释放一个许可。

semaphore类中比较重要的方法：

1. public void acquire();用来获取一个许可，若无，则一直等待，直到获取许可成功。
2. public void acquire(int permits);获取permits个许可。
3. public void release();释放许可，在释放之前，必须获得许可。
4. public void release(int permits);释放permits个许可。

上面4个方法都会被阻塞，如果想立即得到执行结果，可以使用下面几个方法。

1. public boolean tryAcquire();尝试获取一个许可，若获取成功则立即返回true，若获取失败，则立即返回false；
2. public boolean tryAcquire(long timeout,TimeUnit unit); 尝试获取一个许可，若在指定的时间内获取成功，则立即返回true，否则立即返回false;
3. public boolean tryAcquire(int permits):尝试获取 permits 个许可，若获取成功，则立即返回 true，若获取失败，则立即返回 false;
4. public boolean tryAcquire(int permits, long timeout, TimeUnit unit): 尝试获取 permits个许可，若在指定的时间内获取成功，则立即返回 true，否则则立即返回 false;
5. 还可以通过 availablePermits()方法得到可用的许可数目。
