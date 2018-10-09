---
title: REST 介绍
comments: true
tags:
  - REST
categories: 
  - 架构
date: 2018-04-30 18:52:12
---
## 1 简介

**REST (Representational State Transfer)** was introduced and defined in **2000** by **Roy Fielding** in his doctoral dissertation（博士论文）. REST is **an architectural style** for **designing distributed systems**. It is **not a standard but a set of constraints（约束）**, such as being **stateless, having a client/server relationship, and a uniform interface**. REST is **not strictly related to HTTP**, but it is most commonly **associated** with it.

<!--more-->

## 2 原则

- **Resources** expose（暴露） easily understood directory structure URIs.
- **Representations** transfer（传递） JSON or XML to represent data objects and attributes.
- **Messages** use HTTP methods explicitly（明确的） (for example, GET, POST, PUT, and DELETE).
- **Stateless** interactions（交互） store no client context on the server between requests. State dependencies limit and restrict scalability（依赖状态限制了可伸缩性）. The client holds session state.

## 3 HTTP 方法

使用 HTTP 方法以便在 HTTP 请求中映射 CRUD(create,retrieve(取回),update,delete) 操作。
幂等（idempotent）：指使用同样的参数，不管重复进行多少次操作，均显示同样的结果。

### 3.1 GET（Retrieve）

- 用于获取信息，即查询操作（Retrieve）。该操作必须是安全的和幂等的；
- 它可能有副作用，但是用户不关心；
- 请求可选择条件。
```HTTP
GET /addresses/1
```

### 3.2 POST（Create）

- 通常用于创建实体，即创建操作（Create）；
- 也可用于更新操作（Update）；
- 非幂等。
```HTTP
POST /addresses
```

### 3.3 PUT（Update）

- 通常用于更新实体，即更新操作（Update）；
- 也可用于创建操作（Create）；
- 幂等（该特性是与 POST 的主要差别）。
*注意：* PUT 替换一个已存在的实体，若只提供该实体的部分字段属性，则其余字段属性会被替换为空字符串或 null。 
```HTTP
PUT /addresses/1
```

### 3.4 DELETE（Delete）

- 通常用于删除实体，即删除操作（Delete）；
*注意：* 删除不一定要立即执行，也可为异步操作或者长时间的请求。
```HTTP
DELETE /addresses/1
```

### 3.5 PATCH（补丁）（Update）

- 通常用于更新实体，**仅更新指定的字符属性**，即更新操作（Update）；
- 幂等
```HTTP
PATCH /addresses/1
```

## HTTP 状态码

- 1XX - informational
- 2XX - success
- 3XX - redirection
- 4XX - client error
- 5XX - server error

## Media types

- Accept：指明客户端接收响应内容的类型，如 `application/json` 告诉服务端返回 JSON；
- Content-Type：指明客户端发送请求内容的类型，如 `application/xml` 告诉服务端接收 XML；

## 参考

1 [Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
2 [Understanding REST](https://spring.io/understanding/REST)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。