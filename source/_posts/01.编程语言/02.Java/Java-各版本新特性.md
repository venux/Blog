---
title: Java各版本新特性
comments: true
tags:
  - Java
categories:
  - 01.编程语言
  - 02.Java
date: 2018-04-01 22:45:48
---
## 1 Java8 新特性（2014/3/18）

- **Lambda 表达式** − Lambda允许把函数作为一个方法的参数（函数作为参数传递进方法中。
```java
// 使用 java 7 排序
private void sortUsingJava7(List<String> names){   
  Collections.sort(names, new Comparator<String>() {
      @Override
      public int compare(String s1, String s2) {
        return s1.compareTo(s2);
      }
  });
}

// 使用 java 8 排序
private void sortUsingJava8(List<String> names){
  Collections.sort(names, (s1, s2) -> s1.compareTo(s2));
}
```
- **方法引用** − 方法引用提供了非常有用的语法，可以直接引用已有Java类或对象（实例）的方法或构造器。与lambda联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码。
- **默认方法** − 默认方法就是一个在接口里面有了一个实现的方法。
```java
public class Java8Tester {
   public static void main(String args[]){
      Vehicle vehicle = new Car();
      vehicle.print();
   }
}
 
interface Vehicle {
   default void print(){
      System.out.println("我是一辆车!");
   }
    
   static void blowHorn(){
      System.out.println("按喇叭!!!");
   }
}
 
interface FourWheeler {
   default void print(){
      System.out.println("我是一辆四轮车!");
   }
}
 
class Car implements Vehicle, FourWheeler {
   public void print(){
      Vehicle.super.print();
      FourWheeler.super.print();
      Vehicle.blowHorn();
      System.out.println("我是一辆汽车!");
   }
}
```
- 新工具 − 新的编译工具，如：Nashorn引擎 jjs、 类依赖分析器jdeps。
- **Stream API（链式编程）** −新添加的Stream API（java.util.stream） 把真正的函数式编程风格引入到Java中。
  - 元素是特定类型的对象，形成一个队列。 Java中的Stream并不会存储元素，而是按需计算。
  - 数据源 流的来源。 可以是集合，数组，I/O channel， 产生器generator 等。
  - 聚合操作 类似SQL语句一样的操作， 比如filter, map, reduce, find, match, sorted等。  
  - Pipelining: 中间操作都会返回流对象本身。 这样多个操作可以串联成一个管道， 如同流式风格（fluent style）。 这样做可以对操作进行优化， 比如延迟执行(laziness)和短路( short-circuiting)。
  - 内部迭代： 以前对集合遍历都是通过Iterator或者For-Each的方式, 显式的在集合外部进行迭代， 这叫做外部迭代。 Stream提供了内部迭代的方式， 通过访问者模式(Visitor)实现。
```java
List<String>strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
List<String> filtered = strings.stream()
                                .filter(string -> !string.isEmpty())
                                .collect(Collectors.toList());
 
System.out.println("筛选列表: " + filtered);
String mergedString = strings.stream()
                              .filter(string -> !string.isEmpty())
                              .collect(Collectors.joining(", "));
System.out.println("合并字符串: " + mergedString);
```
- Date Time API − 加强对日期与时间的处理。
- Optional 类 − Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常。
- Nashorn, JavaScript 引擎 − Java 8提供了一个新的Nashorn javascript引擎，它允许我们在JVM上运行特定的javascript应用。

<!--more-->

# 2 Java9 新特性（）

# 3 Java10 新特性（2018/3/20）

## 注意

本文主要用于记录个人不明了之处，故可能忽略许多知识点，如有需要，请自行查找相关资料，谢谢。