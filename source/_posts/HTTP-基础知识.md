---
title: HTTP笔记
comments: true
date: 2017-09-05 17:19:28
tags: HTTP
categories: HTTP
---

![图一](/images/posts/HTTP1.png)

## 1.应用层

决定向用户提供应用服务时通信的活动。
TCP/IP协议簇内预存了各类通用的应用服务，如FTP文件传输协议，DNS域名系统服务。HTTP协议也在该层。

## 2.传输层

对上层应用层提供处于网络连接中两台计算机间的数据传输。
在传输层有两个性质不同的协议：TCP（Transmission Control Protocol，传输控制协议）和UDP（User Data Protocol，用户数据报协议）。

## 3.网络层

处理在网络上流动的数据包（网络传输的最小数据单位），该层规定了通过怎样的路径到达对方计算机，并把数据包传送给对方。

<!--more-->

## 4.链路层

用来处理连接网络的硬件部分，包括控制操作系统，硬件设备驱动,网络适配器（网卡）及光纤等物理可见部分。

## 5.IP协议

IP（Internet Protocol）网际协议位于网络层。TCP/IP协议簇中的IP指的就是网际协议。
作用是把各种数据包发送给对方，而要确保发送正确需满足各类条件，其中两个重要的就是IP地址和MAC（Media Access Control Address）地址。
IP地址指明节点被分配的地址，MAC地址指网卡的固定地址，可配对。IP地址可变换而MAC地址基本不变。

## 6.ARP协议

ARP（Address Resolution Protocol）协议是一种用以解析地址的协议，根据通信方的IP地址反查出对应的MAC地址。

## 7.TCP协议

TCP协议位于传输层，提供可靠的字节流服务。采用三次握手（three-way handshaking）策略：发送端先发送带SYN（synchronize）标志的数据包给对方，接收端接受到后回传一个带SYN/ACK（acknowledgement）标志的数据包确认，最后，发送端回传ACK标志的数据包，表示握手结束。

## 8.DNS服务

DNS（Domain Name System）服务用于域名到IP地址之间解析，位于应用层。
![图二](/images/posts/HTTP2.png)

## 9.URI（Uniform Resource Identifier）统一资源标识符

由某个协议方案表示的资源的定位标识符。

### 9.1Uniform 

规定统一的格式可方便处理多种不同类型的资源，而不用根据上下文环境来识别资源指定的访问方式。

### 9.2Resource

 资源的定义是可标识的任何东西。

### 9.3Identifier 

表示可标识的对象，即标识符。

## 10.URL（Uniform Resource Locator）统一资源定位符

资源的地点，是URI的子集。

## 参考

1 图解HTTP（第1章：基础知识）