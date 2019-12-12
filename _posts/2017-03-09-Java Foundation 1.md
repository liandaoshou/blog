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

* final：最后的，锁定，防止修改，

    final类不能被继承，没有子类，final类中的方法默认是final的。
    
    final方法不能被子类所覆盖，一旦定义，子类中不允许出现同名方法，可以被继承。
    
    final成员变量表示常量，只能被赋值一次，赋值后值不再改变。
        
```$xslt
package vip.liandao.javabasis.controller;

public class UseFinal {
    private final String a = "cc";
    public final int E;

    public UseFinal(int x) {
        E = x;
    }

    public static void main(String[] args) {
        UseFinal c = new UseFinal(1);
        System.out.println(c.E);

        UseFinal1 u = new UseFinal1(2);
        u.ia("1");
        u.ia(1);
        u.ia();
        ff(3);


        // Non-static field 'a' cannot be referenced from a static context
        // a = "567";
        // final a = "777";
    }

    public static final void ia() {
        System.out.println("iaia");
    }

    // final 方法可以被重写
    public static void ia(String a) {
        System.out.println("string");
    }

    public static void ff(final int i) {
        System.out.println(i);
        // i= 2;
        // Cannot assign a value to final variable 'i'
    }
}

final class info {

}

//class info2 extends info {
//// Cannot inherit from final 'vip.liandao.javabasis.controller.info'
//}

class UseFinal1 extends UseFinal{
//    public static final void ia() {
//        // 'ia()' cannot override 'ia()' in 'vip.liandao.javabasis.controller.UseFinal'; overridden method is final
//    }
    public UseFinal1(int x) {
        super(x);
    }

    public static void ia(int a) {
        System.out.println("int");
    }
}
```
        
* abstract： 抽象的

抽象类和抽象方法

抽象方法不能有方法主体

抽象类不能被实例化，抽象类中方法未具体化

抽象类中不一定包含abstract，可以没有abstract方法

一旦类中包含abstract方法，类必须是abstract类

```$xslt
package vip.liandao.javabasis.controller;

public class UseAbstract {
    public static void main(String[] args) {
        a aa = new a();
        aa.y();
        aa.z();
    }
}

abstract class x {
    abstract void y();

    void z() {
        System.out.println("zz");
    }
}

class a extends x{

    @Override
    void y() {
        System.out.println("yy");
    }

//    void z() {
//        System.out.println("2zz");
//    }
}

```

* static 

静态变量：

static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

静态方法：

static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。


* synchronized 关键字声明的方法同一时间只能被一个线程访问。synchronized 修饰符可以应用于四个访问修饰符。


* transient
序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。

该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
```$xslt
public transient int limit = 55;   // 不会持久化
public int b; // 持久化
```

* volatile

volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。
一个 volatile 对象引用可能是 null。