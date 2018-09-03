---
title: Oracle级联更新
comments: true
tags: Oracle
categories:
  - 02.数据库
  - 03.Oracle
date: 2018-07-23 16:57:27
---

## 1. 介绍

Oracle本身是不支持外键的级联更新操作，需将外键设为延迟约束后，再通过触发器实现。

## 参考
1 [Oracle外键级联删除和级联更新](https://www.2cto.com/database/201507/417496.html)