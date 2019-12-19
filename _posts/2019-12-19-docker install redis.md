---
layout: post
title:  "docker安装redis"
date:   2019-12-19 15:30:00 +0800
categories: docker 
tag: docker
---
## docker安装redis

### 查找

```
docker search redis
NAME                             DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
redis                            Redis is an open source key-value store that…   7635                [OK]
bitnami/redis                    Bitnami Redis Docker Image                      134                                     [OK]
sameersbn/redis                                                                  78                                      [OK]
grokzen/redis-cluster            Redis cluster 3.0, 3.2, 4.0 & 5.0               62
rediscommander/redis-commander   Alpine image for redis-commander - Redis man…   32                                      [OK]
kubeguide/redis-master           redis-master with "Hello World!"                31
redislabs/redis                  Clustered in-memory database engine compatib…   24
arm32v7/redis                    Redis is an open source key-value store that…   19
oliver006/redis_exporter          Prometheus Exporter for Redis Metrics. Supp…   18
redislabs/redisearch             Redis With the RedisSearch module pre-loaded…   17
webhippie/redis                  Docker images for Redis                         10                                      [OK]
s7anley/redis-sentinel-docker    Redis Sentinel                                  9                                       [OK]
insready/redis-stat              Docker image for the real-time Redis monitor…   9                                       [OK]
bitnami/redis-sentinel           Bitnami Docker Image for Redis Sentinel         8                                       [OK]
redislabs/redisgraph             A graph database module for Redis               8                                       [OK]
arm64v8/redis                    Redis is an open source key-value store that…   7
redislabs/redismod               An automated build of redismod - latest Redi…   5                                       [OK]
centos/redis-32-centos7          Redis in-memory data structure store, used a…   4
frodenas/redis                   A Docker Image for Redis                        2                                       [OK]
circleci/redis                   CircleCI images for Redis                       2                                       [OK]
runnable/redis-stunnel           stunnel to redis provided by linking contain…   1                                       [OK]
wodby/redis                      Redis container image with orchestration        1                                       [OK]
tiredofit/redis                  Redis Server w/ Zabbix monitoring and S6 Ove…   1                                       [OK]
xetamus/redis-resource           forked redis-resource                           0                                       [OK]
cflondonservices/redis           Docker image for running redis                  0
```

### 获取

```
docker pull redis
Using default tag: latest
latest: Pulling from library/redis
000eee12ec04: Pull complete                                                                                                                        5cc53381c195: Pull complete                                                                                                                        48bb7bcb5fbf: Pull complete                                                                                                                        ef8a890bb1c2: Pull complete                                                                                                                        32ada9c6fb0d: Pull complete                                                                                                                        76e034b0f296: Pull complete                                                                                                                        Digest: sha256:1eedfc017b0cd3e232878ce38bd9328518219802a8ef37fe34f58dcf591688ef
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest
```

### 安装
```
docker run -p 6379:6379 -d redis:latest redis-server
4368b2db0c26debe1ab59b19a240182b90bdf9abc5feb9f68958a25112ee8e2c
```

### 检查
```
docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                                                                        NAMES
4368b2db0c26        redis:latest          "docker-entrypoint.s…"   40 seconds ago      Up 39 seconds       0.0.0.0:6379->6379/tcp 

```

### 几种连接方式

```
docker exec -ti 4368b2db0c26 redis-cli
docker exec -ti 4368b2db0c26 redis-cli -h localhost -p 6379 
docker exec -ti 4368b2db0c26 redis-cli -h 127.0.0.1 -p 6379 


docker exec -it redis_s redis-cli

远程连接
docker exec -it redis_s redis-cli -h 192.168.1.100 -p 6379 -a your_password //如果有密码 使用 -a参数
```
