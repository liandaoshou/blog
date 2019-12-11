---
layout: post
title:  "Win10安装docker及常用操作"
date:   2019-12-10 09:20:00 +0800
categories: Win10 docker
tag: docker
---

#安装
Win10需要开启Hyper-V

选择应用和功能->启用或关闭Windows功能<br>
选中Hyper-V点击确定，电脑重启配置<br>
配置完成后，安装Toolbox<br>
https://www.docker.com/get-docker<br>
安装完成后docker图标就会出来，可以用docker version查看版本号。


```
#docker version
Client: Docker Engine - Community
 Version:           19.03.5
 API version:       1.40
 Go version:        go1.12.12
 Git commit:        633a0ea
 Built:             Wed Nov 13 07:22:37 2019
 OS/Arch:           windows/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.5
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.12
  Git commit:       633a0ea
  Built:            Wed Nov 13 07:29:19 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
```

#常用操作
1. 容器

```
docker run -it ubuntu /bin/bash
```

参数说明：

* -i: 交互式操作。
* -t: 终端。
* ubuntu: ubuntu 镜像。
* /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

要退出终端，直接输入 exit:


查看所有容器

```
docker ps - a
```

启动已经停止的容器

```
docker start "ID"
```

后台运行
```
docker run -itd --name ubuntu-test ubuntu /bin/bash
```
加了-d参数默认不会进入容器，想要进入容器运行 docker exec

停止一个容器

```
docker stop "ID"
```

停止的容器可以通过restart启动

```
docker restart "ID"
```

进入容器
```
docker attach "ID"
or 
docker exec -it "ID" /bin/bash
```

推荐使用docker exec 不会因为退出容器导致容器停止

参数说明可以使用 docker exec --help 查看

导出容器
```
docker export "ID" > ubuntu.tar
```
会将容器快照到本地文件

导入容器快照 可以通过url或者目录导入
```
docker import "URL"
```

删除容器
```
docker rm -f "ID"
```

清理所有处于终止状态的容器
```
docker container prune
```

运行web应用

```
docker pull training/webapp
docker run -d -P training/webapp python app.py
```

-d 容器运行在后台
-P 端口映射

查看web应用

```
docker ps
```

指定端口

```
docker run -d -p 5000:5000  "应用"
```

查看端口
```
docker port "ID or 容器名"
```

查看日志

```
docker logs -f "ID"
```

查看进程

```
docker top "容器名"
```

停止
```
docker stop "容器名"
```

查看最后一次创建的容器
```
docker ps -l
```

删除
```
docker rm "容器名"
```


2. 镜像
查看本机镜像
```
docker images
```
* REPOSITORY 镜像仓库源
* TAG 镜像标签
* IMAGE ID 镜像ID
* CREATED 镜像创建时间
* SIZE 镜像大小 

同一个仓库源可以有多个TAG，代表仓库源不同的版本
```
docker run -t -i ubuntu:15.10 /bin/bash
```
参数说明<br>
-i 交互式操作<br>
-t 终端<br>
ubuntu:15.10: 这是指用 ubuntu 15.10 版本镜像为基础来启动容器。<br>
/bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

如果不指定镜像版本，docker会使用latest镜像

获取一个新的镜像
```$xslt
docker pull ubuntu:14.10
```
下载完成后可以直接用镜像来运行容器

查找镜像
```$xslt
docker search mysql
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   8922                [OK]
mariadb                           MariaDB is a community-developed fork of MyS…   3135                [OK]
mysql/mysql-server                Optimized MySQL Server Docker images. Create…   659                                     [OK]
percona                           Percona Server is a fork of the MySQL relati…   462                 [OK]
centos/mysql-57-centos7           MySQL 5.7 SQL database server                   65
centurylink/mysql                 Image containing mysql. Optimized to be link…   61                                      [OK]
mysql/mysql-cluster               Experimental MySQL Cluster Docker images. Cr…   59
deitch/mysql-backup               REPLACED! Please use http://hub.docker.com/r…   41                                      [OK]
bitnami/mysql                     Bitnami MySQL Docker Image                      35                                      [OK]
tutum/mysql                       Base docker image to run a MySQL database se…   34
schickling/mysql-backup-s3        Backup MySQL to S3 (supports periodic backup…   28                                      [OK]
prom/mysqld-exporter                                                              23                                      [OK]
linuxserver/mysql                 A Mysql container, brought to you by LinuxSe…   22
centos/mysql-56-centos7           MySQL 5.6 SQL database server                   17
circleci/mysql                    MySQL is a widely used, open-source relation…   16
mysql/mysql-router                MySQL Router provides transparent routing be…   14
arey/mysql-client                 Run a MySQL client from a docker container      13                                      [OK]
openshift/mysql-55-centos7        DEPRECATED: A Centos7 based MySQL v5.5 image…   6
fradelg/mysql-cron-backup         MySQL/MariaDB database backup using cron tas…   4                                       [OK]
genschsa/mysql-employees          MySQL Employee Sample Database                  3                                       [OK]
ansibleplaybookbundle/mysql-apb   An APB which deploys RHSCL MySQL                2                                       [OK]
devilbox/mysql                    Retagged MySQL, MariaDB and PerconaDB offici…   2
jelastic/mysql                    An image of the MySQL database server mainta…   1
monasca/mysql-init                A minimal decoupled init container for mysql    0
widdpim/mysql-client              Dockerized MySQL Client (5.7) including Curl…   0                                       [OK]
```

NAME: 镜像仓库源的名称

DESCRIPTION: 镜像的描述

OFFICIAL: 是否 docker 官方发布

stars: 类似 Github 里面的 star，表示点赞、喜欢的意思。

AUTOMATED: 自动构建。

镜像下载成功后使用镜像
```$xslt
docker run mysql
```

删除镜像
```$xslt
docker rmi mysql
```

更新镜像

当仓库中的镜像不能满足我们的时候，可以使用更新镜像

更新镜像前需要先创建容器
```$xslt
docker run -t -i ubuntu:15.01 /bin/bash
```

容器内使用 apt-get update 更新
提交容器
```$xslt
docker commit -m="has update" -a="test" e218edb10161 runoob/ubuntu:v2
```

-m: 提交的描述信息

-a: 指定镜像作者

e218edb10161：容器 ID

runoob/ubuntu:v2: 指定要创建的目标镜像名

构建镜像
```
docker build
```

3. 仓库
```$xslt
docker search ubuntu
docker pull ubuntu
docker push ubuntu
```


常用命令

docker rmi -f  删除 docker images

容器生命周期管理
```$xslt
run
start/stop/restart
kill
rm
pause/unpause
create
exec

```

容器操作
```$xslt
ps
inspect
top
attach
events
logs
wait
export
port
```

容器rootfs命令
```$xslt
commit
cp
diff
```

镜像仓库
```$xslt
login
pull
push
search
```

本地镜像管理
```$xslt
images
rmi
tag
build
history
save
load
import
info|version
info
version
```

资源

```$xslt
Docker 官方主页: https://www.docker.com
Docker 官方博客: https://blog.docker.com/
Docker 官方文档: https://docs.docker.com/
Docker Store: https://store.docker.com
Docker Cloud: https://cloud.docker.com
Docker Hub: https://hub.docker.com
Docker 的源代码仓库: https://github.com/moby/moby
Docker 发布版本历史: https://docs.docker.com/release-notes/
Docker 常见问题: https://docs.docker.com/engine/faq/
Docker 远端应用 API: https://docs.docker.com/develop/sdk/

Docker 国内镜像
阿里云的加速器：https://help.aliyun.com/document_detail/60750.html
网易加速器：http://hub-mirror.c.163.com
官方中国加速器：https://registry.docker-cn.com
ustc 的镜像：https://docker.mirrors.ustc.edu.cn
daocloud：https://www.daocloud.io/mirror#accelerator-doc（注册后使用）
```