---
title: SQLServer转Oracle
comments: true
tags:
  - SQL Server
  - Oracle
date: 2018-07-12 13:31:10
---

## 1. 情景

公司项目的新客户数据库为 Oracle，故需将项目的 SQL Server 库转换为 Oracle 库。

## 2. 工具

- SQL Server 自带的 bcm（注意：需将 SQL Server 安装目录下对应版本的 Tools\Binn 目录，如`C:\Program Files\Microsoft SQL Server\100\Tools\Binn` 添加到环境变量 Path 中）；
- [SQL Developer 17.2](http://download.oracle.com/otn/java/sqldeveloper/sqldeveloper-17.2.0.188.1159-no-jre.zip)(注意：需安装配置 Java 8)；

### 参考

- [Migrating a Microsoft SQL Server Database to Oracle Database 11g](http://www.oracle.com/webfolder/technetwork/tutorials/obe/db/hol08/sqldev_migration/mssqlserver/migrate_microsoft_sqlserver_otn.htm)
- [用 SQL Developer 3.2 将 SQL Server 2008 数据库离线迁移到 Oracle 11g](https://blog.csdn.net/rootcn/article/details/8894130)
- [Oracle和sqlserver数据类型对应](https://www.cnblogs.com/benbenfishfish/p/8675075.html)