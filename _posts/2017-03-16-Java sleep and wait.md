---
layout: post
title:  "Java sleep 和 wait 的区别"
date:   2017-03-16 21:54:09 +0800
categories: Java Sleep And Wait
tag: Java
---

### sleep 和 wait 的区别

1. 对于sleep()方法，sleep属于Tread类，wait()属于Object类。
2. sleep()方法导致程序执行指定的时间，让出cpu改其他线程，但是监控状态依然保持，当指定时间到后又会恢复自动运行状态。
sleep需要传入指定的时间，wait不需要。
3. 调用sleep方法过程中，线程不会释放对象锁。
4. 调用wait方法后线程会放弃对象锁，进入等待对象的等待锁池，只有针对此对象调用的notify或者notifyall线程才准备获取对象锁进入运行状态。

