---
title: java-集合
comments: true
tags:
  - Java
categories:
  - 01.编程语言
  - 02.Java
date: 2018-04-09 21:43:16
---
## 1 集合遍历

### 1.1 迭代器（实现 Iterator<E> 接口的实例）

- 检查是否有尚未访问的元素。
- 访问集合中的下一个元素。
- 删除集合的最后访问元素。

### 1.2 for-each循环

- for-each循环遍历任何实现类实现Iterable接口的集合。

`ps:`不能使用for-each循环从集合中删除元素，将抛出ConcurrentModificationException异常。

### 1.3 forEach()方法

- Iterable接口包含一个新的 forEach(Consumer action)方法。

```java
public static void main(String[] args) {
    // Create a list of strings
    List<String> names = new ArrayList<>();
    names.add("A");
    names.add("B");
    names.add("C");

    names.forEach(System.out::println);
  }
```
<!--more-->

### 2 集合（Set接口）（唯一对象的集合）

- 集合是唯一元素的集合。当向集合添加重复元素时，它们将被忽略。
- Java最多允许一个Set中的一个空元素。 
- Set 中元素的排序并不重要。Java不保证 Set 中元素的排序。

### 2.1 数学集

- HashSet 类：不保证顺序元素
- LinkedHashSet 类：保证插入元素顺序

### 2.2 排序集

SortedSet 接口表示Java集合中的排序集合框架。
- 元素实现Comparable接口，将使用compareTo()方法排序，称之为自然排序；
- 传递一个比较器自定义排序；
- 若指定Comparator，则用Comparator排序而忽略Comparable。
- TreeSet是SortedSet接口的一个实现。

### 2.3 导航集（有序集）

NavigableSet 表示Java集合中的可导航集合框架。NavigableSet 接口继承了SortedSet接口和扩展 SortedSet 。
- TreeSet 类是 NavigableSet 接口的实现类之一。

## 3 列表（List接口）（有序、可重复）

- ArrayList：访问快，添加删除慢
- LinkedList：访问慢，添加删除快
- LinkIterator接口（继承Iterator接口）遍历列表

## 4 队列（Queue接口）（先进先出FIFO）

- LinkedList：简单的队列允许在尾部插入和从头部移除。
- PriorityQueue：优先级队列为每个元素分配优先级，并允许从队列中删除具有最高优先级的元素。
- DelayQueue：延迟队列向每个元素添加延迟，并仅在其延迟已过去时删除该元素。
- Deque、ArrayDeque、LinkedList（FIFO或LIFO）：双端队列允许其元件从头部和尾部插入和移除。
- BlockingQueue接口（线程安全、适用于生产者/消费者）、ArrayBlockingQueue、LinkedBlockingQueue、PriorityBlockingQueue、SynchronousQueue：阻塞队列阻塞线程，当线程已满时向其添加元素，当线程为空时，它阻止线程从中删除元素。
- TransferQueue：传输队列是阻塞队列，其中对象的切换发生在生产者线程和消费者线程之间。
- 阻塞双端队列是双端队列和阻塞队列的组合。

## 5 映射（Map<K,V>接口） （键不能重复）

- HashMap
- LinkedHashMap
- WeakHashMap

## 6 Collection 类

该类中包含许多静态的辅助方法用于处理集合，如排序、搜索等。

## 注意

本文主要用于记录个人不明了之处，故可能忽略许多知识点，如有需要，请自行查找相关资料，谢谢。