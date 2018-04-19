---
title: java-Maven
comments: true
tags:
  - Java
  - Maven
categories: Java
date: 2018-04-15 17:36:50
---
## 1 介绍

Maven 是一个项目构建和管理的自动化工具，提供了帮助管理 构建、文档、报告、依赖、scms、发布、分发的方法。可以方便的编译代码、进行依赖管理、管理二进制库等等。

Maven 使用惯例优于配置的原则 。它要求在没有定制之前，所有的项目都有如下的结构：

目录|目的
----|----
${basedir}|存放 pom.xml和所有的子目录
${basedir}/src/main/java|项目的 java源代码
${basedir}/src/main/resources|项目的资源，比如说 property文件
${basedir}/src/test/java|项目的测试类，比如说 JUnit代码
${basedir}/src/test/resources|测试使用的资源

一个 maven 项目在默认情况下会产生 JAR 文件，另外 ，编译后 的 classes 会放在 ${basedir}/target/classes 下面， JAR 文件会放在 ${basedir}/target 下面。
<!--more-->

## 2 下载&安装&配置

### 2.1 前提

需安装配置 java 开发环境

### 2.2 下载地址

[Maven下载](http://maven.apache.org/download.cgi)

### 2.3 安装

直接解压缩到指定目录

### 2.4 配置

配置文件：`‪C:\Program Files\apache-maven-3.5.0\conf\settings.xml`
1. **MAVEN_HOME**:C:\Program Files\apache-maven-3.5.0（注：结尾不加分号）
2. **PATH**:%MAVEN_HOME%\bin;
3. **MAVEN_OPTS**: -Xms128m -Xmx512m;(设置Maven可用内存大小)
4. 修改本地仓库路径：setting.xml 中的 localRepository。

### 2.5 测试

- **maven -v**:版本号

### 2.6 集成IDE

- Eclipse IDE：[M2Eclipse](https://www.eclipse.org/m2e/)，直接搜索 Maven 即可。
  - Launching Maven builds from within Eclipse
  - Dependency management for Eclipse build path based on Maven’s pom.xml
  - Resolving Maven dependencies from the Eclipse workspace without installing to local Maven repository
  - Automatic downloading of the required dependencies and sources from the remote Maven repositories
  - Wizards for creating new Maven projects, pom.xml and to enable Maven support on existing projects
  - Quick search for dependencies in remote Maven repositories
  - Quick fixes in the Java editor for looking up required dependencies/jars by the class or package name
  - Integration with other Eclipse tools, such as WTP, AJDT, Mylyn, Subclipse and others.
- Intellij IDEA:[Intellij IDEA-Maven](https://www.jetbrains.com/help/idea/maven.html)

## 3 核心概念

### 3.1 POM（Project Object Model）[ps:个人理解为类似于VS的csproj文件，用于管理项目]

pom 是一个 xml，是maven工作的基础，在执行 task 或者 goal 时，maven 会去项目根目录下读取 pom.xml 获得需要的配置信息。该文件包括项目的信息和 maven build 项目所需的配置信息，通常有项目信息(如版本、成员)、项目的依赖、插件和 goal 、build 选项等等。
pom 是可继承的，大型项目中，子模块的 pom 需指定父模块的 pom。
节点定义：
- project：pom文件的顶级元素
- modelVersion：所使用的object model版本，为了确保稳定的使用，这个元素是强制性的。除非maven开发者升级模板，否则不需要修改
- groupId：是项目创建团体或组织的唯一标志符，通常是域名倒写，如groupId  org.apache.maven.plugins就是为所有maven插件预留的
- artifactId：是项目artifact唯一的基地址名
- packaging：artifact打包的方式，如jar、war、ear等等。默认为jar。这个不仅表示项目最终产生何种后缀的文件，也表示build过程使用什么样的lifecycle。
- version：artifact的版本，通常能看见为类似0.0.1-SNAPSHOT，其中SNAPSHOT表示项目开发中，为开发版本
- name：表示项目的展现名，在maven生成的文档中使用
- url：表示项目的地址，在maven生成的文档中使用
- description：表示项目的描述，在maven生成的文档中使用
- dependencies：表示依赖，在子节点dependencies中添加具体依赖的groupId - artifactId和version
- build：表示build配置
- parent：表示父pom

### 3.2 Artifact（类似于 nuget 中的包）

- 需指定项目要产生的文件，如 jar，源文件，二进制，war，pom 等，类似于 VS 中的项目类型。
- groupId:artifactId:version 组成的标识符唯一识别，唯一确定了一个 artifact。
- 需要被使用(依赖)的 artifact 都要放在仓库(见Repository)中。
 
### 3.3 Repositories（仓储）

- 主要用来存储 Artifact。
- 可分为本地和远程。
  - 本地对 Windows 系统存放于`用户/.m2/repository`，可修改。

### 3.4 Build Lifecycle（构建生存周期）

指一个项目的构建过程，由 phase（片段） 构成。分三种：
- default：处理项目的部署，大致流程：
  1. validate 验证项目是否正确以及必须的信息是否可用
  2. compile 编译源代码
  3. test 测试编译后的代码，即执行单元测试代码
  4. package 打包编译后的代码，在target目录下生成package文件
  5. integration-test 处理package以便需要时可以部署到集成测试环境
  6. verify 检验package是否有效并且达到质量标准
  7. install 安装package到本地仓库，方便本地其它项目使用
  8. deploy 部署，拷贝最终的package到远程仓库和替他开发这或项目共享，在集成或发布环境完成
- clean：处理项目的清理
- site：处理项目的文档生成

注意：phase 是有序的，执行指定的 phase 时，会先执行完之前的 phase。

### 3.5 Goal（任务）

表示一个特定的任务，区别于 build。

- mvn compile：编译
- mvn package：打包
- mvn deploy：部署
- mvn clean install：先执行 clean 之前的 phase，在执行 clean，install。
- mvn install：安装到本地

### 3.6 Archetype（原型）

类似于 .net core 的项目模板

## 4 常用参数

- mvn -e：显示详细错误
- mvn -U：强制更新snapshot类型的插件或依赖库（否则maven一天只会更新一次snapshot依赖）
- mvn -o：运行offline模式，不联网更新依赖
- mvn -N：仅在当前项目模块执行命令，关闭reactor
- mvn -pl：module_name在指定模块上执行命令
- mvn -ff：在递归执行命令过程中，一旦发生错误就直接退出
- mvn -Dxxx=yyy：指定java全局属性
- mvn -Pxxx：引用profile xxx
- mvn test-compile：编译测试代码
- mvn test：运行程序中的单元测试
- mvn compile：编译项目
- mvn package：打包，此时target目录下会出现maven-quickstart-1.0-SNAPSHOT.jar文件，即为打包后文件
- mvn install：打包并安装到本地仓库，此时本机仓库会新增maven-quickstart-1.0-SNAPSHOT.jar文件。每个phase都可以作为goal，也可以联合，如之前介绍的mvn clean install
- mvn archetype:generate：创建maven项目
- mvn package：打包，上面已经介绍过了
- mvn package：-Prelease打包，并生成部署用的包，比如deploy/*.tgz
- mvn install：打包并安装到本地库
- mvn eclipse:eclipse：生成eclipse项目文件
- mvn eclipse:clean：清除eclipse项目文件
- mvn site：生成项目相关信息的网站
- mvn -Dwtpversion=2.0：指定maven版本
- mvn -Dmaven.test.skip=true：如果命令包含了test phase，则忽略单元测试
- mvn -DuserProp=filePath：指定用户自定义配置文件位置
- mvn -DdownloadSources=true -Declipse.addVersionToProjectName=true eclipse:eclipse：生成eclipse项目文件，尝试从仓库下载源代码，并且生成的项目包含模块版本（注意如果使用公用POM，上述的开关缺省已打开）
- mvn -Dsurefire.useFile=false：如果执行单元测试出错，用该命令可以在console输出失败的单元测试及相关信息
- set MAVEN_OPTS=-Xmx512m -XX:MaxPermSize=256m：调大jvm内存和持久代，maven/jvm out of memory error
- mvn -X：maven log level设定为debug在运行
- mvn debug：运行jpda允许remote debug
- mvn –help 帮助

## 参考

1 [Maven官网](http://maven.apache.org/index.html)
2 [Maven入门](http://blog.csdn.net/column/details/maven-it.html)
3 [Maven介绍，包括作用、核心概念、用法、常用命令、扩展及配置](http://www.trinea.cn/android/maven/)
4 [Maven入门介绍](http://www.oracle.com/technetwork/cn/community/java/apache-maven-getting-started-1-406235-zhs.html)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。