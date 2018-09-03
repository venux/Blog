---
title: Java基础知识02
comments: true
tags:
  - Java
categories:
  - 01.编程语言
  - 02.Java
date: 2018-03-29 22:01:27
---
## 1 数据结构

### 1.1 枚举（Enumeration）

定义了一种从数据结构中取回连续元素的方式，已被迭代器取代。

### 1.2 位集合（BitSet）

实现了一组可以单独设置和清除的位或标志。该类在处理一组布尔值的时候非常有用，你只需要给每个值赋值一"位"，然后对位进行适当的设置或清除，就可以对布尔值进行操作了。

### 1.3 向量（Vector）

- 向量（Vector）类和传统数组非常相似，但是Vector的大小能根据需要动态的变化。
- 和数组一样，Vector对象的元素也能通过索引访问。
- 使用Vector类最主要的好处就是在创建对象的时候不必给对象指定大小，它的大小会根据需要动态的变化。

### 1.4 栈（Stack）

栈（Stack）实现了一个后进先出（LIFO）的数据结构。

### 1.5 字典（Dictionary）（已过时，使用Map接口替代）

字典（Dictionary） 类是一个**抽象类**，它定义了键映射到值的数据结构。

### 1.6 哈希表（Hashtable）

Hashtable类提供了一种在用户定义键结构的基础上来组织数据的手段。

### 1.7 属性（Properties）

Properties 继承于 Hashtable.Properties 类表示了一个持久的属性集.属性列表中每个键及其对应值都是一个字符串。Properties 类被许多Java类使用。例如，在获取环境变量时它就作为System.getProperties()方法的返回值。

<!--more-->

## 2 **集合框架**

集合框架是一个用来代表和操纵集合的统一架构。

### 2.1 设计目标

- 高性能,基本集合（动态数组，链表，树，哈希表）的实现也必须是高效的。
- 允许不同类型的集合，以类似的方式工作，具有高度的互操作性。
- 对一个集合的扩展和适应必须是简单的。

### 2.2 内容

- 接口：是代表集合的抽象数据类型。接口允许集合独立操纵其代表的细节。在面向对象的语言，接口通常形成一个层次。
- 实现（类）：是集合接口的具体实现。从本质上讲，它们是可重复使用的数据结构。
- 算法：是实现集合接口的对象里的方法执行的一些有用的计算，例如：搜索和排序。这些算法被称为多态，那是因为相同的方法可以在相似的接口上有着不同的实现。

### 2.3 集合接口


接口|描述
----|----
Collection 接口|允许你使用一组对象，是Collection层次结构的根接口。
List 接口|继承于Collection和一个 List实例存储一个有序集合的元素。
Set|继承于 Collection，是一个不包含重复元素的集合。
SortedSet|继承于Set保存有序的集合。
Map|将唯一的键映射到值。
Map.Entry|描述在一个Map中的一个元素（键/值对）。是一个Map的内部类。
SortedMap|继承于Map，使Key保持在升序排列。
Enumeration|这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。

### 2.4 集合类

类名|描述
----|----
AbstractCollection|实现了大部分的集合接口。
AbstractList|继承于AbstractCollection 并且实现了大部分List接口。
AbstractSequentialList|继承于AbstractList，提供了对数据元素的链式访问而不是随机访问。
LinkedList|继承于 AbstractSequentialList，实现了一个链表。
ArrayList|通过继承AbstractList，实现动态数组。
AbstractSet|继承于AbstractCollection 并且实现了大部分Set接口。
HashSet|继承了AbstractSet，并且使用一个哈希表。
LinkedHashSet|具有可预知迭代顺序的 Set 接口的哈希表和链接列表实现。
TreeSet|继承于AbstractSet，使用元素的自然顺序对元素进行排序.
AbstractMap|实现了大部分的Map接口。
HashMap|继承了HashMap，并且使用一个哈希表。
TreeMap|继承了AbstractMap，并且使用一颗树。
WeakHashMap|继承AbstractMap类，使用弱密钥的哈希表。
LinkedHashMap|继承于HashMap，使用元素的自然顺序对元素进行排序.
IdentityHashMap|继承AbstractMap类，比较文档时使用引用相等。

## 3 序列化

- 一个类的对象要想序列化成功，必须满足两个条件：
  - 该类必须实现 java.io.Serializable 对象。
  - 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的（transient ）。
- ObjectOutputStream（writeObject）—：序列化
  ```java
  public final void writeObject(Object x) throws IOException
  ```
- ObjectInputStream（readObject）：反序列化
  ```java
  public final Object readObject() throws IOException,ClassNotFoundException
  ```

## 4 网络编程

### 4.1 网络协议（java.net）

- TCP： TCP是传输控制协议的缩写，它保障了两个应用程序之间的可靠通信。通常用于互联网协议，被称TCP / IP。
- UDP:UDP是用户数据报协议的缩写，一个无连接的协议。提供了应用程序之间要发送的数据的数据包。

### 4.2 Socket（java.net.Socket）

主要使用ServerSocket和Socket类

- 1. 服务器实例化一个 ServerSocket 对象，表示通过服务器上的端口通信。
- 2. 服务器调用 ServerSocket 类的 accept() 方法，该方法将一直等待，直到客户端连接到服务器上给定的端口。
- 3. 服务器正在等待时，一个客户端实例化一个 Socket 对象，指定服务器名称和端口号来请求连接。
- 4. Socket 类的构造函数试图将客户端连接到指定的服务器和端口号。如果通信被建立，则在客户端创建一个 Socket 对象能够与服务器进行通信。
- 5. 在服务器端，accept() 方法返回服务器上一个新的 socket 引用，该 socket 连接到客户端的 socket。

## 5 多线程

### 5.1 线程的生命周期

![Thread](/images/posts/Java_Thread.jpg)

- 新建状态:使用 new 关键字和 Thread 类或其子类建立一个线程对象后，该线程对象就处于新建状态。它保持这个状态直到程序 start() 这个线程。
- 就绪状态:当线程对象调用了start()方法之后，该线程就进入就绪状态。就绪状态的线程处于就绪队列中，要等待JVM里线程调度器的调度。
- 运行状态:如果就绪状态的线程获取 CPU 资源，就可以执行 run()，此时线程便处于运行状态。处于运行状态的线程最为复杂，它可以变为阻塞状态、就绪状态和死亡状态。
- 阻塞状态:如果一个线程执行了sleep（睡眠）、suspend（挂起）等方法，失去所占用资源之后，该线程就从运行状态进入阻塞状态。在睡眠时间已到或获得设备资源后可以重新进入就绪状态。可以分为三种：
  - 等待阻塞：运行状态中的线程执行 wait() 方法，使线程进入到等待阻塞状态。
  - 同步阻塞：线程在获取 synchronized 同步锁失败(因为同步锁被其他线程占用)。
  - 其他阻塞：通过调用线程的 sleep() 或 join() 发出了 I/O 请求时，线程就会进入到阻塞状态。当sleep() 状态超时，join() 等待线程终止或超时，或者 I/O 处理完毕，线程重新转入就绪状态。
- 死亡状态:一个运行状态的线程完成任务或者其他终止条件发生时，该线程就切换到终止状态。

### 5.2 线程的优先级

- 线程的优先级是一个整数，其取值范围是 1 （Thread.MIN_PRIORITY ） - 10 （Thread.MAX_PRIORITY ）。
- 默认情况下，每一个线程都会分配一个优先级 NORM_PRIORITY（5）。

### 5.3 创建线程

- 通过实现 Runnable 接口；
- 通过继承 Thread 类本身；
- 通过 Callable 和 Future 创建线程。

## 6 文档注释

### 6.1 javadoc 标签

标签|描述|示例
----|----|----
@author|标识一个类的作者|@author description
@deprecated|指名一个过期的类或成员|@deprecated description
{@docRoot}|指明当前文档根目录的路径|Directory Path
@exception|标志一个类抛出的异常|@exception exception-name explanation
{@inheritDoc}|从直接父类继承的注释|Inherits a comment from the immediate surperclass.
{@link}|插入一个到另一个主题的链接|{@link name text}
{@linkplain}|插入一个到另一个主题的链接，但是该链接显示纯文本字体|Inserts an in-line link to another topic.
@param|说明一个方法的参数|@param parameter-name explanation
@return|说明返回值类型|@return explanation
@see|指定一个到另一个主题的链接|@see anchor
@serial|说明一个序列化属性|@serial description
@serialData|说明通过writeObject( ) 和 writeExternal( )方法写的数据|@serialData description
@serialField|说明一个ObjectStreamField组件|@serialField name type description
@since|标记当引入一个特定的变化时|@since release
@throws|和 @exception标签一样.|The @throws tag has the same meaning as the @exception tag.
{@value}|显示常量的值，该常量必须是static属性。|Displays the value of a constant, which must be a static field.
@version|指定类的版本|@version info

## 注意

本文主要用于记录个人不明了之处，故可能忽略许多知识点，如有需要，请自行查找相关资料，谢谢。