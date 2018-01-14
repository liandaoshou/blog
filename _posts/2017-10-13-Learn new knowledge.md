---
layout: post
title:  "新建一个laravel项目!"
date:   2017-10-13 22:03:54 +0800
categories: Learn new knowledge
tag: php
---

本地环境搭建 
mysql
php > 7 
 - PHP OpenSSL 扩展
 - PHP PDO 扩展
 - PHP Mbstring 扩展
 - PHP Tokenizer 扩展
 - PHP XML 扩展
    
php新版本 > 7 快速启动，可以抛弃集成环境包，直接启动
    `php - S localhost:8000` 

Composer 

安装Laravel installer
    `composer global require "laravel/installer"`

安装完成后，新建项目
    `laravel new project`

项目创建后，cd project 修改文件名 将文件.env.example  修改为.env 
修改成功后，生成项目KEY
    `php artisan key:generate`

生成成功后，运行项目
    `php artisan serve`

然后就可以看到欢迎界面了