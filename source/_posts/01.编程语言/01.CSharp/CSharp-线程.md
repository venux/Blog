---
title: 线程笔记
comments: true
tags:
  - APS.NET
  - 'C#'
categories:
  - 01.编程语言
  - 01.CSharp
date: 2017-10-13 19:26:03
---
## 1 基础知识

### 1.1 进程&线程

- **进程**：应用程序的实例要使用的资源的集合。
    - 每个进程都被赋予一个虚拟地址空间，确保进程中的数据和代码无法由另一个进程访问，确保了应用程序实例的健壮性；
    - 进程无法访问OS内核代码，保证系统稳定性和安全性。
- 线程
<!--more-->

### 1.2 垃圾回收背后的线程情况

执行垃圾回收时，CLR 必须挂起（暂停）所有线程，遍历它们的栈来查找根以便对堆中的对象进行标记，再次遍历它们的栈（有的对象在压缩期间发生了移动，所以要更新它们的根），再恢复所有的线程。所以，较少线程的数量会显著提升垃圾回收的性能。

### 1.3 调试背后的线程情况

每次使用调试器并遇到断电，Windows 都会挂起正在调试的应用程序中的所有线程，并在单步执行或者运行应用程序后恢复所有线程。所以，线程越多，调试体验越差。

## 1.4 

## 2 深入

## 建议

### 2.1 要构建高性能应用程序和组件，就应该尽量避免上下文切换；
### 2.2 应尽量使用线程池来执行异步操作；


## 参考