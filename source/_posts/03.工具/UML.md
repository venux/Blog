---
title: UML
comments: true
tags: UML
categories:
  - 03.工具
date: 2017-10-15 16:36:32
---
## 1 UML介绍

UML(Unified Modeling Language)又称统一建模语言或标准建模语言，一个支持模型化和软件系统开发的图形化语言，为软件开发的所有阶段提供模型化和可视化支持，包括由需求分析到规格，到构造和配置。 

<!--more-->

## 2 分类

- 用例图（use case diagrams）：描述用户需求，从用户的角度描述系统的功能
- 静态图
    - 类图（class  diagrams）：显示系统的静态结构
    - 对象图（object diagrams）
- 交互图
    - 序列图：描述对象之间的交互顺序，着重体现对象间消息传递的时间顺序
    - 协作图（Collaboration diagrams）：描述对象之间的合作关系，侧重对象之间的消息传递 
- 行为图
    - 状态图（Statechart diagrams）：描述对象的所有状态以及事件发生而引起的状态之间的转移
    - 活动图（Activity diagrams）：描述满足用例要求所要进行的活动以及活动时间的约束关系
- 实现图  
    - 构件图（Component diagrams）：描述代码构件的物理结构以及各构件之间的依赖关系
    - 部署图（Deployment diagrams）：系统中硬件的物理体系结构

## 3 类图

### 3.1 类

1 类(Class)封装了数据和行为，是面向对象的重要组成部分，它是具有相同属性、操作、关系的对象集合的总称。
2 在系统中，每个类具有一定的职责，职责指的是类所担任的任务，即类要完成什么样的功能，要承担什么样的义务。一个类可以有多种职责，设计得好的类一般只有一种职责，在定义类的时候，将类的职责分解成为类的属性和操作（即方法）。
3 类的属性即类的数据职责，类的操作即类的行为职责。

![类的UML图示](/images/posts/UML1.jpg)

- 类名，斜体表示抽象类
- 属性，表示方式：`可见性 名称:类型 [= 缺省值]`，可见性又分为 +（公有）、-（私有）、#（受保护），缺省值可选项。
- 操作：类的行为，即成员方法。表示方式：`可见性 名称(参数列表) [:返回类型]`，返回类型可选项。

### 3.2 接口

![接口的UML图示](http://www.uml.org.cn/oobject/images/20121123113.jpg)

### 3.3 关系

- **关联关系**：表示一类对象与另一类对象之间有联系（如将一个类的对象作为另一个类的成员变量）
![关联关系](http://www.uml.org.cn/oobject/images/2012112314.jpg)
    - **双向关联**
    ![双向关联](http://www.uml.org.cn/oobject/images/2012112315.jpg)
    - **单向关联**
    ![单项关联](http://www.uml.org.cn/oobject/images/2012112316.jpg)
    - **自关联**
    ![自关联](http://www.uml.org.cn/oobject/images/2012112317.jpg)
    - **多重关联**
    ![多重关联](http://www.uml.org.cn/oobject/images/2012112318.jpg)
        - 1..1: 表示另一个类的一个对象只与该类的一个对象有关系
        - 0..*：表示另一个类的一个对象与该类的零个或多个对象有关系
        - 1..*：表示另一个类的一个对象与该类的一个或多个对象有关系
        - 0..1：表示另一个类的一个对象没有或只与该类的一个对象有关系
        - m..n：表示另一个类的一个对象与该类最少m，最多n个对象有关系 (m≤n)
- **聚合（Aggregation）关系**：表示整体与部分的关系。在聚合关系中，成员对象是整体对象的一部分，但是成员对象可以脱离整体对象独立存在。在UML中，聚合关系用带空心菱形的直线表示。
![聚合关系](http://www.uml.org.cn/oobject/images/2012112319.jpg)
- **组合（Composition）关系**：也表示类之间整体和部分的关系，但是在组合关系中整体对象可以控制成员对象的生命周期，一旦整体对象不存在，成员对象也将不存在，成员对象与整体对象之间具有同生共死的关系。在UML中，组合关系用带实心菱形的直线表示。
![组合关系](http://www.uml.org.cn/oobject/images/20121123110.jpg)
- **依赖（Dependency）关系**：一种使用关系，特定事物的改变有可能会影响到使用该事物的其他事物，在需要表示一个事物使用另一个事物时使用依赖关系。大多数情况下，依赖关系体现在某个类的方法使用另一个类的对象作为参数。用带箭头的虚线表示，由依赖的一方指向被依赖的一方。
![依赖关系](http://www.uml.org.cn/oobject/images/20121123111.jpg)
- **泛化（Generalization）关系**：用于描述父类与子类之间的关系，父类又称作基类或超类，子类又称作派生类。在UML中，泛化关系用带空心三角形的直线来表示。
![泛化关系](http://www.uml.org.cn/oobject/images/20121123112.jpg)
- **实现（Implementation）关系**：是用来规定接口和实现接口的类或者构建结构的关系，接口是操作的集合，而这些操作就用于规定类或者构建的一种服务。接口之间也可以有与类之间关系类似的继承关系和依赖关系，但是接口和类之间还存在一种实现关系(Realization)，在这种关系中，类实现了接口，类中的操作实现了接口中所声明的操作。在UML中，类与接口之间的实现关系用带空心三角形的虚线来表示。
![实现关系](http://www.uml.org.cn/oobject/images/20121123114.jpg)

## 参考

- [统一建模语音百科](https://baike.baidu.com/item/%E7%BB%9F%E4%B8%80%E5%BB%BA%E6%A8%A1%E8%AF%AD%E8%A8%80/3160571?fr=aladdin&fromid=446747&fromtitle=UML)
- [深入浅出UML类图](http://www.uml.org.cn/oobject/201211231.asp)
- [浅谈UML的概念和模型之UML九种图](http://blog.csdn.net/jiuqiyuliang/article/details/8552956/)
- [UML的9种图例解析](http://blog.csdn.net/fatherican/article/details/44966891)