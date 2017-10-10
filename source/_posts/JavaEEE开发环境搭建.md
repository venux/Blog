---
title: JavaEEE开发环境搭建
comments: true
date: 2017-09-18 18:46:11
tags: 
    - Java
    - Tomcat
    - Eclipse    
categories: Java
---

## 1.Java环境

### 1.1 [Java下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

### 1.2 环境变量配置

1. **JAVA_HOME**:C:\Program Files\Java\jdk1.8.0_144（注：结尾不加分号）
2. **PATH**:%JAVA_HOME%\bin;
3. **CLASS_PATH**:.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

### 1.3 测试

- **java-version**:版本号
- **java**:Java环境
- **javac**:Java编译器

### 1.4 Eclipse集成

- **默认**：Eclipse 会自动关联环境变量中配置的 JDK。
- **手动**：“Window”–“Preferences”–“Java”–“Installed JREs”–“Add”–“Standard VM”–选择jdk安装目录。 （多个版本的JDK手工进行配置）

<!--more-->

## 2.Tomcat服务器

### 2.1 [Tomcat下载](http://tomcat.apache.org/download-90.cgi)

### 2.2 环境变量配置

1. **CATALINA_HOME**：C:\Program Files\Tomcat 8.5（注：结尾不加分号）
2. **PATH**:%CATALINA_HOME%\bin;

### 2.3 测试

- **localhost:8080**:Tomcat默认主页

### 2.4 Eclipse集成

- “Window”–“Preferences”–“Server”–“Runtime Environment”–“Add”–选择Tomcat安装目录。

## 3.Eclipse IDE

### 3.1 [Eclipse下载](https://www.eclipse.org/downloads/)

## 4.Maven

基于项目对象模型POM（Project Object Model），用来管理项目的构建、报告和文档的软件项目管理工具。主要提供：
- 统一开发规范和工具
- 统一管理 jar 包

### 4.1 [Maven下载](http://maven.apache.org/download.cgi)

### 4.2 环境变量配置

1. **MAVEN_HOME**:C:\Program Files\apache-maven-3.5.0（注：结尾不加分号）
2. **PATH**:%MAVEN_HOME%\lib;
3. **MAVEN_OPTS**: -Xms128m -Xmx512m;(设置Maven可用内存大小)

### 4.3 测试

- **maven -v**:版本号

### 4.4 配置文件

`‪C:\Program Files\apache-maven-3.5.0\conf\settings.xml`


### 参考

1 [Maven官网](http://maven.apache.org/index.html)
2 [Maven入门](http://blog.csdn.net/column/details/maven-it.html)
3 [Eclipse Maven插件安装](http://blog.csdn.net/lfsfxy9/article/details/9397937)