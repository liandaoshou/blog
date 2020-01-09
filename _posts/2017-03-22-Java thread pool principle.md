---
layout: post
title:  "Java 线程池原理"
date:   2017-03-22 09:11:23 +0800
categories: Java thread pool principle
tag: Java
---

## 线程池原理

线程池做的工作主要是控制运行的程序数量，处理过程中将任务放入队列，然后再线程创建后启动这些任务，如果线程数量超过最大数量，超出数量的线程排队等候，
等待其他线程执行完毕，再从队列中取出任务来执行。

主要特点为：线程复用，控制最大并发数，线程管理。

### 线程复用

每一个Thread的类都有一个start方法。当调用start启动线程时Java虚拟机会调用该类的run方法。那么此类的run()方法中就是调用了Runnable对象的run()方法。
我们可以继续继承重写Tread类，在其Start方法中添加不断循环调用传递过来的Runnable对象。这就是线程池的实现原理，循环方法中不断获取Runnable是用Queue实现的。
在获取下一个Runnable之前可以是阻塞的。

### 线程池的组成

一般线程池主要分为以下4个部分：

1. 线程池管理器 用于创建并管理线程池
2. 工作线程 线程池中的线程
3. 任务接口 每个任务必须实现接口，用于工作线程调度实现
4. 任务队列 用于存放待处理的任务，提供一种缓冲机制

Java中的线程池通过Executor框架实现，该框架用到了Executor,Executors,ExecutorService,ThreadPoolExecutor,callable和future，FutureTask这几个类。

![线程池框架结构](/images/posts/20170322/01.png)<br>

ThreadPoolExecutor构造方法如下：

```
public ThreadPoolExecutor(int corePoolSize,int maximumPoolSize, long keepAliveTime,
    TimeUnit unit, BlockingQueue<Runnable> workQueue) {
    this(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue,
    Executors.defaultThreadFactory(), defaultHandler);
}
```

1. corePoolSize 指定了线程池中的线程数量。
2. maximumPoolSize 指定了线程池中最大线程数。
3. keepAliveTime 当前线程池数量超过corePoolSize时，多余的空闲线程的存活时间，即多少时间内会被销毁。
4. unit keepAliveTime的单位。
5. workQueue 任务队列，被提交但尚未被执行的任务。
6. threadFactory 线程工厂，用于创建线程，一般用默认即可。
7. handler 拒绝策略，当任务太多来不及处理时，如何拒绝任务。


### 拒绝策略

线程池中线程用完了，无法再继续执行新任务，同时等待队列也排满了，再也塞不下新任务，这时候就需要拒绝策略处理问题。
1. AbortPolicy 直接抛出异常，阻止系统继续运行。
2. CallerRunsPolicy 只要线程池未关闭，该策略直接在调用者线程中，运行当前被丢弃的任务，并不是真的丢弃任务，但是任务提交线程的性能极有可能会急剧下降。
3. DiscardOldestPolicy 丢弃一个最老的请求，也就是即将被执行的一个任务，并尝试再次提交当前任务。
4. DiscardPolicy 默默的丢弃无法处理的任务，如果允许任务丢失，此策略最优。

以上内置策略均实现了RejectedExecutionHandler接口，若以上策略无法满足需求，可自己扩展RejectedExecutionHandler接口。


## 线程池工作过程

1. 线程池刚创建时，里面没有一个线程，任务队列时作为参数传进进来的，就算队列内有任务，线程池也不会马上执行。
2. 当调用execute()方法添加一个任务时，线程池会做出如下判断：
    a) 如果正在运行的线程数量小于corePoolSize，那么马上创建线程任务运行这个任务；
    b) 如果正在运行的线程任务大于或等于corePoolSize，将这个任务放入队列；
    c) 如果队列满了，线程运行数量小于maximumPllSize，那么还是要创建非核心线程立即运行这个任务。
    d) 如果队列满了，而且正在运行的线程数大于或等于maximumPoolSize，那么线程池会抛出异常RejectExecutionException;
3. 当一个线程完成任务时，会从队列中去下一个任务来执行。
4. 当一个线程无事可做，超过一定的事件（keepAliveTime）时，线程池会判断，如果当前运行线程数大于corePoolSize，那么这个线程就会被停掉。
所以线程池的所有任务完成后，最终会收缩到corePoolSize的大小。

![线程池工作过程](/images/posts/20170322/02.png)<br>