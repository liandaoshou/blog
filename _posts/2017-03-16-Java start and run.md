---
layout: post
title:  "Java start 和 run 的区别"
date:   2017-03-16 22:11:49 +0800
categories: Java Start And Run
tag: Java
---

### start和run区别

1. start() 方法用来启动线程，真正实现多线程运行，这时无需等待run方法体代码执行完毕，可以直接执行下面的代码。
2. 通过调用Thread类的start方法来启动线程，这时线程处于就绪状态，并没有运行。
3. 方法run()是线程体，包含要执行的线程内容，线程进入运行状态，开始运行run函数中的代码，run方法运行结束，线程终止。
