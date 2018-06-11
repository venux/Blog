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

使用 Gradle Wrapper 可方便快捷升级 Gradle。具体命令：`gradle wrapper --gradle-version=4.8 --distribution-type=bin`。

### 2.6 Gradle 文件结构

- build.gradle：构建 Gradle 脚本；
- settings.gradle：指定哪些项目需要构建，可配置多个项目；
- gradle
    - wrapper
        - gradle-wrapper.jar：包含下载 Gradle 发布包的编译后代码；
        - gradle-wrapper.properties：运行时配置；
- gradlew：Unix 系统的启动脚本；
- gradlew.bat：Windows 系统的启动脚本；

## 3. Gradle Wrapper（简称 Wrapper）

**推荐使用 Gradle Wrapper 来执行 Gradle 构建。**它是一串脚本用于动态调用指定版本的 Gradle，若不存在，则先下载。这样，开发者可快速开始和运行 Gradle 项目，而不必按照手册安装流程，从而节约时间和金钱。具体流程如下图：
![Gradle Wrapper](https://docs.gradle.org/4.8/userguide/img/wrapper-workflow.png)

### 3.1 优点

- 标准化指定 Gradle 版本的项目，使得构建更加可靠和健壮。
- 在不同环境或不同用户之间，提供多个版本 Gradle，更加简单方便；
- 标准化；
- 可靠性；
- 可控制性；
- 健壮性；

### 3.2 新建 Gradle Wrapper

通常要生成 Wrapper 文件需要向安装一个 Gradle，庆幸的是这是一次性的。每个 Gradle 都自带一个叫 wrapper 的任务。
运行 `gradle wrapper` 命令用以生成 Wrapper 文件，具体路径 `gradle/wrapper`。

`注意：`若所有开发者和环境均需使用 Wrapper 文件，请将其添加到版本管理工具中。部分公司不允许将二进制文件添加到版本管理工具，这样就没其他解决方案了。

#### 3.2.1 参数配置选项：

- `--gradle-version`：指定 Gradle 版本。
- `--distribution-type`：发布包类型，可选择 **bin** 和 **all**。默认为 **bin**。
- `--gradle-distribution-url`：发布包地址，该选项会忽略`--gradle-version`和`--distribution-type`参数。
- `--gradle-distribution-sha256-sum`：校验发布包 SHA256 HASH 码。

`示例`：gradle wrapper --gradle-version 4.0 --distribution-type all 

#### 3.2.2 gradle-wrapper.properties文件

主要用以存储 Gradle 发布包信息，具体如下：
- Gradle 发布包的服务网路路径；
- Gradle 发布包的类型，默认为 `-bin` 二进制包，只包括运行时而不包括示例代码和文档；
- Gradle 发布包的版本，默认为生成 Wrapper 文件时的版本；

### 3.3 使用 Gradle Wrapper

根据不同系统，运行 `gradlew` 或 `gradlew.bat` 脚本来取代 `gradle` 命令。
`ps`：
- 若本机未装配置版本的 Gradle，则会自动下载并保持到本机中。若配置未变，则复用。
- 多个项目可能分别有 Wrapper 脚本，请确认执行正确的脚本。

### 3.4 升级 Gradle Wrapper

- 手动修改配置文件`gradle-wrapper.properties`的`distributionUrl`属性；
- **推荐**执行`gradle wrapper` task 时，指定版本信息，默认为当前版本；

### 3.5 自定义 Gradle Wrapper

默认设置可满足大多数要求，然而可通过修改`build.gradle`配置来自定义相关配置。
块节点为`wrapper`，具体参数详情请参考[Wrapper](https://docs.gradle.org/4.8/dsl/org.gradle.api.tasks.wrapper.Wrapper.html)。

## 4. 创建一个新的 Gradle 构建

### 4.1 初始化 

`gradle init`命令，该命令可[创建不同类型的项目](https://docs.gradle.org/4.7/userguide/build_init_plugin.html?&_ga=2.66304238.1375004092.1528446888-1875152485.1526436983#sec:build_init_types)，且可将 Maven 项目（pom.xml）转换为 Gradle 项目。

### 4.2 创建 task

Gradle 提供一系列 API（使用 Groovy 或 基于 Kotlin 的 DSL 语言） 用于创建和配置 task。一个 Project 包括一个 Task 集合，每个单独提供一些基础功能。[具体详情](https://docs.gradle.org/4.7/userguide/more_about_tasks.html)
```gradle
task copy(type: Copy, group: "Custom", description: "Copies sources to the dest directory") {
    from "src"
    into "dest"
}
```

### 4.3 应用插件

Gradle 提供一系列[插件](http://plugins.gradle.org/?_ga=2.27464572.1375004092.1528446888-1875152485.1526436983)。
`ps`：plugins{} 代码块放置在配置文件最上方。
```gradle
plugins{
    id "base"
}
```

### 4.4 查看可用的 task

`gradle tasks` 命令

### 4.5 分析 & 调试构建

Gradle 提供一个叫`build scan`（专业版功能）的方式用于构建过程可视化。通过使用`--scan`命令或者对项目应用`scan`插件即可。

### 4.6 查看可用的 properties

`gradle properties` 命令

## 5. 创建构建浏览（Build Scans）

构建浏览是一个用于展示构建的 what happened and why 的工具，具有可分享，集中管理特性。可免费发布到 [https://scans.gradle.com](https://scans.gradle.com)。方式：
- `--scan`命令参数；
- 插件
    ```gradle
    plugins {
        id 'com.gradle.build-scan' version '1.13.3' 
    }
    ```

同意许可协议，或者直接配置好
```gradle
buildScan {
    termsOfServiceUrl = 'https://gradle.com/terms-of-service'
    termsOfServiceAgree = 'yes'
}
```

对所有构建进行默认配置 build scan，在`~/.gradle/init.d`目录中创建 gradle 文件用于默认 build。
```gradle
initscript {
    repositories {
        gradlePluginPortal()
    }

    dependencies {
        classpath 'com.gradle:build-scan-plugin:1.13.3'
    }
}

rootProject {
    apply plugin: com.gradle.scan.plugin.BuildScanPlugin

    buildScan {
        termsOfServiceUrl = 'https://gradle.com/terms-of-service'
        termsOfServiceAgree = 'yes'
    }
}
```

[官方用户手册](https://docs.gradle.com/build-scan-plugin/)

## 参考

1 [博客](http://www.venux.cn)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。