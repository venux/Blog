---
title: Gradle
comments: true
tags:
  - Java
  - 工具
categories:
  - 01.编程语言
  - 02.Java
date: 2018-06-10 22:05:19
---
## 1. 介绍

一个自动化构建工具，用于加速开发者生产率，特点：
- Build Anything;
- Automate Everything;
- Deliver Faster;

<!--more-->

## 2. 安装 & 配置 & 测试 & 升级

### 2.1 前提

JDK 1.7 版本以上。

### 2.2 安装

- 通过包管理工具（SDKMAN、Homebrew、Scoop、Chocolatey、MacPorts）安装，具体参加[官网](https://gradle.org/install/#helpful-information)；
- 手动安装，下载二进制压缩包、解压到指定目录；

### 2.3 配置

将 $GradlePaht\bin 添加到 Path 环境变量中；

### 2.4 测试

gradle -v

### 2.5 升级

使用 Gradle Wrapper 可方便快捷升级 Gradle。具体命令：`$ ./gradlew wrapper --gradle-version=4.8 --distribution-type=bin`。

## 3. Gradle Wrapper（简称 Wrapper）

推荐使用 Gradle Wrapper 来执行 Gradle 构建。它是一串脚本用于动态调用指定版本的 Gradle，若不存在，则先下载。这样，开发者可快速开始和运行 Gradle 项目，而不必按照手册安装流程，从而节约时间和金钱。具体流程如下图：
![Gradle Wrapper](https://docs.gradle.org/4.8/userguide/img/wrapper-workflow.png)

### 3.1 优点

- 标准化指定 Gradle 版本的项目，使得构建更加可靠和健壮。
- 在不同环境或不同用户之间，提供多个版本 Gradle，更加简单方便；

### 3.2 新建 Gradle 项目并添加 Wrapper

通常要生成 Wrapper 文件需要向安装一个 Gradle，庆幸的是这是一次性的。每个 Gradle 都自带一个叫 wrapper 的任务。
运行 `gradle wrapper` 命令用以生成 Wrapper 文件，具体路径 `gradle/wrapper`。
**gradle-wrapper.properties**文件用以存储 Gradle 发布包信息，具体如下：
- Gradle 发布包的服务网路路径；
- Gradle 发布包的类型，默认为 `-bin` 二进制包，只包括运行时而不包括示例代码和文档；
- Gradle 发布包的版本，默认为生成 Wrapper 文件时的版本；
可通过参数指定配置选项：
- `--gradle-version`：指定 Gradle 版本。
- `--distribution-type`：发布包类型，可选择 **bin** 和 **all**。默认为 **bin**。
- `--gradle-distribution-url`：发布包地址，该选项会忽略`--gradle-version`和`--distribution-type`参数。
- `--gradle-distribution-sha256-sum`：校验发布包 SHA256 HASH 码。
`示例`：gradle wrapper --gradle-version 4.0 --distribution-type all
`注意：`若所有开发者和环境均需使用 Wrapper 文件，请将其添加到版本管理工具中。部分公司不允许将二进制文件添加到版本管理工具，这样就没其他解决方案了。

### 3.3 Gradle Wrapper 文件结构

[Gradle Wrapper 文件结构](/images/posts/Gradle Wrapper文件结构.png)

### 3.4 运行已有 Wrapper 的项目

### 3.5 通过 Wrapper 升级 Gradle

## 2. 入门



## 参考

1 [博客](http://www.venux.cn)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。