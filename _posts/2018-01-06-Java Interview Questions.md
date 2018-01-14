---
layout: post
title:  "Java 面试题整理"
date:   2018-01-06 13:27:00 +0800
categories: Java Interview Questions
tag: Java
---

JavaEE 企业
JavaSE 标准
JavaME 微型

JRE 包含 JVM
JDK 包含 JRE

Java程序初始化的顺序是怎么样的？
初始化一般遵循三个原则：
1.静态对象（变量）优先于非静态对象（变量）初始化，其中静态对象（变量）只初始化一次，而非静态对象（变量）可能会初始化多次。
2.父类优先于子类进行初始化。
3.按照成员变量定于顺序进行初始化。
父类静态变量、父类静态代码块、子类静态变量、子类静态变量代码块、父类非静态变量、父类非静态代码块、父类构造函数、子类非静态变量、子类非静态代码块、子类构造函数

变量的类型：
成员变量、静态变量、局部变量

成员变量的作用域
public 公共 当前类可访问 同一包可访问 子类可访问 其他包可访问
private 私有 当前类可访问 同一包不可访问 子类不可访问 其他包不可访问
protected 受保护 当前类可访问 同一包可访问 子类可访问 其他包不可访问
default 其他 当前类可访问 同一包可访问 子类不可访问 其他包不可访问

public abstract final 可以修饰类

构造函数：
1.构造函数必须与类名相同，并且不能有返回值。
2.每个类可以有多个构造函数，没有提供的时候，编译器会自动提供一个没有参数的默认的构造函数，如果写了构造函数，就不会再创建构造函数了。
3.构造函数不能被继承，不能被覆盖，但是构造函数能够被重载。


面向对象的特征和原则
特征：继承、封装、多态、抽象
原则：单一职责原则、依赖原则、接口分离原则、替换原则、开放封闭原则

多态的表现方式：重载、覆盖
重载：同一个类中有多个同名方法，在编译的时候确定到底调用那个方法。
覆盖：子类可以覆盖父类的方法，在程序运行时动态绑定。

重载和覆盖的区别
1.覆盖是子类和父类的关系是垂直关系，重载是同一个类的水平关系。
2.覆盖只能由一个方法或一对方法产生关系，重载是多个方法之间的关系。
3.覆盖要求参数列表相同，重载要求参数列表不同。

内部类由哪些
静态内部类
成员（普通）内部类
局部内部类
外部类
匿名内部类


break、continue、return区别
break：结束当前循环
continue：跳过当前本次循环，进入当前下次循环
return：直接结束输出

final、finally、finalize区别
final：可以声明属性、方法和类，表示属性不可变、方法不可覆盖、类不可被继承。
finally：是try catch的一部分，用于标识必须被执行
finalize：Object的一个方法，垃圾回收器执行被调用回收对象的finalize（），可以覆盖来实现其他资源的回收。

switch 1.7前只能使用枚举的或者Integer包装类，1.7后支持String

volatile有什么作用
修饰成员变量后，每次都直接从内存中获取，不会从缓存中获取，但是他并不能保证原子性，一般情况下不能替换sychronized，并且volatile会阻止编译器对代码的优化，会降低程序的执行效率。

strictfp关键字
确保浮点运算精准

Java的基本数据类型
int         4 
short       2
long        8
byte        1
float       4   
double      8   
char        2
boolean     1

const常量：只允许读不允许修改

值传递与引用传递有哪些区别
值传递：开辟一个新的存储单元
引用传递：指向同一个存储单元

Math类中round、ceil、floor
round四舍五入
ceil向上取整
floor向下取整


i++ 和 ++i的区别
i++ 执行完后自增
++i 先自增再执行

==、equals、hashcode 区别
== 运算检测两个变量值是否相等，仅用基本数据类型，如果是对象就会比较内存地址
equals 比较对象内容
hashcode 将内存地址转换为int值，如果没有重写所有对象都是不等的。

String、StringBuffer、StringBuilder和StringTokenizer的区别
String对象是不可变对象，一旦创建不可变更。
StringBuffer拼接字符串，创建临时的对象，字符串缓冲区，是线程安全的。
StringBuilder也是字符串缓冲区，但是不是线程安全的。
效率stringbuider最高，stringBuffer次之，String最低。
StringTokenizer是分割字符串的工具类。

finally在代码什么时候被执行
return之前执行，一定会被执行吗？
报错就不会被执行，System.exit(0);也不会被执行。

异常处理的原理
异常是指程序运行时（非编译时）所发生的非正常情况或错误，Java把异常当对象处理，定义了一个基类java.lang.Throwable,Java异常分为Error（错误）和Exception（异常）两大类。开发也可以自己创建异常类。


Throwable类中常用的方法
像catch(Exception e)中的Exception就是异常的变量类型，e则是形参。通常在进行异常输出时有如下几个方法可用：
e.getCause():返回抛出异常的原因。
e.getMessage():返回异常信息。
e.printStackTrace():发生异常时，跟踪堆栈信息并输出。


常见异常：
java.lang.IllegalAccessError：违法访问错误。当一个应用试图访问、修改某个类的域（Field）或者调用其方法，但是又违反域或方法的可见性声明，则抛出该异常。
java.lang.InstantiationError：实例化错误。当一个应用试图通过Java的new操作符构造一个抽象类或者接口时抛出该异常.
java.lang.OutOfMemoryError：内存不足错误。当可用内存不足以让Java虚拟机分配给一个对象时抛出该错误。
java.lang.StackOverflowError：堆栈溢出错误。当一个应用递归调用的层次太深而导致堆栈溢出或者陷入死循环时抛出该错误。
java.lang.ClassCastException：类造型异常。假设有类A和B（A不是B的父类或子类），O是A的实例，那么当强制将O构造为类B的实例时抛出该异常。该异常经常被称为强制类型转换异常。
java.lang.ClassNotFoundException：找不到类异常。当应用试图根据字符串形式的类名构造类，而在遍历CLASSPAH之后找不到对应名称的class文件时，抛出该异常。
java.lang.ArithmeticException：算术条件异常。譬如：整数除零等。
java.lang.ArrayIndexOutOfBoundsException：数组索引越界异常。当对数组的索引值为负数或大于等于数组大小时抛出。
java.lang.IndexOutOfBoundsException：索引越界异常。当访问某个序列的索引值小于0或大于等于序列大小时，抛出该异常。
java.lang.InstantiationException：实例化异常。当试图通过newInstance()方法创建某个类的实例，而该类是一个抽象类或接口时，抛出该异常。
java.lang.NoSuchFieldException：属性不存在异常。当访问某个类的不存在的属性时抛出该异常。
java.lang.NoSuchMethodException：方法不存在异常。当访问某个类的不存在的方法时抛出该异常。
java.lang.NullPointerException：空指针异常。当应用试图在要求使用对象的地方使用了null时，抛出该异常。譬如：调用null对象的实例方法、访问null对象的属性、计算null对象的长度、使用throw语句抛出null等等。
java.lang.NumberFormatException：数字格式异常。当试图将一个String转换为指定的数字类型，而该字符串确不满足数字类型要求的格式时，抛出该异常。
java.lang.StringIndexOutOfBoundsException：字符串索引越界异常。当使用索引值访问某个字符串中的字符，而该索引值小于0或大于等于序列大小时，抛出该异常。
其他异常：
java.lang.AbstractMethodError：抽象方法错误。当应用试图调用抽象方法时抛出。
java.lang.AssertionError：断言错。用来指示一个断言失败的情况。
java.lang.ClassCircularityError：类循环依赖错误。在初始化一个类时，若检测到类之间循环依赖则抛出该异常。
java.lang.ClassFormatError：类格式错误。当Java虚拟机试图从一个文件中读取Java类，而检测到该文件的内容不符合类的有效格式时抛出。
java.lang.Error：错误。是所有错误的基类，用于标识严重的程序运行问题。这些问题通常描述一些不应被应用程序捕获的反常情况。
java.lang.ExceptionInInitializerError：初始化程序错误。当执行一个类的静态初始化程序的过程中，发生了异常时抛出。静态初始化程序是指直接包含于类中的static语句段。
java.lang.IncompatibleClassChangeError：不兼容的类变化错误。当正在执行的方法所依赖的类定义发生了不兼容的改变时，抛出该异常。一般在修改了应用中的某些类的声明定义而没有对整个应用重新编译而直接运行的情况下，容易引发该错误。
java.lang.InternalError：内部错误。用于指示Java虚拟机发生了内部错误。
java.lang.LinkageError：链接错误。该错误及其所有子类指示某个类依赖于另外一些类，在该类编译之后，被依赖的类改变了其类定义而没有重新编译所有的类，进而引发错误的情况。
java.lang.NoClassDefFoundError：未找到类定义错误。当Java虚拟机或者类装载器试图实例化某个类，而找不到该类的定义时抛出该错误。
java.lang.NoSuchFieldError：域不存在错误。当应用试图访问或者修改某类的某个域，而该类的定义中没有该域的定义时抛出该错误。
java.lang.NoSuchMethodError：方法不存在错误。当应用试图调用某类的某个方法，而该类的定义中没有该方法的定义时抛出该错误。
java.lang.ThreadDeath：线程结束。当调用Thread类的stop方法时抛出该错误，用于指示线程结束。
java.lang.UnknownError：未知错误。用于指示Java虚拟机发生了未知严重错误的情况。
java.lang.UnsatisfiedLinkError：未满足的链接错误。当Java虚拟机未找到某个类的声明为native方法的本机语言定义时抛出。
java.lang.UnsupportedClassVersionError：不支持的类版本错误。当Java虚拟机试图从读取某个类文件，但是发现该文件的主、次版本号不被当前Java虚拟机支持的时候，抛出该错误。
java.lang.VerifyError：验证错误。当验证器检测到某个类文件中存在内部不兼容或者安全问题时抛出该错误。
java.lang.VirtualMachineError：虚拟机错误。用于指示虚拟机被破坏或者继续执行操作所需的资源不足的情况。
java.lang.ArrayStoreException：数组存储异常。当向数组中存放非数组声明类型对象时抛出。
java.lang.CloneNotSupportedException：不支持克隆异常。当没有实现Cloneable接口或者不支持克隆方法时,调用其clone()方法则抛出该异常。
java.lang.EnumConstantNotPresentException：枚举常量不存在异常。当应用试图通过名称和枚举类型访问一个枚举对象，但该枚举对象并不包含常量时，抛出该异常。
java.lang.Exception：根异常。用以描述应用程序希望捕获的情况。
java.lang.IllegalAccessException：违法的访问异常。当应用试图通过反射方式创建某个类的实例、访问该类属性、调用该类方法，而当时又无法访问类的、属性的、方法的或构造方法的定义时抛出该异常。
java.lang.IllegalMonitorStateException：违法的监控状态异常。当某个线程试图等待一个自己并不拥有的对象（O）的监控器或者通知其他线程等待该对象（O）的监控器时，抛出该异常。
java.lang.IllegalStateException：违法的状态异常。当在Java环境和应用尚未处于某个方法的合法调用状态，而调用了该方法时，抛出该异常。
java.lang.IllegalThreadStateException：违法的线程状态异常。当县城尚未处于某个方法的合法调用状态，而调用了该方法时，抛出异常。
java.lang.InterruptedException：被中止异常。当某个线程处于长时间的等待、休眠或其他暂停状态，而此时其他的线程通过Thread的interrupt方法终止该线程时抛出该异常。
java.lang.NegativeArraySizeException：数组大小为负值异常。当使用负数大小值创建数组时抛出该异常。
java.lang.SecurityException：安全异常。由安全管理器抛出，用于指示违反安全情况的异常。
java.lang.TypeNotPresentException：类型不存在异常。

Java IO流
IO流的本质是数据传输，流可以分为两个大类，字节流和字符流。
字节流：8bit，包含两个抽象类
    InputStream（输入流） 
    OutputStream（输出流） 
字符流：16bit，包含两个抽象类
    Reader（输入流） 
    Writer（输出流） 
字节流和字符流的区别是：字节流在处理输入输出时不会用到缓存，而字符流用到了缓存。
流的主要作用为了改善程序的性能并使用方便。


File（String pathname） 根据指定路径创建File对象
createNewFile（） 目录或者文件存在返回false，否则创建文件或文件夹
delete（） 删除文件或文件夹
isFile（） 判断对象是否是文件
isDirectory（） 判断对象是否是文件夹
listFiles（） 若对象代表目录，范围目录内所有文件的File对象
mkdir（） 根据当前对象制定的路径创建目录
exists（） 判断对象对应文件是否存在

Java Socket
Java中Socket可以分为两个类型：
面向连接的Socket通信协议（TCP，传输控制协议）
面向无连接的Socket通信协议（UDP，用户数据报协议）
TCP必须先建立连接，先连接再通信，面向连接，安全可靠，可是效率相对低下。
UDP类似发短信，非面向连接，不安全，数据可能丢失，效率高。

UDP通讯协议的特点：
1.将数据集封装为数据包，面向无连接。
2.每个数据包的大小限制为64K。
3.面对无连接，所以不可靠。
4.因为不需要连接，速度快。
5.UDP通讯部分客户端和服务端，只分发送端与接收端。

UDP发送端使用步骤：
1.建立UDP的服务。
2.准备数据，把数据封装到数据包中，发送端的数据包要带上IP地址和端口号。
3.调用UDP的服务，发送数据。
4.关闭资源。

UDP接收端使用步骤：
1.建立UDP的服务。
2.准备空的数据包接收数据。
3.调用UDP服务接收数据。
4.关闭资源。


TCP通讯协议的特点：
1.TCP是基于IO流的数据传输，面向连接。
2.TCP进行数据传输的时候是没有大小限制的。
3.TCP是面向连接的，通过三次握手机制保证数据的完整性，可靠协议。
4.TCP面向连接的，速度慢。
5.TCP区分客户端和服务端。

TCP的客户端的使用步骤：
1.建立TCP的客户端服务。
2.获取到对应的流对象。
3.写出或读取数据。
4.关闭资源。

ServerSocket的使用步骤：
1.建立TCP服务端的服务。
2.接受客户端的连接产生一个socket。
3.获取对应的流对象或者写出数据。
4.关闭资源。

Java NIO
NIO的目的是为了让Java程序员可以实现高速I/O而无需编写自定义的本机代码。NIO将最耗时的I/O操作（即填充和提取缓冲区）转移回操作系统，因而可以极大的提高速度。
流与块的比较
原来的I/O库与NIO最重要区别是数据打包和传输的方式，I/O是以流的方式处理数据，而NIO是以块的方式处理数据。
通道和缓冲区是NIO中的核心对象，几乎每一个I/O操作中都要使用。



ArrayList、vector、linkedList 区别
ArrayList和vector都是在内存中开辟一块联系的存储空间来存储，都有初始存储空间，当存储元素超过就会扩充，ArrayList扩充为原来的1.5倍，Vector默认扩充为原来2倍（每次扩充可以设置），ArrayList、linkedList非线程安全，vector是线程安全的。LinkedList是有序的，对数据指定位置插入或者删除效率高于其他。

HashMap、HashTable、TreeMap、weakHashMap区别
HashMap可以设置key为Null
HashTable是线程安全的，不允许设置key为Null
LinkedHashMap是有序的
TreeMap自然排序或自定义顺序排列


线程四种状态：运行、就绪、挂起、结束。
Java多线程实现的三种方法
1.继承Thread类，重写run（）方法
2.实现Runnable接口，实现接口的run（）方法
3.实现Callable接口，重写call（）方法，Callable接口属于Executor框架的功能类，Callable执行完后有返回值，其他没有返回值，call方法可以抛出异常，Callable可以拿到Future对象，Future对象表示异步计算的结果，提供检查计算是否完成的方法。

run（）方法和start（）方法有什么区别？
start是启用，run是具体的执行方法，完成实际操作，run方法执行结束后当前线程终止。

多线程同步实现方法有哪些
synchronized
wait()方法与notify()方法
Lock锁

sleep()方法与wait()方法有什么区别
sleep是Thread类定义的方法，wait方法是Object类中定义的方法
sleep必须指定时间，wait方法可以指定时间也可以不定义时间
wait需要通过notify或者notifyAll来唤醒
sleep方法不一定非要定义同步中，wait必须定义在同步中
sleep不会释放锁，wait会释放锁

终止线程方法有哪些
stop()方法和suspend()方法来终止。
stop会导致程序执行的不正确，并且难定位。
调用suspend方法容易发生死锁。
以上两个方法不介意使用。
通过状态位控制线程结束。
使用interrupt方法终止线程

synchronized与Lock有什么异同
用法不同，synchronized可以在方法上也可以在代码块中，Lock需要定义起始和终止位置。
性能不一样Lock在资源竞争激烈情况下性能基本保持稳定，Synchronized性能下降比较快
锁机制不同，synchronized是自动解锁，Lock必须手动释放。

join()方法的作用
调用方法必须先执行完了run方法后才执行join后面的代码，如果join里面有时间，就最长等待多久后执行后面的代码。

springMVC的运行原理
客户端请求提交到分发器，分发器查询一个或多个映射，找到请求的控制器，分发器将请求提交到控制器，控制器调用模型层，分发器找到指定的视图，将视图显示到客户端。
客户端请求提交到DispatcherServlet
由DispatcherServlet控制器查询一个或多个HandlerMapping，找到处理请求的Controller
DispatcherServlet将请求提交到Controller
Controller调用业务逻辑处理后，返回ModelAndView
DispatcherServlet查询一个或多个ViewResoler视图解析器，找到ModelAndView指定的视图
视图负责将结果显示到客户端

spring注解
@Aspect
@Component
@Resource
@Controller
@RequestMapping
@ResponseBody
....

1. mybatis配置
2. SqlMapConfig.xml，此文件作为mybatis的全局配置文件，配置了mybatis的运行环境等信息。
3. mapper.xml文件即sql映射文件，文件中配置了操作数据库的sql语句。此文件需要在SqlMapConfig.xml中加载。
4. 通过mybatis环境等配置信息构造SqlSessionFactory即会话工厂
5. 由会话工厂创建sqlSession即会话，操作数据库需要通过sqlSession进行。
6. mybatis底层自定义了Executor执行器接口操作数据库，Executor接口有两个实现，一个是基本执行器、一个是缓存执行器。
7. Mapped Statement也是mybatis一个底层封装对象，它包装了mybatis配置信息及sql映射信息等。mapper.xml文件中一个sql对应一个Mapped Statement对象，sql的id即是Mapped statement的id。
8. Mapped Statement对sql执行输入参数进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql前将输入的java对象映射至sql中，输入参数映射就是jdbc编程中对preparedStatement设置参数。
9. Mapped Statement对sql执行输出结果进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql后将输出结果映射至java对象中，输出结果映射过程相当于jdbc编程中对结果的解析处理过程。


#TODO
ArrayList的实现原理
以数组实现。节约空间，但数组有容量限制。超出限制时会增加50%容量，用System.arraycopy()复制到新的数组，因此最好能给出数组大小的预估值。默认第一次插入元素时创建大小为10的数组。
按数组下标访问元素—get(i)/set(i,e) 的性能很高，这是数组的基本优势。
直接在数组末尾加入元素—add(e)的性能也高，但如果按下标插入、删除元素—add(i,e), remove(i), remove(e)，则要用System.arraycopy()来移动部分受影响的元素，性能就变差了，这是基本劣势。

HashMap的实现原理
HashMap基于hashing原理，我们通过put()和get()方法储存和获取对象。当我们将键值对传递给put()方法时，它调用键对象的hashCode()方法来计算hashcode，让后找到bucket位置来储存值对象。当获取对象时，通过键对象的equals()方法找到正确的键值对，然后返回值对象。HashMap使用链表来解决碰撞问题，当发生碰撞了，对象将会储存在链表的下一个节点中。 HashMap在每个链表节点中储存键值对对象。
当两个不同的键对象的hashcode相同时会发生什么？ 它们会储存在同一个bucket位置的链表中。键对象的equals()方法用来找到键值对。

HashSet的实现原理
HashSet实现Set接口，由哈希表（实际上是一个HashMap实例）支持。它不保证set 的迭代顺序；特别是它不保证该顺序恒久不变。此类允许使用null元素。
对于HashSet而言，它是基于HashMap实现的，HashSet底层使用HashMap来保存所有元素，因此HashSet 的实现比较简单，相关HashSet的操作，基本上都是直接调用底层HashMap的相关方法来完成。
对于HashSet中保存的对象，请注意正确重写其equals和hashCode方法，以保证放入的对象的唯一性。

LinkedHashMap的实现原理
LinkedHashMap是Hash表和链表的实现，并且依靠着双向链表保证了迭代顺序是插入的顺序。


ConcurrentHashMap的实现原理
数据结构 ConcurrentHashMap的目标是实现支持高并发、高吞吐量的线程安全的HashMap。当然不能直接对整个hashtable加锁，所以在ConcurrentHashMap中，数据的组织结构和HashMap有所区别。
一个ConcurrentHashMap由多个segment组成，每一个segment都包含了一个HashEntry数组的hashtable， 每一个segment包含了对自己的hashtable的操作，比如get，put，replace等操作，这些操作发生的时候，对自己的hashtable进行锁定。由于每一个segment写操作只锁定自己的hashtable，所以可能存在多个线程同时写的情况，性能无疑好于只有一个hashtable锁定的情况。
在ConcurrentHashMap的remove，put操作还是比较简单的，都是将remove或者put操作交给key所对应的segment去做的，所以当几个操作不在同一个segment的时候就可以并发的进行。
而segment中的remove操作除了加锁之外和HashMap中的remove操作基本无异。


spring事务
编程式事务：代码强相关commit rollback
声明式事务：aop


线程池
Java通过Exectutors提供四种线程池
newCachedThreadPool 创建可缓存的线程池，如果线程池长度超过需要处理的，可以灵活回收线程，如果无可回收的则创建新的线程
newFixedThreadPool 创建一个定长的线程池，可以控制线程的最大并发数，超出线程会在队列中等待。
newScheduledThreadPool创建一个定长的线程池，支持顶起及周期性任务执行。
newSingleThreadExecutor创建一个单线程化的线程池，只会用唯一的线程执行，保证所有任务安装指定顺序执行。


AOP
切面编程，不改变原有代码逻辑，可动态的添加日志，安全或异常处理功能。

拦截器、过滤器、监听器


git的常用命令
迁代码 clone 路径 代码路径
git add . 文件添加至缓冲区
git commit -am 本地文件提交
git diff 查看差异
git status 查看是否有修改
git branch 查看分支
git checkout 分支
git checkout -b 分支  创建分支和切换分支
git branch -d 分支  删除分支
git merge 合并分支
git rm 文件名 删除文件
git rm -r * 递归删除
git mv 重命名或移动一个文件


反射
在运行状态都能知道这个类的所有方法和属性，对于任意一个对象，都能调用他的任意方法和属性。
反射机制能做什么？
在运行时判断对象的所属类。
在运行时构造任意一个类的对象。
在运行时判断任意一个类的成员变量和方法。
在运行时调用任意一个对象的方法。
生成动态代理。

amq
MQ
JMS
发送消息的基本步骤：
(1)、创建连接使用的工厂类JMS ConnectionFactory
(2)、使用管理对象JMS ConnectionFactory建立连接Connection，并启动
(3)、使用连接Connection 建立会话Session
(4)、使用会话Session和管理对象Destination创建消息生产者MessageSender
(5)、使用消息生产者MessageSender发送消息
消息接收者从JMS接受消息的步骤
(1)、创建连接使用的工厂类JMS ConnectionFactory
(2)、使用管理对象JMS ConnectionFactory建立连接Connection，并启动
(3)、使用连接Connection 建立会话Session
(4)、使用会话Session和管理对象Destination创建消息接收者MessageReceiver
(5)、使用消息接收者MessageReceiver接受消息，需要用setMessageListener将MessageListener接口绑定到MessageReceiver消息接收者必须实现了MessageListener接口，需要定义onMessage事件方法。

rest接口和API接口

redis
redis-cli
PING
keys * 


linux
find 
nestatus

jvm调优

jvm结构
    JVM主要包括四个部分:
    1.类加载器：在JVM启动时或者在类运行时将需要的class加载到JVM中。
    2.执行引擎：负责执行class文件中包含的字节码指令。
    3.内存区：是在JVM运行的时候操作所分配的内存区。运行时内存区主要可以划分为5个区域
        方法区(Method Area)：用于存储类结构信息的地方，包括常量池、静态变量、构造函数等。虽然JVM规范把方法区描述为堆的一个逻辑部分， 但它却有个别名non-heap（非堆），所以大家不要搞混淆了。方法区还包含一个运行时常量池。
        java堆(Heap)：存储java实例或者对象的地方。这块是GC的主要区域（后面解释）。从存储的内容我们可以很容易知道，方法区和堆是被所有java线程共享的。
        java栈(Stack)：java栈总是和线程关联在一起，每当创建一个线程时，JVM就会为这个线程创建一个对应的java栈。在这个java栈中又会包含多个栈帧，每运行一个方法就创建一个栈帧，用于存储局部变量表、操作栈、方法返回值等。每一个方法从调用直至执行完成的过程，就对应一个栈帧在java栈中入栈到出栈的过程。所以java栈是现成私有的。
        程序计数器(PC Register)：用于保存当前线程执行的内存地址。由于JVM程序是多线程执行的（线程轮流切换），所以为了保证线程切换回来后，还能恢复到原先状态，就需要一个独立的计数器，记录之前中断的地方，可见程序计数器也是线程私有的。
        本地方法栈(Native Method Stack)：和java栈的作用差不多，只不过是为JVM使用到的native方法服务的。
    4.本地方法接口：主要是调用C或C++实现的本地方法及返回结果。

内存分配
静态内存和动态内存。很容易理解，编译时就能够确定的内存就是静态内存，即内存是固定的，系统一次性分配，比如int类型变量；动态内存分配就是在程序执行时才知道要分配的存储空间大小，比如java对象的内存空间。根据上面我们知道，java栈、程序计数器、本地方法栈都是线程私有的，线程生就生，线程灭就灭，栈中的栈帧随着方法的结束也会撤销，内存自然就跟着回收了。所以这几个区域的内存分配与回收是确定的，我们不需要管的。但是java堆和方法区则不一样，我们只有在程序运行期间才知道会创建哪些对象，所以这部分内存的分配和回收都是动态的。一般我们所说的垃圾回收也是针对的这一部分。
总之Stack的内存管理是顺序分配的，而且定长，不存在内存回收问题；而Heap 则是为java对象的实例随机分配内存，不定长度，所以存在内存分配和回收的问题。

垃圾检测、回收算法
引用计数法：给一个对象添加引用计数器，每当有个地方引用它，计数器就加1；引用失效就减1。
如果有两个对象A和B，互相引用，除此之外，没有其他任何对象引用它们，实际上这两个对象已经无法访问，即是我们说的垃圾对象。但是互相引用，计数不为0，导致无法回收，所以还有另一种方法：
可达性分析算法：以根集对象为起始点进行搜索，如果有对象不可达的话，即是垃圾对象。这里的根集一般包括java栈中引用的对象、方法区常量池中引用的对象
本地方法中引用的对象等。
总之，JVM在做垃圾回收的时候，会检查堆中的所有对象是否会被这些根集对象引用，不能够被引用的对象就会被垃圾收集器回收。一般回收算法也有如下几种：

1.标记-清除（Mark-sweep）
算法和名字一样，分为两个阶段：标记和清除。标记所有需要回收的对象，然后统一回收。这是最基础的算法，后续的收集算法都是基于这个算法扩展的。
不足：效率低；标记清除之后会产生大量碎片。
2.复制（Copying）
此算法把内存空间划为两个相等的区域，每次只使用其中一个区域。垃圾回收时，遍历当前使用区域，把正在使用中的对象复制到另外一个区域中。此算法每次只处理正在使用中的对象，因此复制成本比较小，同时复制过去以后还能进行相应的内存整理，不会出现“碎片”问题。当然，此算法的缺点也是很明显的，就是需要两倍内存空间。
3.标记-整理（Mark-Compact）
此算法结合了“标记-清除”和“复制”两个算法的优点。也是分两阶段，第一阶段从根节点开始标记所有被引用对象，第二阶段遍历整个堆，把清除未标记对象并且把存活对象“压缩”到堆的其中一块，按顺序排放。此算法避免了“标记-清除”的碎片问题，同时也避免了“复制”算法的空间问题。
4.分代收集算法
这是当前商业虚拟机常用的垃圾收集算法。分代的垃圾回收策略，是基于这样一个事实：不同的对象的生命周期是不一样的。因此，不同生命周期的对象可以采取不同的收集方式，以便提高回收效率。
为什么要运用分代垃圾回收策略？在java程序运行的过程中，会产生大量的对象，因每个对象所能承担的职责不同所具有的功能不同所以也有着不一样的生命周期，有的对象生命周期较长，比如Http请求中的Session对象，线程，Socket连接等；有的对象生命周期较短，比如String对象，由于其不变类的特性，有的在使用一次后即可回收。试想，在不进行对象存活时间区分的情况下，每次垃圾回收都是对整个堆空间进行回收，那么消耗的时间相对会很长，而且对于存活时间较长的对象进行的扫描工作等都是徒劳。因此就需要引入分治的思想，所谓分治的思想就是因地制宜，将对象进行代的划分，把不同生命周期的对象放在不同的代上使用不同的垃圾回收方式。
如何划分？将对象按其生命周期的不同划分成：年轻代(Young Generation)、年老代(Old Generation)、持久代(Permanent Generation)。其中持久代主要存放的是类信息，所以与java对象的回收关系不大，与回收息息相关的是年轻代和年老代。

年轻代：是所有新对象产生的地方。年轻代被分为3个部分——Enden区和两个Survivor区（From和to）当Eden区被对象填满时，就会执行Minor GC。并把所有存活下来的对象转移到其中一个survivor区（假设为from区）。Minor GC同样会检查存活下来的对象，并把它们转移到另一个survivor区（假设为to区）。这样在一段时间内，总会有一个空的survivor区。经过多次GC周期后，仍然存活下来的对象会被转移到年老代内存空间。通常这是在年轻代有资格提升到年老代前通过设定年龄阈值来完成的。需要注意，Survivor的两个区是对称的，没先后关系，from和to是相对的。
年老代：在年轻代中经历了N次回收后仍然没有被清除的对象，就会被放到年老代中，可以说他们都是久经沙场而不亡的一代，都是生命周期较长的对象。对于年老代和永久代，就不能再采用像年轻代中那样搬移腾挪的回收算法，因为那些对于这些回收战场上的老兵来说是小儿科。通常会在老年代内存被占满时将会触发Full GC,回收整个堆内存。
持久代：用于存放静态文件，比如java类、方法等。持久代对垃圾回收没有显著的影响。

分代里涉及了前面几种算法。年轻代：涉及了复制算法；年老代：涉及了“标记-整理（Mark-Sweep）”的算法。

垃圾收集器


类加载的步骤：
1.装载，根据查找路径找到对应的class文件然后导入。
2.链接
    检查：检查待加载的class文件正确性
    准备：给类中的静态变量分配存储空间
    解析：将符号引用转换为直接引用
3.初始化，将静态变量和静态代码块执行初始化工作。

类的生命周期：
　　加载 loading
　　验证 verification
　　准备 preparation
　　解析 resolution
　　初始化 initialization
　　使用 using
　　卸载 unloading

GC
GC是JVM内部的一个进程，回收无效对象的内存用于将来的分配。不能保证GC的必然执行，只能调用System.gc()或者Runtime.getRuntime().gc()，但是执行时，会造成所有的响应，去查看是否有内存需要回收，所以无必要不能频繁使用。

Java内存泄露
不再使用的对象或者变量还在内存中占有存储空间。
内存泄露主要有两种情况，一个是堆中申请的空间没有被释放，二是对象已不再使用，但还在内存中保留。
1.静态集合类，例如HashMap和Vector，如果这些容器是静态的，在程序结束前不能释放，就会造成内存泄露。
2.各种连接，数据库连接，网络连接IO连接，连接后不及时释放，会造成大量的对象无法被回收。
3.监听器，若不及时释放也会导致内存泄露。
4.变量不合理的作用域，定义作用范文大于使用范围。
5.不合理的单例模式也可能造成内存泄露。

Java堆栈的区别
堆和栈都是内存中存放数据的地方。
栈存放基本数据类型的变量和对象的引用变量。
堆存放引用类型的变量，需要通过new等方式创建的。
堆是先进先出，栈是先进后出。
队列是队头出，队尾入。



常用的加密/解密算法
1.Base64
严格来说Base64并不是一种加密/解密算法，而是一种编码方式。Base64不生成密钥，通过Base64编码后的密文就可以直接“翻译”为明文，但是可以通过向明文中添加混淆字符来达到加密的效果。
2.DES
DES是一种基于56位密钥的对称算法，1976年被美国联邦政府的国家标准局确定为联邦资料处理标准（FIPS），随后在国际上广泛流传开来。现在DES已经不是一种安全的加密算法，已被公开破解，现在DES已经被高级加密标准（AES）所代替。
3.3DES
3DES是DES的一种派生算法，主要提升了DES的一些实用所需的安全性。
4.AES
AES是现在对称加密算法中最流行的算法之一。


设计模式
创建型模式：这些设计模式提供了一种在创建对象的同时隐藏创建逻辑的方式，而不是使用 new 运算符直接实例化对象。这使得程序在判断针对某个给定实例需要创建哪些对象时更加灵活。
    工厂模式（Factory Pattern）
    抽象工厂模式（Abstract Factory Pattern）
    单例模式（Singleton Pattern）
    建造者模式（Builder Pattern）
    原型模式（Prototype Pattern）
结构型模式：这些设计模式关注类和对象的组合。继承的概念被用来组合接口和定义组合对象获得新功能的方式。
    适配器模式（Adapter Pattern）
    桥接模式（Bridge Pattern）
    过滤器模式（Filter、Criteria Pattern）
    组合模式（Composite Pattern）
    装饰器模式（Decorator Pattern）
    外观模式（Facade Pattern）
    享元模式（Flyweight Pattern）
    代理模式（Proxy Pattern）
行为型模式：这些设计模式特别关注对象之间的通信。
    责任链模式（Chain of Responsibility Pattern）
    命令模式（Command Pattern）
    解释器模式（Interpreter Pattern）
    迭代器模式（Iterator Pattern）
    中介者模式（Mediator Pattern）
    备忘录模式（Memento Pattern）
    观察者模式（Observer Pattern）
    状态模式（State Pattern）
    空对象模式（Null Object Pattern）
    策略模式（Strategy Pattern）
    模板模式（Template Pattern）
    访问者模式（Visitor Pattern）
J2EE 模式：这些设计模式特别关注表示层。这些模式是由 Sun Java Center 鉴定的。  
    MVC 模式（MVC Pattern）
    业务代表模式（Business Delegate Pattern）
    组合实体模式（Composite Entity Pattern）
    数据访问对象模式（Data Access Object Pattern）
    前端控制器模式（Front Controller Pattern）
    拦截过滤器模式（Intercepting Filter Pattern）
    服务定位器模式（Service Locator Pattern）
    传输对象模式（Transfer Object Pattern）  
设计模式的六大原则
    1、开闭原则（Open Close Principle）
    开闭原则的意思是：对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。简言之，是为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。
    2、里氏代换原则（Liskov Substitution Principle）
    里氏代换原则是面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。LSP 是继承复用的基石，只有当派生类可以替换掉基类，且软件单位的功能不受到影响时，基类才能真正被复用，而派生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。
    3、依赖倒转原则（Dependence Inversion Principle）
    这个原则是开闭原则的基础，具体内容：针对接口编程，依赖于抽象而不依赖于具体。
    4、接口隔离原则（Interface Segregation Principle）
    这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。它还有另外一个意思是：降低类之间的耦合度。由此可见，其实设计模式就是从大型软件架构出发、便于升级和维护的软件设计思想，它强调降低依赖，降低耦合。
    5、迪米特法则，又称最少知道原则（Demeter Principle）
    最少知道原则是指：一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。
    6、合成复用原则（Composite Reuse Principle）
    合成复用原则是指：尽量使用合成/聚合的方式，而不是使用继承。

第一种（懒汉，线程不安全）：
 
Java代码  
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
  
    public static Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
}  
 
 这种写法lazy loading很明显，但是致命的是在多线程不能正常工作。
第二种（懒汉，线程安全）：
 
Java代码  
public class Singleton {  
    private static Singleton instance;  
    private Singleton (){}  
    public static synchronized Singleton getInstance() {  
    if (instance == null) {  
        instance = new Singleton();  
    }  
    return instance;  
    }  
}  
 
 这种写法能够在多线程中很好的工作，而且看起来它也具备很好的lazy loading，但是，遗憾的是，效率很低，99%情况下不需要同步。
第三种（饿汉）：
 
Java代码  
public class Singleton {  
    private static Singleton instance = new Singleton();  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return instance;  
    }  
}  
 
 这种方式基于classloder机制避免了多线程的同步问题，不过，instance在类装载时就实例化，虽然导致类装载的原因有很多种，在单例模式中大多数都是调用getInstance方法， 但是也不能确定有其他的方式（或者其他的静态方法）导致类装载，这时候初始化instance显然没有达到lazy loading的效果。
第四种（饿汉，变种）：
 
Java代码  
public class Singleton {  
    private Singleton instance = null;  
    static {  
    instance = new Singleton();  
    }  
    private Singleton (){}  
    public static Singleton getInstance() {  
    return this.instance;  
    }  
}  
 
 表面上看起来差别挺大，其实更第三种方式差不多，都是在类初始化即实例化instance。
第五种（静态内部类）：
 
Java代码  
public class Singleton {  
    private static class SingletonHolder {  
    private static final Singleton INSTANCE = new Singleton();  
    }  
    private Singleton (){}  
    public static final Singleton getInstance() {  
    return SingletonHolder.INSTANCE;  
    }  
}  
 
这种方式同样利用了classloder的机制来保证初始化instance时只有一个线程，它跟第三种和第四种方式不同的是（很细微的差别）：第三种和第四种方式是只要Singleton类被装载了，那么instance就会被实例化（没有达到lazy loading效果），而这种方式是Singleton类被装载了，instance不一定被初始化。因为SingletonHolder类没有被主动使用，只有显示通过调用getInstance方法时，才会显示装载SingletonHolder类，从而实例化instance。想象一下，如果实例化instance很消耗资源，我想让他延迟加载，另外一方面，我不希望在Singleton类加载时就实例化，因为我不能确保Singleton类还可能在其他的地方被主动使用从而被加载，那么这个时候实例化instance显然是不合适的。这个时候，这种方式相比第三和第四种方式就显得很合理。
第六种（枚举）：
 
Java代码  
public enum Singleton {  
    INSTANCE;  
    public void whateverMethod() {  
    }  
}  
 
 这种方式是Effective Java作者Josh Bloch 提倡的方式，它不仅能避免多线程同步问题，而且还能防止反序列化重新创建新的对象，可谓是很坚强的壁垒啊，不过，个人认为由于1.5中才加入enum特性，用这种方式写不免让人感觉生疏，在实际工作中，我也很少看见有人这么写过。
第七种（双重校验锁）：
Java代码  
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        if (singleton == null) {  
            singleton = new Singleton();  
        }  
        }  
    }  
    return singleton;  
    }  
}  
 
 这个是第二种方式的升级版，俗称双重检查锁定，详细介绍请查看：http://www.ibm.com/developerworks/cn/java/j-dcl.html
在JDK1.5之后，双重检查锁定才能够正常达到单例效果。
 
总结
有两个问题需要注意：
1.如果单例由不同的类装载器装入，那便有可能存在多个单例类的实例。假定不是远端存取，例如一些servlet容器对每个servlet使用完全不同的类装载器，这样的话如果有两个servlet访问一个单例类，它们就都会有各自的实例。
2.如果Singleton实现了java.io.Serializable接口，那么这个类的实例就可能被序列化和复原。不管怎样，如果你序列化一个单例类的对象，接下来复原多个那个对象，那你就会有多个单例类的实例。
对第一个问题修复的办法是：
 
Java代码  
private static Class getClass(String classname)      
                                         throws ClassNotFoundException {     
      ClassLoader classLoader = Thread.currentThread().getContextClassLoader();     
      
      if(classLoader == null)     
         classLoader = Singleton.class.getClassLoader();     
      
      return (classLoader.loadClass(classname));     
   }     
}  
 对第二个问题修复的办法是：
 
Java代码  
public class Singleton implements java.io.Serializable {     
   public static Singleton INSTANCE = new Singleton();     
      
   protected Singleton() {     
        
   }     
   private Object readResolve() {     
            return INSTANCE;     
      }    
}   
 
对我来说，我比较喜欢第三种和第五种方式，简单易懂，而且在JVM层实现了线程安全（如果不是多个类加载器环境），一般的情况下，我会使用第三种方式，只有在要明确实现lazy loading效果时才会使用第五种方式，另外，如果涉及到反序列化创建对象时我会试着使用枚举的方式来实现单例，不过，我一直会保证我的程序是线程安全的，而且我永远不会使用第一种和第二种方式，如果有其他特殊的需求，我可能会使用第七种方式，毕竟，JDK1.5已经没有双重检查锁定的问题了。

第一种不算单例，第四种和第三种就是一种，如果算的话，第五种也可以分开写了。所以说，一般单例都是五种写法。懒汉，恶汉，双重校验锁，枚举和静态内部类。




数据结构和算法
数据结构

Java中有一个Arrays类，专门用来操作array。 
Arrays中拥有一组static函数， 
- equals()：比较两个array是否相等。array拥有相同元素个数，且所有对应元素两两相等。 
- fill()：将值填入array中。 
- sort()：用来对array进行排序。 
- binarySearch()：在排好序的array中寻找元素。 
- System.arraycopy()：array的复制。

int [] intArr = new int[10];

Array是Java中随机访问一连串对象最有效率的数据结构，但很不灵活，大小固定，且不知道里面有多少元素。为此JDK已经为我们提供了一系列相应的类来实现功能强大且更灵活的基本数据结构。这些类均在java.util包中。其继承结构如下： 
Collection 
├List 
│├LinkedList 
│├ArrayList 
│└Vector 
│　└Stack 
└Set 
│ └SortedSet 
└Queue

-Map 
├HashTable 
├HashMap 
└WeakHashMap

List

List是一个接口，不能实例化，需要实例化一个ArrayList或者LinkedList。 
ArrayList里面的内部实现，是通过一定的增长规则动态复制增加数组长度来实现动态增加元素的。如果在大数据量的情况下，在某一个位置随机插入或者删除元素，就会产生性能问题。LinkedList可以解决这类问题，但LinkedList在通过下标取元素的时候，需要遍历整个链表节点匹配，数据量大的情况下，效率不高。Vector是一种老的动态数组，是线程同步的，效率很低，一般不赞成使用。Stack是Java实现了一个堆栈，先进后出结构。

遍历时删除问题

使用增强for循环遍历List(所有实现子类ArrayList,Stack等)元素对其中元素进行删除，会抛出java.util.ConcurrentModificationException的异常。若使用下面这种方式：

for(int i = 0;i < list.size();i++){
            list.remove(i);
}

则会删除下标为偶数的元素，因为每次删除后，后面的元素的下标全部减1，相当于元素位置全部左移一位，再次删除时，会跳过一个元素进行删除。这是非常不好的。如果非得要这样删除，可以倒着来：

for(int i = list.size()-1 ;i >= 0 ;i--){
            list.remove(i);
}

或者新建一个要删除的List，最后一起删除。list.removeAll(deleteList);

Set

Set接口继承Collection接口，最大的特点是集合中的元素都是唯一的，没有重复。它有两个子类，HashSet和TreeSet。

HashSet

不允许出现重复元素；
不保证集合中元素的顺序。哈希算法来的~
允许包含值为null的元素，但最多只能有一个null元素。
TreeSet

不允许出现重复元素；
集合中元素的顺序按某种规则进行排序
不允许包含值为null的元素
Map

Map接口，没有继承Collection接口，它是独立的一个接口。它使用key-value的键值对存储数据。常用的两个子类是HashMap和TreeMap。 
- HashMap：Map基于散列表的实现。插入和查询“键值对”的开销是固定的。可以通过构造器设置容量capacity和负载因子load factor，以调整容器的性能。 
- LinkedHashMap： 类似于HashMap，但是迭代遍历它时，取得“键值对”的顺序是其插入次序，或者是最近最少使用(LRU)的次序。只比HashMap慢一点。而在迭代访问时发而更快，因为它使用链表维护内部次序。 
- TreeMap ： 基于红黑树数据结构的实现。查看“键”或“键值对”时，它们会被排序(次序由Comparabel或Comparator决定)。TreeMap的特点在 于，你得到的结果是经过排序的。TreeMap是唯一的带有subMap()方法的Map，它可以返回一个子树。 
- WeakHashMao ：弱键(weak key)Map，Map中使用的对象也被允许释放: 这是为解决特殊问题设计的。如果没有map之外的引用指向某个“键”，则此“键”可以被垃圾收集器回收。 
- IdentifyHashMap： : 使用==代替equals()对“键”作比较的hash map。专为解决特殊问题而设计。

线程安全

Vector是线程同步的，也就是线程安全的，对多线程的操作采用了synchronized处理。但因为效率低，已不建议使用。ArrayList和LinkedList都是线程不安全的，在多线程环境中，对数据的修改会造成错误的结果。有两种解决方案：

使用同步包装器

List safedList = Collections.synchronizedList(new ArrayList());
Set safedSet=Collections.synchronizedSet(new HashSet());
Map safedMap=Collections.synchronizedMap(new HashMap());


查看其源码，发现是Collections类给不安全的集合类包装了一层，然后生成一个新的类，新类里面采用了synchronized对集合的操作进行了同步处理。

...
        public int size() {
            synchronized (mutex) {return c.size();}
        }
        public boolean isEmpty() {
            synchronized (mutex) {return c.isEmpty();}
        }
        public boolean contains(Object o) {
            synchronized (mutex) {return c.contains(o);}
        }
        public Object[] toArray() {
            synchronized (mutex) {return c.toArray();}
        }
        public <T> T[] toArray(T[] a) {
            synchronized (mutex) {return c.toArray(a);}
        }

        public Iterator<E> iterator() {
            return c.iterator(); // Must be manually synched by user!
        }

        public boolean add(E e) {
            synchronized (mutex) {return c.add(e);}
        }
        public boolean remove(Object o) {
            synchronized (mutex) {return c.remove(o);}
        }

        public boolean containsAll(Collection<?> coll) {
            synchronized (mutex) {return c.containsAll(coll);}
        }
        public boolean addAll(Collection<? extends E> coll) {
            synchronized (mutex) {return c.addAll(coll);}
        }
        public boolean removeAll(Collection<?> coll) {
            synchronized (mutex) {return c.removeAll(coll);}
        }
        public boolean retainAll(Collection<?> coll) {
            synchronized (mutex) {return c.retainAll(coll);}
        }
        public void clear() {
            synchronized (mutex) {c.clear();}
        }
...

使用安全的集合类

Java5.0新加入的ConcurrentLinkedQueue、ConcurrentHashMap、CopyOnWriteArrayList和CopyOnWriteArraySet，这些集合类都是线程安全的。这些类在 java.util.concurrent包下。 
而至于这些新的类为什么能保证线程安全，这里不作详述，可以参考网上大牛的分析。

Android中的List、Map替代方案

SimpleArrayMap

SparseArray与SparseArrayCompat和LongSparseArray

这3个类中，前2个基本上是同一类，只不过第二个类有removeAt方法，第三个是Long类型的。 
这3个类也是用来代替HashMap,只不过他们的键(key)的类型是整型Integer或者Long类型，在实际开发中，如月份缩写的映射，或者进行文件缓存映射，ViewHolder都特别适用

AtomicFile

AtomicFile首先不是用来代替File的，而是作为File的辅助类存在， AtomicFile的作用是实现事务性原子操作，即文件读写必须完整，适合多线程中的文件读写操作。 
用来实现多线程中的文件读写的安全操作

算法

二分查找

对于有序数组，二分查找的效率在大数据量的情况下，效率明显：

private static int find(int [] arr,int searchKey){
        int lowerBound = 0;
        int upperBound = arr.length -1;
        int curIn;
        while(lowerBound <= upperBound){
            curIn = (lowerBound + upperBound) / 2;
            if(arr[curIn] == searchKey){
                return curIn;
            }else{
                if(arr[curIn] < searchKey){
                    lowerBound = curIn + 1;
                }else{
                    upperBound = curIn - 1;
                }
            }
        }
        return -1;
    }

使用递归的方式编写，貌似看起来好理解点：

private static int recursiveFind(int[] arr,int start,int end,int searchKey){
        if (start <= end) {
            // 中间位置
            int middle = (start + end) >> 1; // (start+end)/2
            if (searchKey == arr[middle]) {
                // 等于中值直接返回
                return middle;
            } else if (searchKey < arr[middle]) {
                // 小于中值时在中值前面找
                return recursiveFind(arr, start, middle - 1, searchKey);
            } else {
                // 大于中值在中值后面找
                return recursiveFind(arr, middle + 1, end, searchKey);
            }
        } else {
            // 找不到
            return -1;
        }
    }

排序

简单排序

冒泡排序

对乱序的数组，很常见的排序方法是冒泡排序：

private static void bubbleSrot(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = i + 1; j < arr.length; j++) {
                if(arr[i] > arr[j]){
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
    }

这种排序方法速度是很慢的，运行时间为O（N²）级。 
选择排序改进了冒泡排序，将必要的交换次数从O（N²）减少到O（N），不幸的是比较次数依然是O（N²）级。 
然而，选择排序依然为大记录量的排序提出了一个非常重要的改进，因为这些大量的记录需要在内存中移动，这就使交换的时间和比较的时间相比起来，交换的时间更为重要。（一般来说，Java语言中不是这种情况，Java中只是改变了引用位置，而实际对象的位置并没有发生改变）

选择排序

private static void chooseSort(int[] arr) {
        for (int i = 0; i < arr.length; i++) {
            int least = i;
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[least]) {
                    least = j;
                }
            }
            // 将当前第一个元素与它后面序列中的最小的一个 元素交换，也就是将最小的元素放在最前端
            int temp = arr[i];
            arr[i] = arr[least];
            arr[least] = temp;
        }
    }  

选择排序的效率：选择排序和冒泡排序执行了相同次数的比较：N*(N-1)/2。对于10个数据项，需要45次比较，然而，10个数据项只需要少于10次的交换。对于100个数据项，需要4950次比较，但只进行不到100次交换。N值很大时，比较的次数是主要的，所以结论是选择排序和冒泡哦排序一样运行了O（N²）时间。但是，选择排序无疑更快，因为它进行的交换少得多。


插入排序

插入排序，在一般情况下，比冒泡排序快一倍，比选择排序快一点。

private static void insertionSort(int[] arr){
        int in,out;
        for(out = 1 ; out < arr.length ; out ++){
            int temp = arr[out];
            in = out;
            while(in > 0 && arr[in-1] >= temp){
                arr[in] = arr[in - 1];
                --in;
            }
            arr[in] = temp;
        }
    }

在外层的for循环中，out变量从1开始，向右移动。它标记了未排序部分的最左端数据。而在内层的while循环中，in变量从out变量开始，向左移动，直到temp变量小于in所指的数组数据项，或者它已经不能再向左移动为止。while循环的每一趟都向左移动了一个已排序的数据项。

插入排序的效率：这个算法中，第一趟排序，最多比较一次，第二趟排序，最多比较两次，以此类推，最后一趟最多比较N-1次，因此有1+2+3+…+N-1 = N*(N-1)/2。然而，因为在每一趟排序发现插入点之前，平均只有全体数据项的一半真的进行了比较，所以除以2最后是N*(N-1)/4。 
对于随机顺序的数据，插入排序也需要O（N²）的时间级。当数据基本有序，插入排序几乎只需要O(N)的时间，这对把一个基本有序的文件进行排序是一个简单而有效的方法。 
对于逆序排列的数据，每次比较和移动都会执行，所以插入排序不比冒泡排序快。

归并排序

归并排序比简单排序要有效的多，至少在速度上是这样的。冒泡排序、选择排序、插入排序要用O（N²）的时间，而归并排序只需要O(N*logN)的时间。 
归并排序的一个缺点是它需要在存储器中有另一个大小等于被排序的数据项数目的数组。如果初始数组几乎占满整个存储器，那么归并排序将不能工作。但是，如果有足够的空间，归并排序会是一个很好的选择。 
原理是合并两个已排序的数组到一个数组：

//将两个已排序的数组合并到第三个数组上。
    private static void merge(int[] arrA,  int[] arrB,  int[] arrC) {
        int aDex = 0, bDex = 0, cDex = 0;
        int sizeA = arrA.length;
        int sizeB = arrB.length;

        // A数组和B数组都不为空
        while (aDex < sizeA && bDex < sizeB) {
            if (arrA[aDex] < arrB[bDex]) {
                arrC[cDex++] = arrA[aDex++];
            } else {
                arrC[cDex++] = arrB[bDex++];
            }
        }
        //A数组不为空，B数组为空
        while (aDex < sizeA) {
            arrC[cDex++] = arrA[aDex++];
        }
        //A数组为空，B数组不为空
        while (bDex < sizeB) {
            arrC[cDex++] = arrB[bDex++];
        }
    }

于是，详细的完整实现如下：

static class DArray{
        private int [] theArray;

        public DArray(int[] theArray) {
            this.theArray = theArray;
        }

        //执行归并排序
        public void mergeSort(){
            //复制一份出来
            int [] workSpace = new int [theArray.length];
            reMergeSort(workSpace, 0, theArray.length-1);
        }

        private void reMergeSort(int [] workSpace,int lowerBound,int upperBound) {
            if(lowerBound == upperBound){
                return;
            }else{
                int mid = (lowerBound + upperBound) / 2;
                reMergeSort(workSpace, lowerBound, mid);
                reMergeSort(workSpace, mid + 1, upperBound);
                merge(workSpace, lowerBound, mid + 1,upperBound);
            }
        }

        private void merge(int [] workSpace,int lowPtr,int highPtr,int upperBound){
            int j= 0;//workSpace's index
            int lowerBound = lowPtr;
            int mid = highPtr -1;
            int n = upperBound - lowerBound + 1;
            while(lowPtr <= mid && highPtr <= upperBound){
                if(theArray[lowPtr] < theArray[highPtr]){
                    workSpace[j++] = theArray[lowPtr++];
                }else{
                    workSpace[j++] = theArray[highPtr++];
                }
            }

            while(lowPtr <= mid){
                workSpace[j++] = theArray[lowPtr++];
            }

            while(highPtr <= upperBound){
                workSpace[j++] = theArray[highPtr++];
            }

            for(j = 0;j < n ;j++){
                theArray[lowerBound+j] = workSpace[j];
            }
        }
    }

运行测试：

int b[] = new int[] { 3, 4, 1, 5, 5, 6, 8, 9, 7 };
DArray dArray = new DArray(b);
dArray.mergeSort();
System.out.println(Arrays.toString(b));//输出结果：[1, 3, 4, 5, 5, 6, 7, 8, 9]

高级排序

有2个高级的排序算法，希尔排序和快速排序。这两种排序算法都比简单排序算法快得多：希尔排序大约需要O(N*(logN)²)时间，快速排序需要O(N*logN)时间。这两种排序算法都和归并排序不同，不需要大量的辅助存储空间。希尔排序几乎和归并排序一样容易实现，而快速排序是所有通用排序算法中最快的一种排序算法。 
还有一种基数排序，是一种不常用但很有趣的排序算法。

希尔排序

希尔排序是基于插入排序的。

private static void shellSort(int[] arr) {
        int inner, outer;
        int temp;
        int h = 1;
        int nElem = arr.length;
        while (h <= nElem / 3) {
            h = h * 3 + 1;
        }
        while (h > 0) {
            for (outer = h; outer < nElem; outer++) {
                temp = arr[outer];
                inner = outer;
                while (inner > h - 1 && arr[inner - h] >= temp) {
                    arr[inner] = arr[inner - h];
                    inner -= h;
                }
                arr[inner] = temp;
            }
            h = (h - 1) / 3;
        }
    }

快速排序

快速排序是最流行的排序算法，在大多数情况下，快速排序都是最快的，执行时间是O(N*logN)级。

划分

划分是快速排序的根本机制。划分本身也是一个有用的操作。 
划分数据就是把数据分为两组，使所有关键字大于特定值的数据项在一组，所有关键字小于特定值的数据项在另一组。

private static int partitionIt(int[] arr ,int left,int right,int pivot){
        int leftPtr = left - 1;
        int rightPtr = right + 1;
        while(true){
            while(leftPtr < right && arr[++leftPtr] < pivot);
            while(rightPtr > 0 && arr[--rightPtr] > pivot);

            if(leftPtr >= rightPtr){
                break;
            }else{
                //交换leftPtr和rightPtr位置的元素
                int temp = arr[leftPtr];
                arr[leftPtr] = arr[rightPtr];
                arr[rightPtr] = temp;
            }
        }
        return leftPtr;//返回枢纽位置
    }
快速排序

//快速排序
    private static void recQuickSort(int arr [] ,int left,int right){
        if(right - left <= 0){
            return;
        }else{
            int pivot = arr[right];//一般使用数组最右边的元素作为枢纽
            int partition = partitionIt(arr, left, right, pivot);
            recQuickSort(arr, left, partition-1);
            recQuickSort(arr, partition+1, right);
        }
    }


    //划分
    private static int partitionIt(int[] arr ,int left,int right,int pivot){
        int leftPtr = left - 1;
        //int rightPtr = right + 1;
        int rightPtr = right ; //使用最右边的元素作为枢纽，划分时就要将最右端的数据项排除在外
        while(true){
            while(arr[++leftPtr] < pivot);
            while(rightPtr > 0 && arr[--rightPtr] > pivot);

            if(leftPtr >= rightPtr){
                break;
            }else{
                //交换leftPtr和rightPtr位置的元素
                int temp = arr[leftPtr];
                arr[leftPtr] = arr[rightPtr];
                arr[rightPtr] = temp;
            }
        }
        //交换leftPtr和right位置的元素
        int temp = arr[leftPtr];
        arr[leftPtr] = arr[right];
        arr[right] = temp;
        return leftPtr;//返回枢纽位置
    }    
最后测试，10万条随机数据，排序完成耗时18~25ms。希尔排序耗时差不多，而简单排序中的插入排序和选择排序耗时3500ms以上，冒泡排序最慢，超过17000ms以上才完成；归并排序比希尔排序和快速排序稍微慢点，在30ms左右。


单元测试
JUnit

TestNG


系统调优

Web性能优化分为服务器端和浏览器端两个方面。

一、浏览器端，关于浏览器端优化，分很多个方面
1、压缩源码和图片
JavaScript文件源代码可以采用混淆压缩的方式，CSS文件源代码进行普通压缩，JPG图片可以根据具体质量来压缩为50%到70%，PNG可以使用一些开源压缩软件来压缩，比如24色变成8色、去掉一些PNG格式信息等。

2、选择合适的图片格式
如果图片颜色数较多就使用JPG格式，如果图片颜色数较少就使用PNG格式，如果能够通过服务器端判断浏览器支持WebP，那么就使用WebP格式和SVG格式。

3、合并静态资源
包括CSS、JavaScript和小图片，减少HTTP请求。有很大一部分用户访问会因为这一条而取得最大受益

4、开启服务器端的Gzip压缩
这对文本资源非常有效，对图片资源则没那么大的压缩比率。

5、使用CDN
或者一些公开库使用第三方提供的静态资源地址（比如jQuery、normalize.css）。一方面增加并发下载量，另一方面能够和其他网站共享缓存。

6、延长静态资源缓存时间
这样，频繁访问网站的访客就能够更快地访问。不过，这里要通过修改文件名的方式，确保在资源更新的时候，用户会拉取到最新的内容。

7、把CSS放在页面头部，把JavaScript放在页面底部
这样就不会阻塞页面渲染，让页面出现长时间的空白。


a、扩容 ，扩容的理解，就是扩充服务器并行处理的能力，简单来说就是加服务器，增加处理请求的能力，例如增加nginx 、tomcat等应用服务器的个数，或者物理服务器的个数，还有加大服务器带宽等等，这里考虑的是硬件方面
b、调优 ，调优，包括系统调优和代码调优 。 系统调优就是说加快处理速度，比如我们所提到的CDN、ehcache、redis等缓存技术，消息队列等等，加快服务间的响应速度，增加系统吞吐量，避免并发，至于代码调优，这些就需要多积累了，比如重构、工厂等， 数据库调优的话这个我不是很懂，只知道索引和存储过程


一条sql执行过长的时间，你如何优化，从哪些方面？
答：1、查看sql是否涉及多表的联表或者子查询，如果有，看是否能进行业务拆分，相关字段冗余或者合并成临时表（业务和算法的优化）
2、涉及链表的查询，是否能进行分表查询，单表查询之后的结果进行字段整合
3、如果以上两种都不能操作，非要链表查询，那么考虑对相对应的查询条件做索引。加快查询速度
4、针对数量大的表进行历史表分离（如交易流水表）
5、数据库主从分离，读写分离，降低读写针对同一表同时的压力，至于主从同步，mysql有自带的binlog实现 主从同步
6、explain分析sql语句，查看执行计划，分析索引是否用上，分析扫描行数等等
7、查看mysql执行日志，看看是否有其他方面的问题