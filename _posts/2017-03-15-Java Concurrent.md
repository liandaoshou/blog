---
layout: post
title:  "Java 多线程并发"
date:   2017-03-15 16:15:09 +0800
categories: Java Concurrent
tag: Java
---

# Java多线程并发

### 并发和并行

并发是指同一个时间段内多个任务同时在执行，并且都没有执行结束，并发任务强调在一个时间段内同时执行，而一个时间段由多个单位时间积累而成，
所以说并发的多个任务在单位时间内不一定同时在执行。

并行是指在单位时间内多个任务同时在执行。在多线程编程实践中，线程个数往往多于CPU的个数，所以一般都称为多线程并发编程而不是多线程并行编程。

## Java线程实现/创建方式

### 继承Thread类

Thread类本质是实现Runnable的接口一个实例，代表一个线程实例，代表一个线程的实例，启动线程的唯一方式就是通过Thread类的start()实例方法，start()方法是一个native方法，它启动一个新的线程并执行run()方法.

```java
public class UseThread  {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start();
    }
}

class MyThread extends Thread {
    public void run () {
        System.out.println("run1");
    }
}
```

### 实现Runnable接口

如果一个类已经继承另一个类就无法直接继承Thread，可以实现一个Runnable接口。
首先定义一个实现Runnable接口。覆盖Runnable接口中的run方法，将线程要运行的方法放在run方法中。通过Thread类建立线程对象，将Runnable接口的子类对象作为实际参数传递给Thread类的构造函数。
调用Thread类的start方法开启线程并调用Runnable接口的子类的run()方法。

实现和继承方式的区别：
    1.避免单继承的局限性。
    2.在定义线程过程中，建立使用实现方式。
    
两种方式的区别：
    1.继承Tread线程代码存放Tread子类的run方法中。
    2.实现Runnable线程代码在接口的子类run方法中。

```java
public class UseThread  {
    public static void main(String[] args) {
        MyThread1 myThread1 = new MyThread1();
        Thread thread = new Thread(myThread1);
        thread.start();
    }
}

class MyThread1 implements Runnable {

    @Override
    public void run() {
        System.out.println("run2");
    }
}
```

### ExecutorService、Callable<Class>、Future有返回值的线程

有返回值的任务必须实现Callable接口，无返回值的可以使用Runnable接口。执行Callable任务后，可以获得一个Future的对象，在对象上调用get可以获得Callable任务返回的Object。
结合线程池接口ExecutorService就可以实现有返回结果的多线程。

```java
public class UseThread {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        MyCallable callable = new MyCallable();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        Future f = executor.submit(callable);
        System.out.println("提交任务之后，获取结果之前 " + getStringDate());
        System.out.println("获取返回值: " + f.get());
        System.out.println("获取到结果之后 " + getStringDate());
    }

    public static String getStringDate() {
        Date currentTime = new Date();
        SimpleDateFormat formatter = new SimpleDateFormat("HH:mm:ss");
        return formatter.format(currentTime);
    }
}

class MyCallable implements Callable {

    @Override
    public Object call() throws Exception {
        Thread.sleep(3000);
        return "call1";
    }
}
```

## 基于线程池

### newCachedThreadPool 缓存线程池

创建一个可根据需要创建新的线程池，但是之前构造的线程可以同时重用，对于执行很多短期异步任务而言，线程通常可以提高程序性能。调用execute重用之前构造的线程（如果线程可用）。
如果现有没有线程可用则创建一个新线程添加到池中。终止并从缓存中移除60秒内未被使用的线程。因此长时间保持空闲的线程池不会使用任何资源。

### newFixedThreadPool 定长线程池，可控制线程最大并发数，超出的线程会在队列中等待

创建一个可重用固定线程数量的线程池，以共享的无界队列方式来运行这些线程。在任意点，在大多数线程会处于处理活动状态。如果所有线程处于活动状态时提交附件任务，则在有可用线程之前，
附加任务会在队列中等待。如果在所有线程处于活动状态时提交附加任务，则在有可用线程之前，附件任务将在队列中等待。如果关闭钱的执行期间由于失败导致线程终止，会有新线程代替执行后续任务。
如果线程被显式关闭之前，池中线程将会一直存在。

### newScheduledThreadPool 定长线程池，支持定时及周期性任务执行

创建一个线程池，可安排在给定延迟后运行命令或定期执行。

### newSingleThreadExecutor 单一线程

单一线程，这个线程池可用在线程结束或者发生异常时，重一个线程来替代原来的线程继续执行下去。


## 线程生命周期

线程被创建并启动后，不是一启动就进入执行状态，也不是一直处于执行状态。在线程生命周期中，要经过新建（new）、就绪（Runnable）、运行（Running）、
阻塞（Blocked）和死亡（Dead）五种状态。尤其当线程启动以后，不可能一直霸占CPU独自运行，CPU需要在多条线程之间切换，于是线程状态也会多次在运行、阻塞直接切换。

### 新建

当程序使用new关键字创建一个线程后，该线程就处于新建状态，此时仅由JVM为其分配内存，并初始化成员变量的值。

### 就绪

当线程对象调用start()方法后，该线程处于就绪状态，Java虚拟机会为其创建方法调用栈和程序计数器，等待调度运行。

### 运行

如果处于就绪状态线程获得CPU，开始执行run()方法的线程执行体，则该线程处于运行状态。

### 阻塞

阻塞状态时线程因为某些原因放弃CPU使用权，也让出了CPU timeslice，暂时停止运行知道线程进入可运行状态，才有机会再次获得cpu timeslice 转到运行状态。
阻塞情况分三种：

* 等待阻塞（o.wait->等待队列）

    运行线程的执行o.wait()方法，JVM会把线程放入等待队列中。
    
* 同步阻塞（lock->锁池）

    运行线程获取对象的同步锁时，若该同步锁被别的线程占用，JVM会把该线程放入锁池中。
    
* 其他阻塞
    运行线程执行Thread.sleep或t.join方法，或者发出I/O请求时，JVM会把线程设置为阻塞状态。当sleep()状态超时，join()等待终止或者超时、I/O处理完毕时，线程重新转入可运行状态。
    
### 死亡

线程会在以下三种方式结束，结束后就是死亡状态。
* 正常结束
    run()或者call()方法执行完成，线程正常结束。
* 异常结束
    线程抛出未捕获的Exception或者Error。
* 调用Stop
    直接调用该线程的stop方法结束该线程，此方法容易导致死锁，不建议使用。

## 终止线程的四种方式

### 正常运行结束

程序运行结束，线程自动结束。

### 使用退出标志退出线程

一般run()方法执行完成后，线程就会正常结束，然而有些线程时伺服线程。需要长时间的运行，只有在外部某些条件满足的情况下，才能关闭线程。使用一个变量来控制循环。

例如：
最直接的方法就是设一个 boolean 类型的标志，并通过设置这个标志为 true 或 false 来控制 while循环是否退出，代码示例：
```java
public class ThreadSafe extends Thread {
 public volatile boolean exit = false;
 public void run() {
 while (!exit){
 //do something
 }
 }
}
```
定义了一个退出标志 exit，当 exit 为 true 时，while 循环退出，exit 的默认值为 false.在定义 exit时，使用了一个 Java 关键字 volatile，这个关键字的目的是使 exit 同步，也就是说在同一时刻只能由一个线程来修改 exit 的值。

### Interrupt 方法结束线程

1. 线程处于阻塞状态，如果使用sleep，同步锁的wait，socket中的receiver，accept等方法，会使线程处于阻塞状态。当调用线程interrupt()方法时，会抛出InterruptException异常。
阻塞中的那个方法抛出这个异常，通过代码捕获异常，然后break跳出循环状态，通常很多人认为只要调用interrupt方法就会结束线程。实际上时错误的，一定要捕获InterruptedException异常后，再break跳出循环，才能正常结束run()方法。

2. 线程为处于阻塞状态，使用isInterrupted()判断线程的中断标志来退出循环。当使用interrupt()方法时，中断标志就会置true，和使用自定义的标志来控制循环是一样的道理。

### stop方法终止线程（线程不安全）

程序中可以直接使用Thread.stop()来强制终止线程，但是stop方法很危险。调用之后子线程就会抛出TreadDeathError错误并且会释放子线程持有的所有锁。
一般任何进行加锁的代码块，都是为了保护数据的一致性，如果在调用Thread.stop()后导致线程所持有的所有锁突然释放，那么被保护的数据有可能呈现不一致性，可能会导致其他错误，所以不推荐使用stop终止线程。
