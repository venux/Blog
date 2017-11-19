---
title: 面试
comments: true
date: 2017-10-10 20:03:44
tags: 面试
categories: 面试
---
## 1. C#和.NET

### 1.1 C#基础知识

#### 访问修饰符

- private【Private】 私有（定义类型、嵌套类型）
- protected【Family】 保护（定义类型、嵌套类型、不同程序集中的派生类型）
- C#不支持【Family and Assembly】（定义类型、嵌套类型、同一程序集中的派生类型）
- internal【Assembly】 内部（同一程序集中的所有类型）
- protected internal【Family or Assembly】（定义类型、嵌套类型、同一程序集中的所有类型，不同程序集中的派生类型）
- public【Public】 公有

*PS：*
- 【】中为CLR术语。
- `C#`派生类型重写基类型定义的成员，`C#编译器`要求两者具有相同可访问性，`CLR`允许放宽但不允许收紧成员的可访问性。

<!--more-->

#### 值类型、引用类型

##### 引用类型

1 总是从`托管堆`分配，new 操作符返回指向对象的内存地址；
2 堆上分配的每个对象都有一些额外成员（类型对象指针、同步块索引），这些成员必须初始化；
3 对象中的其他字节（为字段而设）总是设为零；
4 从托管堆分配对象时，可能强制执行一次垃圾回收。

##### 值类型

1 `一般`在`线程栈`上分配；
2 优点：缓解托管堆的压力，减少应用程序生存期内的垃圾回收次数；
3 所有值类型必须从 System.ValueType 派生；
4 值类型可以实现一个或多个接口；
5 所有值类型隐式密封；

##### 区别

- 值类型对象两种表示形式：未装箱和已装箱，引用类型总是已装箱
- 值类型从 System.ValueType 派生，该类型重写了 Equals 方法，能在两对象的字段值完全匹配返回 true，也重写了 GetHashCode 方法，算法会将实例字段的值计算进去。*由于默认实现存在性能问题，故定义值类型需重写。*
- 值类型隐式密封，故不应引入任何虚方法，且所有方法不能时抽象方法，所有方法都隐式密封。
- 引用类型包含堆中对象的地址，默认初始化为 null，值类型总是包含基础类型的一个值，默认初始化为 0。
- 值类型赋给另一个值类型变量，会执行逐字段复制，引用类型则只复制内存地址，故对值类型变量执行操作不会影响另一个值类型，引用类型则不同。
- 由于未装箱的值类型不在堆上分配，一旦定义了该类型的实例的方法不再活动，分配的存储就会释放，而不等垃圾回收。

##### 值类型设计前提：

- 类型具有基元类型的行为，没有成员会改变类型的任何实例字段。即不可变（immutable），建议将全部字段标记为 readonly。
- 类型不需要从其他类型继承。
- 类型也不派生其他任何类型。
- 类型的实例较小（16字节或更小）。
- 类型的实例较大（大于16字节），但不作为方法实参传递，也不作为返回参数。

##### 参考

- [个人笔记](http://www.cnblogs.com/venux/p/6307561.html)

#### 委托、事件

#### 重载、重写

#### 接口、抽象类

#### out和ref

#### 虚方法

#### Object

- Equals:如果两个`对象`具有相同值，就返回true。
    - 对象相等性和同一性
- GetHashCode:若对象要在哈希表集合（如Dictionary）中作为键，则应重写该方法。
    - 良好分布：指针对所有输入，GetHashCode生成的哈希值应该在所有整数中产生一个随机的分布。
- ToString:默认返回类型的完整名称（this.GetType().FullName）。
- GetType:返回类型的一个实例。
    - 非虚方法，防止类重写，隐瞒类型，从而破坏类型安全性。
- [MemberwiseClone](https://msdn.microsoft.com/en-us/library/system.object.memberwiseclone(v=vs.110).aspx):浅拷贝。
    - protected
    - 非虚方法
    - The MemberwiseClone method creates a shallow copy by creating a new object, and then copying the nonstatic fields of the current object to the new object. If a field is a `value` type, `a bit-by-bit copy of the field is performed`. If a field is a `reference` type, `the reference is copied but the referred object is not; therefore, the original object and its clone refer to the same object`.（意即：obj和cloneObj对应的值类型不会同时改变；引用类型同时改变）。    
- Finalize:垃圾回收之前调用该`虚`方法，可重写进行对象清理工作。

#### new操作符

1 计算类型及其所有基类型（直到Object）中定义的所有`实例字段`需要的字节数，堆上每个对象都需要一些额外的成员（overhead成员、开销成员），包括`类型对象指针type object pointer`和`同步块索引sync block index`，CLR利用这些成员管理对象，额外成员的字节数需要计入对象大小。

2 从`托管堆`分配类型要求的字节数，从而分配对象的内存，所有字节设为零。

3 初始化对象的类型对象指针和同步块索引。

4 调用类型的实例构造器，传递实参，编译器自动生成代码调用基类构造器，并负责初始化定义的实例字段，最终调用Object的构造器，返回。

5 返回指向新建对象的一个引用（指针）。

#### 类型转换

1. C#运行类型定义转换操作符方法，但只有使用转型表达式才调用，使用`as`或`is`永不调用它们。

#### 类型、对象、线程栈、托管堆在运行时的相互关系

CLR via C# 4.4 P90

#### 字段和属性有什么区别

- 答一：两者都是类的成员。不同的是：
    1 字段是数据成员，属性是方法成员;
    2 访问上对于属性访问需要使用访问元get,set，字段没有访问元直接赋值或者取值;
    3 属性能override，visual字段不能。

- 答二：如果你编写一些控件给别的开发者用，而需要给他们提供“数据绑定”这种傻瓜化的机制，那么使用属性才可以做到。
属性是方法而字段不是，当你用反射去掉用的时候，它们有各自的API。因为属性是方法，所以它可以和方法那样定义在接口中，或者被继承和重写，重写属性被ORM/AOP等框架用来注入代码。

#### 抽象方法，和虚方法的区别

- 抽象方法一定是虚方法，虚方法未必是抽象方法。
- 虚方法是指可以被继承类重写的方法，而抽象方法是指，基类是抽象类，没有实现它，因此必须被继承类重写的方法。

#### new的几种用法

- 创建对象或者结构（只是用于调用结构构造函数）；
- 隐藏基类成员；
- 泛型里用于约束

#### 什么叫做泛型

- 从编程的角度说是在定义类或者方法的时候省去具体的类型，由调用者来指定，类型+泛型类型合成得到真正的类型。
- 从实现机制上说，泛型是CLR在运行时动态根据泛型类型创建的匿名类型。
- 从OO设计的角度说，泛型体现了多态性。
- 泛型使得程序员可以复用数据结构和算法，并且适应不同的类型，享有编译期间的强类型检查和语法提示。
    一些经典的FCL提供的泛型类型和接口,List<T>、Dictionary<T1, T2>这个属于复用数据结构,IComparer<T>、IEnumerable<T>这个属于复用算法

#### 什么叫做类

就C#而言，类是对象的模板，对象是类的实例。C#是强类型语言，一切皆需要类型，除了内置的简单类型，那些其实例为引用对象的都叫做类。C#也允许定义抽象类和密封类，以及两者的叠加——静态类，它们都无法实例化，其实这是编译器的限制，本质上它们和一般的类没有区别，是特殊情况。

#### EF的理解

- 对象关系映射（ORM）机制和LINQ To EF Provider，在此基础上的缓存机制、延迟加载、对象状态跟踪、事务等等。
- EF是微软官方的ORM框架，结束了之前各种第三方ORM混战的局面，统一了API，这无疑是开发者的福音。EF拥有非常优雅的，基于C#/VB语言优化的API，比如原生的LINQ查询，自然的Code First的对数据结构的定义，Fluent API方式的数据库和关系的定义等等。VS完美支持EF并且提供了多种数据库的适配。

#### 其他

- 开发调试时打开编译器的/checked+开关，虽然会慢点，但能轻松进行溢出检查，及时修正BUG。正式发布时使用/checked-开关。
- System.Decimal是`非常特殊`的类型，虽然C#视其为基元类型，但CLR不然。内部提供各种计算方法和操作符重载，故处理速度慢于CLR基元类型。

### 1.2 ASP.NET

#### 页面传值

- [参考1](http://www.cnblogs.com/zhangkai2237/archive/2012/05/06/2486462.html)

#### ASP.NET服务器控件的生命周期

- [参考1](http://www.cnblogs.com/waters/articles/3373013.html)
- [参考2](http://www.cnblogs.com/peterYong/p/6556597.html)

#### ASP.NET七个内置对象

### 1.3 名词解释

- FCL(Framework Class Library)框架类库
- CLS(Common Language Stander)
- CLR(Common Language Runtime)公共语言运行时
- IDL(Interface Definition Language)接口定义语言
- IL(Intermediate Language)中间语言

### 1.4 IL

#### 指令

- add：两值相加，不执行溢出检查
- add.ovf：两值相加，执行溢出检查，抛出System.OverflowException
- sub：减
- sub.ovf
- mul：乘
- mul.ovf
- conv：转换
- conv.ovf

### 参考

- CLR via C#(第4版)
- [文章一](http://bbs.csdn.net/topics/390919248)

## 2.数据库

### 2.1 基础

- Table1含有字段Col1，Col2，Col3，请用一条标准SQL选出Col2重复条数>=2的所有记录。
```sql
SELECT
    COUNT(1)
FROM
    Table1
GROUP BY
    Col2
HAVING
    COUNT(COL2) >= 2
```

### 2.2 SQL性能优化

### 参考

## 3. 数据结构和算法

### 3.1 数据结构

### 3.2 算法

#### 3.2.1 冒泡排序

#### 3.2.2 快速排序

#### 3.2.3 冒泡排序

### 参考

1.https://github.com/aalhour/C-Sharp-Algorithms

## 4. 编程思想

### 4.1 原则

- SOLID

### 4.2 设计模式

### 4.3 MVC

### 4.4 DDD

## 5. 前端

### 5.1 JavaScript

### 5.2 JQuery

### 5.3 性能优化

### 5.4 其他

## 6. 其他

### 6.1 新技术

### 6.2 职业规划
