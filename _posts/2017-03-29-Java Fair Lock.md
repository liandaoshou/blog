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
加锁时不考虑排队等待问题，直接尝试获取锁，获取不到自动到队尾等待
1. 非公平锁性能比公平锁高 5~10 倍，因为公平锁需要在多核的情况下维护一个队列
2. Java 中的 synchronized 是非公平锁，ReentrantLock 默认的 lock()方法采用的是非公平锁。


## Java公平锁

公平锁指定锁分配机制是公平的，通常先对锁提出获取请求的线程会先被分配到锁，ReentrantLock在构造函数中提供了是否公平锁的初始化方法来定义公平锁。
加锁前检查是否有排队等待的线程，优先排队等待的线程，先来先得。

## ReentrantLock 与 synchronized

1. ReentrantLock 通过方法lock()与unlock()来进行加锁与解锁操作，与synchronized会被JVM自动解锁机制不同，ReentrantLock加锁后需要手动进行解锁。
为了避免程序出现异常无法正常解锁的情况，使用ReentrantLock必须在finally控制模块中进行解锁操作。

2. ReentrantLock相比synchronized优势是可以中断，公平锁，多个锁。


ReentrantLock 实现

```java
public class MyService {
    private Lock lock = new ReentrantLock();
    //Lock lock=new ReentrantLock(true);//公平锁
    //Lock lock=new ReentrantLock(false);//非公平锁
    private Condition condition=lock.newCondition();//创建 Condition
    public void testMethod() {
        try {
            lock.lock();//lock 加锁
            //1：wait 方法等待：
            //System.out.println("开始 wait");
            condition.await();
            //通过创建 Condition 对象来使线程 wait，必须先执行 lock.lock 方法获得锁
            //:2：signal 方法唤醒
            condition.signal();//condition 对象的 signal 方法可以唤醒 wait 线程
            for (int i = 0; i < 5; i++) {
                System.out.println("ThreadName=" + Thread.currentThread().getName()+ (" " + (i + 1)));
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```