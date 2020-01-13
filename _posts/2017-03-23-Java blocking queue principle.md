---
layout: post
title:  "Java 阻塞队列原理"
date:   2017-03-23 19:31:03 +0800
categories: Java blocking queue principle
tag: Java
---

## Java 阻塞队列原理

在阻塞队列中，线程阻塞有两种情况：
1. 当队列中没有数据的情况下，消费者端的所有线程都会被自动阻塞（挂起），直到有数据放入队列。
2. 当队列中填满数据的情况下，生产者端的所有线程都会被自动阻塞（挂起），直到队列中有空的位置，线程被自动唤醒。

### 阻塞队列的主要方法

方法类型 | 抛出异常 | 特殊值 | 阻塞 | 超时
-------- | ------- | ----- | ---- | ----
插入 | add(e) | offer(e) | put(e) | offer(e,time,unit)
移除 | remove() | poll() | take() | poll(time,unit)
检查 | element() | peek() | 不可用 | 不可用

抛出异常： 抛出异常 
特殊值： 返回一个特殊值（null 或 false，视情况而定）
阻塞: 在成功操作之前，一直阻塞线程
超时： 放弃前直在最大时间内阻塞

### 插入操作

1. public abstract boolean add(E paramE)：将指定元素插入此队列中（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则抛出 IllegalStateException。如果该元素是 NULL，则会抛出 NullPointerException 异常。

2. public abstract boolean offer(E paramE)：将指定元素插入此队列中（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则返回 false。

3. public abstract void put(E paramE) throws InterruptedException： 将指定元素插入此队列中，将等待可用的空间（如果有必要）

```
public void put(E paramE) throws InterruptedException {
     checkNotNull(paramE);
     ReentrantLock localReentrantLock = this.lock;
     localReentrantLock.lockInterruptibly();
     try {
         while (this.count == this.items.length)
         this.notFull.await();//如果队列满了，则线程阻塞等待
         enqueue(paramE);
         localReentrantLock.unlock();
     } finally {
        localReentrantLock.unlock();
     }
}
```

4. offer(E o, long timeout, TimeUnit unit)：可以设定等待的时间，如果在指定的时间内，还不能往队列中加入 BlockingQueue，则返回失败。

### 获取数据操作

1. poll(time):取走 BlockingQueue 里排在首位的对象,若不能立即取出,则可以等 time 参数规定的时间,取不到时返回 null;

2. poll(long timeout, TimeUnit unit)：从 BlockingQueue 取出一个队首的对象，如果在指定时间内，队列一旦有数据可取，则立即返回队列中的数据。否则直到时间超时还没有数据可取，返回失败。

3. take():取走 BlockingQueue 里排在首位的对象,若 BlockingQueue 为空,阻断进入等待状态直到 BlockingQueue 有新的数据被加入。

4. drainTo():一次性从 BlockingQueue 获取所有可用的数据对象（还可以指定获取数据的个数），通过该方法，可以提升获取数据效率；不需要多次分批加锁或释放锁。


##  Java 中的阻塞队列

- ArrayBlockingQueue ：由数组结构组成的有界阻塞队列。

用数组实现的有界阻塞队列，此队列按照先进先出（FIFO）的原则对元素进行排序。默认情况下不保证访问者公平的访问队列，所谓公平访问队列是指阻塞的所有生产者线程或消费者线程。
当队列可用时可以按照阻塞的先后顺序访问队列，即先组晒生产者的线程，可以先往队列里插入元素，先阻塞消费者线程，可以先从队列里获取元素。
通常情况下为了保证公平性会降低吞吐量。

` ArrayBlockingQueue fairQueue = new ArrayBlockingQueue(1000,true); `
 
- LinkedBlockingQueue ：由链表结构组成的有界阻塞队列。

基于链表的阻塞队列，同ArrayListBlockingQueue类似，此队列按照先进先出（FIFO）的原则对元素进行排序，而LinkedBlockingQueue之所以能够高效处理并发数据，
还因为其对于生产者端和消费者端分别采用了独立的锁来控制数据同步，这也意味着在高并发的情况下生产者和消费者可以并行地操作队列中的数据，以此来提高整个队列的并发性能。
LinkedBlockingQueue会默认一个类似无限大小的容量（Integer.MAX_VALUE）

- PriorityBlockingQueue ：支持优先级排序的无界阻塞队列。

支持优先级的无界队列，默认情况下元素采取自然顺序升序排序。可以自定义实现compareTo()方法来指定元素进行排序规则，或者初始化PriorityBlockingQueue时，
指定构造参数Comparator来对元素进行排序。需要注意的是不能保证同优先级的元素的顺序。

- DelayQueue：使用优先级队列实现的无界阻塞队列。

支持延时获取元素的无界阻塞队列，队列使用PriorityQueue来实现，队列中的元素必须实现Delayed接口,在创建元素时可以指定多久才能从队列中获取当前元素，只有在延迟期满时才能从队列中提取元素。
DelayQueue运用在以下场景：

1. 缓存系统设计，可以用DelayQueue保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦不能取到元素，表示有效期已到。
2. 定时任务调度，使用DelayQueue保存当天执行的任务和执行时间，获取到任务就开始执行，从TimerQueue就是使用DelayQueue实现的。

- SynchronousQueue：不存储元素的阻塞队列。

是一个不存储元素的阻塞队列，每一个put操作必须等待一个take操作，否则不能继续添加元素，SynchronousQueue可以看成一个传球手，负责把生产者线程处理的数据直接传递给消费者线程。
线程本身不存储任何元素，非常适合传递场景，比如在一个线程中使用的数据，传递给另外一个线程，SynchronousQueue的吞吐量高于LinkedBlocking和ArrayBlockingQueue。

- LinkedTransferQueue：由链表结构组成的无界阻塞队列。

是一个由链表结构组成的无界阻塞TransFerQueue队列。相对于其他阻塞队列，LinkedTransferQueue多了tryTransfer和transfer方法。

1. transfer方法： 如果当前有消费者正在等待接收元素（消费者使用take()方法或带时间限制的poll()方法时），transfer方法可以把生产者传入元素立刻transfer（传输）给消费者。
如果没有消费者在等待元素，transfer方法会将元素放在队列的tail节点，并等到该元素被消费了才返回。

2. tryTransfer方法。则时用来试探下生产者传入的元素是否能直接传给消费者。如果没有消费者等待接收元素，则返回false和transfer方法的区别是tryTransfer方法无论消费者是否接收，
方法立即返回，而transfer方法必须等到消费者消费了才返回。

对于带有时间限制的tryTransfer（E e,long timeout,TimeUnit unit）方法，则是试图把生产者传入元素之间传给消费者，但是如果没有消费者消费该元素则等待指定的时间再返回，如果超时还没消费元素，
则返回false，如果在超时时间内消费了元素，则返回true。


- LinkedBlockingDeque：由链表结构组成的双向阻塞队列

由链表结构组成的双向阻塞队列。所谓双向队列是指可以从队列的两端插入和移除元素。双端队列因为多了一个操作队列的入口，在多线程同事入队时，也就减少了一半的竞争。
相对比其他的阻塞队列，LinedBlockingDeque多了addFirst，addLast，offerFirst，offerLast，peekFirst，PeekLast等方法，以First单词结尾的方法，表示插入，
获取（peek）或移除双端队列的一个元素。以Last单词结尾的方法，表示插入，获取或移除双端队列的最后一个元素。另外插入方法add等同于addLast，移除方法remove等效于
removeFirst。但是take方法却等同于takeFirst，使用时还是用带由First和Last后缀的方法更清楚。

在初始化LinedBlockingDeque时可以设置容量防止其过度膨胀，另外双向队列阻塞队列可运用在工作窃取模式中。



