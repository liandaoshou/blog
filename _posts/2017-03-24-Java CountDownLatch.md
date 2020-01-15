---
layout: post
title:  "Java CountDownLatch (线程计数器)"
date:   2017-03-24 10:40:00 +0800
categories: Java CountDownLatch
tag: Java
---

CountDownLatch类位于java.util.concurrent包下，利用它可以实现类似计数器的功能。比如有一个任务A，需要等待其他4哥任务执行完毕后才能执行，此时就可以用CountDownLatch来实现。

```
final CountDownLatch latch = new CountDownLatch(2);
new Thread(){
    public void run() {
        System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
        Thread.sleep(3000);
        System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
        latch.countDown();
    };
}.start();
new Thread(){
    public void run() {
        System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
        Thread.sleep(3000);
        System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
        latch.countDown();
    };
}.start();
System.out.println("等待 2 个子线程执行完毕...");
latch.await();
System.out.println("2 个子线程已经执行完毕");
System.out.println("继续执行主线程");

```