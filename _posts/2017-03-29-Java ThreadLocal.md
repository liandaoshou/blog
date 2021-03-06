---
layout: post
title:  "Java ThreadLocal 作用（线程本地存储）"
date:   2017-03-29 11:11:00 +0800
categories: Java ThreadLocal
tag: Java
---

ThreadLocal叫线程本地变量，也叫线程本地存储，ThreadLocal的作用是提供线程内的局部变量，这种变量在线程的生命周期内起作用，
减少同一个线程内多个函数或者组件之间一些公共变量的传递的复杂度。

### ThreadLocalMap（线程的一个属性）

1. 每个线程中都有一个自己的ThreadLocalMap类对象，可以将线程自己的对象保持到其中，各管各自，线程可以正确的访问到自己的对象。
2. 将一个公共的ThreadLocal静态实例作为key，将不同对象的引用保存到不同线程的ThreadLocalMap中，然后在线程执行的各处通过这个静态ThreadLocal实例的get()
方法取得自己的线程保存的那个对象，避免了将这个对象作为参数传递的麻烦。
3. ThreadLocalMap其实就是线程里面的一个属性，Tread类中定义

`ThreadLocal.ThreadLocalMap threadLocals = null;`

最常见的 ThreadLocal 使用场景为 用来解决 数据库连接、Session 管理等。

```
private static final ThreadLocal threadSession = new ThreadLocal();
public static Session getSession() throws InfrastructureException {
    Session s = (Session) threadSession.get();
    try {
        if (s == null) {
            s = getSessionFactory().openSession();
            threadSession.set(s);
        }
    } catch (HibernateException ex) {
        throw new InfrastructureException(ex);
    }
    return s;
}
```