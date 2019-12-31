---
layout: post
title:  "JVM 类加载机制"
date:   2017-03-13 09:37:09 +0800
categories: Java JVM Class 
tag: Java
---
## JVM 类加载机制

JVM 类加载机制分为五个部分：加载、验证、准备、解析、初始化。

类的生命周期： 加载-> 验证 -> 准备 -> 解析 -> 初始化 -> 使用 -> 卸载 

![JVM 类加载机制](/images/posts/20170312/02.png)<br>

### 加载

加载阶段会在内存中生成一个代表这个类的java.lang.class对象，作为这个类的各种数据的入口。
主要这类不一定非要从Class文件获取，这类可以从包中读取，也可以在运行时计算生成（动态代理），
也可以由其他文件生成（比如JSP文件转换称为对应的Class类）。

### 验证

验证阶段主要目的是为了确保Class文件的字节流中包含信息是否符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。

### 准备

准备阶段是正式为类变量分配内存并设置类变量的初始阶段，即在方法区中分配这些变量所使用的内存空间。

注意这里所说的初始值概念，比如一个类变量定义为：

    `public static int v = 8080;`
    
实际上变量 v 在准备阶段过后的初始值为 0 而不是 8080，将 v 赋值为 8080 的 put static 指令是程序被编译后，存放于类构造器<client>方法之中。但是注意如果声明为：

    `public static final int v = 8080;`
    
在编译阶段会为 v 生成 ConstantValue 属性，在准备阶段虚拟机会根据 ConstantValue 属性将 v赋值为 8080。

### 解析

解析阶段就是指虚拟机将常量池中符号替换为直接引用的过程。符号引用就是class文件中的：CONSTANT_Class_info、CONSTANT_Field_info、CONSTANT_Method_info等类型的常量。

### 符号引用

符号引用与虚拟机实现的布局无关，引用的目标并不一定要已经加载到内存中。各种虚拟机实现的内存布局可以各不相同，但是它们能接受的符号引用必须是一致的，因为符号引用的字面量形式明确定义在 Java 虚拟机规范的 Class 文件格式中。

### 直接引用

直接引用可以是指向目标的指针，相对偏移量或是一个能间接定位到目标的句柄。如果有了直接引用，那引用的目标必定已经在内存中存在。

### 初始化

初始化阶段是类加载最后一个阶段，前面的类加载阶段之后，除了在加载阶段可以自定义类加载器以外，其它操作都由 JVM 主导。到了初始阶段，才开始真正执行类中定义的 Java 程序代码。

## 类加载

### 类构造器

初始化阶段是执行类构造器client方法的过程，client方法是由编译器自动收集类中的类变量的赋值操作和静态语句块中的语句合并而成的。
虚拟机会保证子client方法执行之前，父类的client方法已执行完毕，如果一个类中没有对静态变量赋值也没有静态语句块，那编译器可以不为这个类生成client方法。

<label style="color:red">注意以下几种情况不会执行类初始化：</label>
1. 通过子类引用父类的静态字段，只会触发父类的初始化，不会触发子类的初始化。
2. 定义对象数组，不会触发该类的初始化。
3. 常量再编译期间会存入调用类的常量池中，本质上并没有直接引用定义常量的类，不会触发定义常量所在的类。
4. 通过类名获取Class对象，不会触发类的初始化。
5. 同类Class.forName加载指定类时。，如果指定参数initialize为false时，也不会触发类初始化，其实这个参数是告诉虚拟机，是否要对类进行初始化。
6. 通过classLoader默认的loadClass方法，也不会触发初始化动作。


### 类加载器

* 启动类加载器 （Bootstrap ClassLoader）

负责加载JAVA_HOME\lib目录中的，或通过-Xbootclasspath参数指定路径中，且被虚拟机认可的类（按文件名识别，如rt.jar）。

* 扩展类加载器 （Extension ClassLoader）

负责加载JAVA_HOME\lib\ext目录中的，或通过java.ext.dirs系统变量指定路径中的类库。

* 应用程序类加载器 （Application ClassLoader）

负责加载用户路径（classpath）上的类库。
JVM通过双亲委派模型进行类的加载，当然我们也可以通过继承java.lang.ClassLoader实现自定义类加载器。

        自定义加载器 ->

                           应用程序类加载器 ->  扩展类加载器 -> 启动类加载器
        自定义加载器 ->

## 双亲委派

当一个类收到类加载请求，他首先不会尝试自己去加载类，而是把请求委派给父类去完成，每一个层次类加载器都是如此。
所有的加载请求都应该传送到启动类加载其中，只有当父类加载器反馈自己无法完成这个请求的时候（在它的加载路径下没有找到所需加载的Class），
子类加载器才会尝试自己的加载。

采用双亲委派的好处是比如加载位于rt.jar包中的类，java.lang.Object，不管是那个加载器加载这个类，最终都会委托顶层的启动类加载器进行加载，这样就保证不同类加载器最终得到都是同样一个Object对象。

![JVM双亲委派](/images/posts/20170312/03.png)<br>


## OSGI 

OSGI  open service gateway initiative，是面向Java的动态模型系统，是Java动态化模块化系统的一系列规范。

* 动态改变构造
    
    
    OSGI服务平台提供在多种网络设备上，无需重启的动态改变构造功能，为了最小化耦合度和初始这些耦合度可管理，OSGI技术提供一种面向服务的架构，使这些组件动态的发现对方。
    
* 模块化编程与热插拔
    
    
    OSGI 旨在为实现Java程序的模块化编程提供基础条件，基于OSGI的程序很可能可以实现模块级的热插拔功能，当程序升级更新时，可以只停用、重新安装然后启动程序的其中一部分，这对企业级程序开发来讲很有诱惑性。
    OSGI 描绘了一个很美好的模块化开发目标，而且定义了实现这个目标的所需要服务与架构，同时也有成熟的框架进行实现支持。但并非所有的应用都适合采用 OSGi 作为基础架构，它在提供强大功能同时，也引入了额外的复杂度，因为它不遵守了类加载的双亲委托模型。
    
### 为什么叫双亲委派机制？

网上查了一部分资料称：相对于AppClassLoader应用程序类加载器，加载工程项目下的CLAASSPATH路径下的类，会委派ExtClassLoader标准扩展类加载器，
这时ExtClassLoader会再次委托BootstrapClassLoader启动类加载器。
BootstrapClassLoader时Java虚拟机第一个类加载器，不能再向上委托了，这个过程一共委托了两次，所以称为双亲委派。（存疑）