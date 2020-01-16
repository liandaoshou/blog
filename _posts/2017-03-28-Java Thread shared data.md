---
layout: post
title:  "Java如何在两个线程之间共享数据"
date:   2017-03-28 09:01:00 +0800
categories: Java Thread Shared data
tag: Java
---

## Java如何在两个线程之间共享数据

Java 里面进行多线程通信的主要方式就是共享内存的方式，共享内存主要关注点有两个，可见性和有序性原子性。

Java内存模型解决了可见性和有序性的问题，而锁解决了原子性的问题，理想情况下我们希望做到同步和互斥。

- 将数据抽象成一个类，并将数据的操作作为这个类的方法。

```
public class MyData {
    private int j=0;
    public synchronized void add(){
        j++;
        System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public synchronized void dec(){
        j--;
        System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public int getData(){
        return j;
    }
}
public class AddRunnable implements Runnable{
    MyData data;
    public AddRunnable(MyData data){
        this.data= data;
    } 
    public void run() {
        data.add();
    }
}
public class DecRunnable implements Runnable {
    MyData data;
    public DecRunnable(MyData data){
        this.data = data;
    }
    public void run() {
        data.dec();
    }
}

public static void main(String[] args) {
    MyData data = new MyData();
    Runnable add = new AddRunnable(data);
    Runnable dec = new DecRunnable(data);
    for(int i=0;i<2;i++){
        new Thread(add).start();
        new Thread(dec).start();
    }
}

```

- Runnable 对象作为一个类的内部类

将Runnable对象作为一个类的内部类，共享数据作为这个类的成员变量，每个线程对共享数据的操作方法也封装在外部类，以便实现对数据的哥哥操作的同步和互斥，
作为内部类的哥哥Runnable对象调用外部类的方法。

```
public class MyData {
    private int j=0;
    public synchronized void add(){
        j++;
        System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public synchronized void dec(){
        j--;
        System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public int getData(){
        return j;
    }
}
public class TestThread {
    public static void main(String[] args) {
        final MyData data = new MyData();
        for(int i=0;i<2;i++){
            new Thread(new Runnable(){
            public void run() {
                data.add();
            }
        }).start();
        new Thread(new Runnable(){
            public void run() {
                data.dec();
            }
            }).start();
        }
    }
}
```