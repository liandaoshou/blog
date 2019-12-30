---
layout: post
title:  "Java基础-集合"
date:   2017-03-14 09:57:09 +0800
categories: Java Base Set
tag: Java
---

# Java集合

## 接口继承关系和实现
    
    集合类存放于Java.util包中，主要有3种：set（集）、list（列表包含Queue）和map（映射）。
    
    1. Collection : Collection 是集合List、Set、Queue的最基本的接口。
    2. Iterator： 迭代器，可以通过迭代器遍历集合中的数据。
    3. Map： 是映射表的基础接口

![Java基础-集合](/images/posts/20170314/01.png)<br>


## List

Java的List是常用的数据类型。List是有序的集合，Java List一共三个实现类，分别是ArrayList、Vector和LinkedList。

### ArrayList（数组）

ArrayList 是最常用的List实现类，内部通过数组实现，它允许对元素进行快速随机访问。数组的缺点是每个元素间不能有间隔，当数组大小不满足时需要增加存储能力，就要将已有的数据复制到新的存储空间中。
当ArrayList的中间位置插入或者删除元素时，需要对数组进行复制，移动。因此适合随机查找和变例，并不适合插入和删除。

### Vector (数组实现，线程同步)

Vector 和 ArrayList一样，通过数组实现的，不同的是它支持线程同步，即某一刻只有一个线程能够写Vector，避免多线程同时写引起的不一致性，但实现同步需要很高的花费，因此访问比ArrayList慢。

### LinkList （链表）

LinkedList 使用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和便利速度比较慢，另外提供List接口中没有定义的方法，专门用于操作表头和表尾，可以当作堆、栈、队列和双向队列使用。

## Set

Set 注重独一无二的性质，该体系集合用于存储无序（存入和取出的顺序不一定相同）元素，值不能重复。对象的相等性本质时对象的hashCode值（Java时依据对象的内存地址计算出的此序号）判断。
若想要让两个不同的对象视为相等，必须覆盖Object的hashCode方法和equals方法。


### HashSet (Hash表)

HashSet存储元素的顺序并不是按照存入时的顺序，按照哈希值来存，所以取数据也是按照Hash值取得，元素的Hash时通过元素的hashcode方法来获取。HashSet首先判断两个元素的Hash值，如果Hash值一样，接着会比较equals方法。
如果equals结果为true，HashSet视为同一个元素，如果equals为false就是不同的元素。

Hash值相同的元素存储在Hash值下顺延（哈希值相同的元素放在一个哈希桶中），哈希相同的存一列。
HashSet通过HashCode值来确定元素在内存中的位置。一个HashCOde位置上可以存放多个元素。

### TreeSet（二叉树）

TreeSet是使用二叉树的原理对新的add()的对象按照指定的顺序排序（升序，降序），每增加一个对象都会进行排序，将对象插入的二叉树指定的位置。
Integer和String对象都可以进行默认的TreeSet排序，而自定义对象是不可的，自己定义的类必须实现Comparable接口，并且覆盖相应的compareTo()函数，才可以正常使用。
在覆盖compare()函数时，要返回相应的值才能使TreeSet按照一定规则排序。
比较此对象的指定对象顺序，如果该对象小于等于或大于指定对象，则分别返回负整数，零或正整数。

### LinkHashSet（HashSet+LinkedHashMap）

LinkedHashSet继承HashSet，基于LinkedHashMap实现，LinkedHashSet底层使用LinkedHashMap来保存所有元素，继承HashSet，其所有方法操作上与HashSet相同。
因此LinkedHashSet提供了四个构造方法，并通过传递表示参数，调用父类构造器，底层构造一个LinkedHashMap来实现，相关参照与父类HashSet一致，直接调用HashSet方法。


## Map
    
### HaspMap （数组+链表+红黑树）

HashMap是根据键的HashCode值存数据，大多数情况下可以直接定位到它的值，所以具有很快的访问速度，但是遍历顺序却时不确定的。HashMap最多只允许一条记录键为null，允许多条记录的值为null。
HashMap是非线程安全的，如果要满足线程安全，可以用Collections的synchronized 方法使HashMap具有线程安全的能力，或者使用ConcurrentHashMap。

Java7 HashMap结构

![Java基础-HashMap结构](/images/posts/20170314/02.png)<br>

HashMap里面是一个数组，然后数组中每个元素是一个单向链表，每个绿色的实体是嵌套类Entry的实例，Entry包含4哥属性：key、value、hash和用于单向链表的next。
1. 当前数组容量，始终保持2^n,可以扩容，扩容后数组大小为当前的两倍。
2. 负载因子，默认为0.75。
3. 阈，扩容的阈值，等于 capacity * loadFactor（当前数组容量 * 负载因子）。

Java HashMap实现

Java8对HashMap进行一些修改，不同是用了红黑树，所以是由数组+链表+红黑树组成。

根据Java7HashMap查找根据Hash值能够快速定位到数组的具体下标，但是之后需要顺着链表一个个比较下去才能找到我们需要的，时间复杂度取决于链表的长度，为O（n）.
为了降低这部分开销，在Java8中，当链表中的元素超过8个以后，会将链表转换为红黑树，在这些位置进行查找的时候可以降低时间复杂度O（logN）。

![Java基础-Java8 HashMap结构](/images/posts/20170314/03.png)<br>

### ConcurrentHashMap

#### Segment 段

    ConcurrentHashMap和HashMap的思路差不多，ConcurrentHashMap支持并发操作，整个ConcurrentHashMap由一个个Segment组成，Segment代表部分或者一段，所以很多地方将其描述为分段锁。
    
#### 线程安全（Segment继承ReentrantLock加锁）
    
    ConcurrentHashMap是一个Segment数组，Segment通过继承ReentrantLock进行加锁，所以每次需要加锁操作锁住一个Segment，这样只要保证每个Segment是线程安全的，也就实现了全局的线程安全。
    
![Java基础-Java7 ConcurrentHashMap结构](/images/posts/20170314/04.png)<br> 

    并行度（默认16）
    concurrencyLevel：并行级别、并发数、Segments数，默认是16，也就是说ConcurrentHashMap由16个Segments，理论上最大同时支持16哥线程并发写，只要操作分别分布在不同的Segment上，这个值可以在初始化的时候设置为其他值。
    但是一旦初始化后，就不可扩容。再具体到每个Segment内部，其实每个Segment很像之前介绍的HashMap，不过它要保证线程安全。
    
    Java8实现引入红黑树
    Java8对ConcurentHashMap进行比较大的改动，Java8也引入了红黑树。
    
      
![Java基础-Java8 ConcurrentHashMap结构](/images/posts/20170314/05.png)<br>   

    
### HashTable （线程安全）

HashTable是遗留类，很多映射常用功能与HashMap类似，不同的是继承Dictionary类，并且是线程安全的，任一时间只有一个线程能写Hashtable，并发性不如ConcurrentHashMap，因为ConcurrentHashMap引入分段锁。
Hashtable不建议在新代码中使用，不需要线程安全的场合可以用HashMap替换，需要线程安全的场合可以用ConcurrentHashMap替换。

### TreeMap（可排序）

TreeMap实现SortedMap接口，能够根据键排序，默认是按键值升序，也可指定排序的比较器，当用Iterator遍历时，得到记录时排序后的。
如果使用排序的映射，可以使用TreeMap。
在使用TreeMap时，key必须实现Comparable接口或者在构造TreeMap传入自定义的Comparator否则会抛出java.lang.ClassCastException类型异常。

### LinkHashMap（记录插入顺序）

LinkedHashMap是HashMap的一个子类，保存记录的插入顺序，在用Iterator遍历LinkedHashMap时，。得到的记录时先插入的，也可以在构造时带参数访问，按照访问次序排序。

