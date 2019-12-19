---
layout: post
title:  "docker安装rabbitmq"
date:   2019-12-19 15:20:00 +0800
categories: docker 
tag: docker
---

## docker安装rabbitmq

### 查找
```
#docker search rabbitmq

NAME                                       DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
rabbitmq                                   RabbitMQ is an open source multi-protocol me…   2945                [OK]
bitnami/rabbitmq                           Bitnami Docker Image for RabbitMQ               38                                      [OK]
tutum/rabbitmq                             Base docker image to run a RabbitMQ server      20
kbudde/rabbitmq-exporter                   rabbitmq_exporter for prometheus                12                                      [OK]
frodenas/rabbitmq                          A Docker Image for RabbitMQ                     12                                      [OK]
cyrilix/rabbitmq-mqtt                      RabbitMQ MQTT Adapter                           8                                       [OK]
arm32v7/rabbitmq                           RabbitMQ is an open source multi-protocol me…   7
gonkulatorlabs/rabbitmq                    DEPRECATED: See maryville/rabbitmq              5                                       [OK]
aweber/rabbitmq-autocluster                RabbitMQ with the Autocluster Plugin            4
pivotalrabbitmq/rabbitmq-server-buildenv   Image used to build and test RabbitMQ server…   3
pivotalrabbitmq/rabbitmq-autocluster       RabbitMQ with the rabbitmq-autocluster plugi…   3
henrylv206/rabbitmq-autocluster            RabbitMQ Cluster                                2                                       [OK]
deadtrickster/rabbitmq_prometheus          RabbitMQ + Prometheus RabbitMQ Exporter plug…   2
riftbit/rabbitmq                           RabbitMQ 3.x Container based on Alpine Linux…   1
amd64/rabbitmq                             RabbitMQ is an open source multi-protocol me…   1
webhostingcoopteam/rabbitmq-conf           RabbitMQ Configurator for Rancher               1                                       [OK]
foxylion/rabbitmq                          Preconfigured RabbitMQ docker image with sup…   1                                       [OK]
activatedgeek/rabbitmqadmin                A rabbitmqadmin docker image for administrat…   1                                       [OK]
arm64v8/rabbitmq                           RabbitMQ is an open source multi-protocol me…   1
ekesken/rabbitmq                           docker image for rabbitmq that is configurab…   0                                       [OK]
i386/rabbitmq                              RabbitMQ is an open source multi-protocol me…   0
pdffiller/rabbitmq                         Rabbitmq 3.7.3 with delayed_message plugin,c…   0
s390x/rabbitmq                             RabbitMQ is an open source multi-protocol me…   0
ppc64le/rabbitmq                           RabbitMQ is an open source multi-protocol me…   0
newsdev/rabbitmq                           rabbitmq:olympics Extends official rabbitmq …   0                                       [OK]

```
### 获取

```
docker pull rabbitmq (镜像未配有控制台)
docker pull rabbitmq:management (镜像配有控制台)

management: Pulling from library/rabbitmq
7ddbc47eeb70: Pull complete                                                                                                                        c1bbdc448b72: Pull complete                                                                                                                        8c3b70e39044: Pull complete                                                                                                                        45d437916d57: Pull complete                                                                                                                        916459a32f87: Pull complete                                                                                                                        4987fa1cb144: Pull complete                                                                                                                        d3294ff2c0a8: Pull complete                                                                                                                        5d1458a0e30b: Pull complete                                                                                                                        5f912931f22b: Pull complete                                                                                                                        4136bd84b69c: Pull complete                                                                                                                        ca51c3034c18: Pull complete                                                                                                                        12e1a4d8ed37: Pull complete                                                                                                                        Digest: sha256:57c19e6b134d064912d3697a4dd24b4b91a27f2a0e2a869636abe84cd27d0fcc
Status: Downloaded newer image for rabbitmq:management
docker.io/library/rabbitmq:management
```

### 安装

```
docker run --name rabbitmq -d -p 15672:15672 -p 5672:5672 rabbitmq:management
f890fbe22ed1c91e6ed8b3617345399070781959d62d3d18f4c881b618fcebbc
```

### 启动 停止 重启

```
docker start rabbitmq
docker stop rabbitmq
docker restart rabbitmq
```

### 控制台检查

浏览器打开：http://localhost:15672/
guest：guest

![控制台图预览1](/images/posts/20191219/01.png)<br>

可以愉快的玩耍了！

