---
layout: post
title:  "Java 线程基本方法"
date:   2017-03-19 13:20:12 +0800
categories: basic method of threads
tag: Java
---

## Java 线程基本方法

线程相关的基本方法有 wait，notify，notifyAll，sleep，join，yield 等。

![线程基本方法](/images/posts/20170319/01.png)<br>

### 线程等待 （wait）

调用该方法线程进入waiting状态，只有等待另外线程的通知或者被中断才会返回，需要注意的是调用wait()方法，会释放对象锁。因此wait方法一般用在同步方法或者同步代码块中。

### 线程睡眠 （sleep）

sleep导致当前线程休眠，与wait方法不同sleep不会释放当前占有锁，sleep(long)会导致线程进入TIMED-WATING 状态。

### 线程让步 （yield）

yield会使当前线程让出cpu执行时间片，与其他线程一起重新竞争cpu时间片，一般情况下优先级高的线程有更大可能成功竞争到cpu时间片，但是不是绝对的，有的操作系统对线程的优先级不敏感。

### 线程中断 （interrupt）

中断一个线程给这个线程一个通知信号，会影响线程内部的中断标识为，这个线程本身不因此改变状态（阻塞，终止等）

### join等待其他线程终止

join() 方法，等待其他线程终止，在当前线程中调用一个线程的 join() 方法，则当前线程转为阻塞状态，回到另一个x线程线程结束，当前线程再由阻塞状态变为就绪状态。

很多情况下，主线程生成并启动了子线程，需要用到子线程返回的结果，也就是需要主线程需要在子线程结束后再结束，这时候就要用到 join() 方法。

```java
    System.out.println(Thread.currentThread().getName() + "线程运行开始!");
    Thread6 thread1 = new Thread6();
    thread1.setName("线程 B");
    thread1.join();
    System.out.println("这时 thread1 执行完毕之后才能执行主线程");
```

### 线程唤醒 （notify）

Object类中的notify方法，唤醒在此对象监视器上的等待的单个线程，如果所有线程都在此对象上等待，则会选择唤醒其中一个线程，选择使任意的，并在对实现做出决定时发生。
线程通过调用其中一个wait方法，在对象监视器上等待，直到当前的线程放弃此对象上的锁定，才能继续执行被唤醒的线程，被唤醒的线程将以常规方式与在该对象上主动同步其他所有线程进行竞争。
类似的方法还有notifyAll(),唤醒再次监视器上的等待所有线程。

### 其他常用方法

1. sleep() 强迫一个线程睡眠设置毫秒数。
2. isAlive() 判断一个线程是否存活。
3. join() 等待线程终止。
4. activeCount() 程序中活跃的线程数。
5. enumerate() 枚举程序中线程。
6. currentThread() 得到当前线程。
7. isDaemon() 是否是守护线程。
8. setDaemon() 设置一个线程为守护线程。
9. setName() 为线程设置一个名称
10. wait() 强迫一个线程等待。
11. notify() 通知一个线程等待。
12. setPriority() 设置一个线程的优先级。
13. getPriority() 获得一个线程的优先级。





