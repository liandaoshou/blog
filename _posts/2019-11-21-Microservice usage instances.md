---
layout: post
title:  "微服务使用实例"
date:   2019-11-21 10:15:00 +0800
categories: 微服务使用实例 Spring cloud Spring boot
tag: Java
---

# 使用环境
1. jdk 8
2. maven 3.6
3. 编辑器 idea

## 提前准备

* RabbitMQ <br>
    mac环境下 （brew 安装）brew install rabbitmq <br/>
    brew services start rabbitmq <br/>
    默认用户名和密码：guest,guest
* nacos <br/>
    https://github.com/alibaba/nacos/releases<br/>
    nacos-server-1.1.4.zip<br/>
    解压<br/>
    目录 bin中<br/>
    sh startup.sh -m standalone<br/>
    配置文件查看端口v
    http://127.0.0.1:8001/nacos<br/>
    使用用户名密码登陆
* redis<br/>
    mac环境下<br/>
        brew install redis

## 新建项目
![新建项目1](/images/posts/20191121/create1.jpg) <br/>
