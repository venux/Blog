---
title: java-Tomcat
comments: true
tags:
  - Java
categories:
  - 01.编程语言
  - 02.Java
date: 2018-04-18 22:13:30
---
## 1 介绍

Apache 基金会下的一款开源的 web 服务器。

## 2.下载

[Tomcat下载](http://tomcat.apache.org/download-90.cgi)

## 3. 安装

解压缩到指定目录

### 3.1 目录结构

- bin：二进制执行文件。里面最常用的文件是startup.bat，如果是 Linux 或 Mac 系统启动文件为 startup.sh。
- conf:配置目录。里面最核心的文件是server.xml。可以在里面改端口号等。默认端口号是8080，也就是说，此端口号不能被其他应用程序占用。
- lib：库文件。tomcat运行时需要的jar包所在的目录
- logs：日志
- temp：临时产生的文件，即缓存
- webapps：web的应用程序。web应用放置到此目录下浏览器可以直接访问
- work：编译以后的class文件。

## 4. 配置

### 4.1 环境变量配置

1. **CATALINA_HOME**：C:\Program Files\Tomcat 8.5（注：结尾不加分号）
2. **PATH**:%CATALINA_HOME%\bin;
3. **CLASS_PATH**:%CATALINA_HOME%\lib;

### 4.2 配置文件

$CATALINA_HOME 目录下的 conf 目录，核心配置文件 server.xml。

## 5. 启动

进入 $CATALINA_HOME 目录下的 bin 目录，运行 startup.bat 即可。

### 6. 测试

- **localhost:8080**:Tomcat默认主页

### 7 Eclipse集成

- “Window”–“Preferences”–“Server”–“Runtime Environment”–“Add”–选择Tomcat安装目录。


<!--more-->

## 参考

1 [博客](http://www.venux.cn)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。