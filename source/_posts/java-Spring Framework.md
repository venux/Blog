---
title: java-Spring Framework
comments: true
tags:
  - Java
  - Spring
  - Spring Framework
categories: 
  - Java
  - Spring
  - Spring Framework
date: 2018-04-29 11:09:12
---
## 1 简介

Spring框架为现代基于Java的企业应用程序提供了一个全面的编程和配置模型 - 在任何类型的部署平台上。 Spring的一个关键元素是应用程序级别的基础架构支持：Spring侧重于企业应用程序的“管道”，以便团队可以专注于应用程序级别的业务逻辑，而不必与特定部署环境形成不必要的联系。

The Spring Framework provides a comprehensive programming and configuration model for modern Java-based enterprise applications - on any kind of deployment platform. A key element of Spring is infrastructural support at the application level: Spring focuses on the "plumbing" of enterprise applications so that teams can focus on application-level business logic, without unnecessary ties to specific deployment environments.

<!--more-->

## 2 特性

- **Core technologies**: dependency injection, events, resources, i18n, validation, data binding, type conversion, SpEL, AOP.
- **Testing**: mock objects, TestContext framework, Spring MVC Test, WebTestClient.
- **Data Access**: transactions, DAO support, JDBC, ORM, Marshalling XML.
- **Spring MVC and Spring WebFlux web frameworks**
- **Integration**: remoting, JMS, JCA, JMX, email, tasks, scheduling, cache.
- **Languages**: Kotlin, Groovy, dynamic languages.

## 3 设计理念

- **Provide choice at every level（各个层面都提供选择）.** Spring lets you defer design decisions as late as possible. For example, you can switch persistence providers through configuration without changing your code. The same is true for many other infrastructure concerns and integration with third-party APIs.
- **Accommodate diverse perspectives（支持不同的观点）.**Spring embraces flexibility and is not opinionated about how things should be done. It supports a wide range of application needs with different perspectives.
- **Maintain strong backward compatibility（保持向后兼容）.**Spring’s evolution has been carefully managed to force few breaking changes between versions. Spring supports a carefully chosen range of JDK versions and third-party libraries to facilitate maintenance of applications and libraries that depend on Spring.
- **Care about API design（关注API设计）.** The Spring team puts a lot of thought and time into making APIs that are intuitive and that hold up across many versions and many years.
- **Set high standards for code quality（高代码标准规范）.** The Spring Framework puts a strong emphasis on meaningful, current, and accurate Javadoc. It is one of very few projects that can claim clean code structure with no circular dependencies between packages.

## 4 核心

### 4.1 Ioc container



## 参考

1 [Spring Framework 预览（Version 5.0.5.RELEASE）](https://docs.spring.io/spring/docs/current/spring-framework-reference/overview.html#overview)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。