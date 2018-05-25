---
title: java-反射
comments: true
tags:
  - Java
categories:
  - 01.编程语言
  - 02.Java
date: 2018-04-09 23:36:43
---
## 1 Class（java.lang.Class）

该类是反射的核心，获取类的Class对象引用方式：
- 使用类文字，如Test.class、double.class（等价于Doubel.TYPE）和void.class；
- 使用Object类的getClass()方法
- 使用Class类的forName()静态方法

<!--more-->

## 2 字段

- getFields()方法返回所有可访问的公共字段在类中声明或继承自超类。
- getDeclaredFields()方法返回所有字段只出现在类的声明中(不是从继承的字段)。
- getField(String name)和 getDeclaredField(String name)通过字段名获取 Field 对象。

## 3 方法

- java.lang.reflect.Method（继承自抽象类Executable） 类的实例表示一个方法。
- java.lang.reflect.Constructor（继承自抽象类Executable） 类的实例表示一个构造函数。
- Parameter 类：可执行文件中的参数。默认情况，参数名称不存储在类文件中，而类似于arg0,arg1。
- TypeVariable：通用方法或构造函数的类型参数。
- Executable类（抽象）：可执行。
  - getParameters()：获取参数数组；
  - getExceptionTypes()：获取异常数组；
  - getTypeParameters()：获取类型参数数组；
  - getModifiers()：获取修饰符

```java
Method[]  getMethods()
Method[]  getDeclaredMethods()：返回当前类的所有声明的构造函数。
Method getMethod(String name,  Class...  parameterTypes)
Method getDeclaredMethod(String name,  Class...  parameterTypes)
```

## 4 构造函数

- Constructor[] getConstructors()：返回当前和超类的所有公共构造函数。
- Constructor[]  getDeclaredConstructors()
- Constructor<T> getConstructor(Class...  parameterTypes)
- Constructor<T> getDeclaredConstructor(Class...  parameterTypes)

## 注意

本文主要用于记录个人不明了之处，故可能忽略许多知识点，如有需要，请自行查找相关资料，谢谢。