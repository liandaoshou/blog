---
layout: post
title:  "Java 后台线程 Daemon"
date:   2017-03-17 09:10:22 +0800
categories: Java Daemon
tag: Java
---

### Java 后台线程

后台线程是指程序运行时后台提供的一种通用服务的线程，这种线程不属于程序中不可或缺的一份部分。
后台线程也称为守护线程，我们创建的线程一般是用于处理我们自己的相关业务，但是后台线程主要用于公共任务，例如JVM处理垃圾回收，使用的就是后台线程。
我们创建线程可以在start()启动前，thread.setDaemon(true);将其设置为后台线程，也可以使用isDaemon()来判断线程是否为后台线程。

特点：

1. 守护线程也称为服务线程，他是后台线程，有一个特性为用户线程提供公共服务，没有用户线程可服务时会自动离开。
2. 守护线程优先级比较低，用于为系统中的其他对象和线程提供服务。
3. 我们创建线程可以在start()启动前，thread.setDaemon(true);将其设置为后台线程。
4. 守护线程中产生的新线程也时守护线程。
5. 守护进程是后台运行的特殊进程，独立控制终端并且周期性得执行某种任务或等待处理某些发生事件。也就是说守护线程不依赖与终端，但是依旧依赖与系统，与系统同生共死。
当JVM所有线程都是守护线程的时候，JVM就可以退出了，如果还有一个以上的非守护线程，JVM不会退出。
