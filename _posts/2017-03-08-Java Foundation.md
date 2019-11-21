---
layout: post
title:  "Java基础 （环境配置与hello world）"
date:   2017-03-08 10:08:12 +0800
categories: Welcome to my blog
tag: Java
---

### 安装Java环境

下载jdk

官网：http://www.oracle.com/technetwork/java/javase/downloads/index.html

傻瓜式安装

安装完成配置 环境变量

安装完成后 命令行输入 java -version 测试是否安装成功

编辑器 idea



### 亘古不变的hello world

```
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}
```
文件保存为HelloWorld.java

命令行工具输入 javac HelloWorld.java

javac 将java文件编译为class字节码文件 

java HelloWorld 

输出

```
hello world
```

```
javac [ options ] [ sourcefiles ] [ @files ]

options命令行选项。sourcefiles一个或多个要编译的源文件（例如 MyClass.java）。@files一个或多个对源文件进行列表的文件。

```