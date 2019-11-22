---
layout: post
title:  "Java基础二（基础语法等）"
date:   2017-03-09 10:00:03 +0800
categories: Java based 2
tag: Java
---

### 基础语法

* 大小写敏感
* 类名 大写开头 驼峰
* 方法名 小写开头 驼峰
* 文件名 与类名一致 大写开头驼峰
* 主方法入口 public static void mian(String []args) 
    由mian方法为入口，开始执行


### Java 标识符
    所有标识符都应该以字母，$，_开始
    关键字不能为标识符
    大小写敏感
    
### Java 修饰符
    访问类的
        public  公共
        private  私有
        protected 保护的
        default 其他

修饰符     | 状态 | 当前类 | 同一包内 | 子孙类 | 其他包 
--------- | ---- | ------------ | --------- | ------ | ------------
public    | 公共  | 当前类可访问 | 同一包可访问 | 子类可访问 | 其他包可访问
private   | 私有 | 当前类可访问 | 同一包不可访问 | 子类不可访问 | 其他包不可访问
protected | 受保护 | 当前类可访问 | 同一包可访问 | 子类可访问 | 其他包不可访问
default   | 其他  | 当前类可访问 | 同一包可访问 | 子类不可访问 | 其他包不可访问
    非访问类的
        final  
        abstract
        static
        synchronized
    
    final ： 方法锁定，防止任何继承类修改，