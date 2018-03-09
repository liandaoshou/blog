---
layout: post
title:  "Spring Boot 线程操作 (二) "
date:   2018-03-09 15:17:00 +0800
categories: Spring Boot thead used
tag: Spring Boot
---


#Spring Boot 线程使用(二) 
@(Spring Boot)[SyncTaskExecutor|SimpleAsyncTaskExecutor|ThreadPoolTaskExecutor] 
### 使用示例
``` 
package com.example.demo.controller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.core.task.AsyncTaskExecutor;
import org.springframework.core.task.SimpleAsyncTaskExecutor;
import org.springframework.core.task.SyncTaskExecutor;
import org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.Future;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

@RestController
public class ThreadTestController {
    private static final Logger log = LoggerFactory.getLogger(ThreadTestController.class);

    //同步
    @RequestMapping("/test")
    public String test(){
        SyncTaskExecutor executor = new SyncTaskExecutor();
        executor.execute(new OutThread());
        System.out.println("Hello, World!");
        log.info("Hello World");
        return "Hello World";
    }

    //异步
    @RequestMapping("/test1")
    public String test1(){
        AsyncTaskExecutor executor = new SimpleAsyncTaskExecutor("sys.out");
        executor.execute(new OutThread());
        System.out.println("Hello");
        return "Hello World";
    }

    //同步线程池
    @RequestMapping("/test2")
    public String test2() {
        System.out.println("start");
        testThreadTask();
        testThreadTask();
        System.out.println("end");
        return "test2";
    }

    private static void testThreadTask() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(2);
        executor.setMaxPoolSize(4);
        executor.setKeepAliveSeconds(120);
        executor.setQueueCapacity(32);
        executor.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy());
        executor.initialize();
        List<Future<String>> taskResults = new ArrayList<Future<String>>();
        for(int k=0; k<10; k++){
            taskResults.add(process(executor, k));
        }

        // 监控是否执行结束
        while (true) {
            boolean isAllDone = true;
            for (Future<String> taskResult : taskResults) {
                isAllDone &= ( taskResult.isDone() || taskResult.isCancelled() );
            }
            if (isAllDone) {
                // 任务都执行完毕，跳出循环
                break;
            }
            try {
                System.out.println("waiting and sleep 1000 ...");
                TimeUnit.MILLISECONDS.sleep(1000);
            } catch (Exception e) {
                System.out.println(e.toString());
                break;
            }
        }
    }

    private static Future<String> process(final ThreadPoolTaskExecutor executor , final int k) {
        return executor.submit(new Callable<String>() {
            @Override
            public String call() throws Exception {
                try {
                    Thread.sleep((k+1)*500);
                    System.out.println(" k=" + k);
                } catch (Exception e) {

                }
                return "k=" + k + " success";
            }
        });
    }

    static class OutThread implements Runnable {
        public void run() {
            for (int i = 0; i < 10; i++) {
                System.out.println(i + " start ...");
                try {
                    Thread.sleep(2 * 1000L);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

``` 
