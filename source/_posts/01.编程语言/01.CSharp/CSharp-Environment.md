---
title: 多环境工作
comments: true
tags: ASP.NET Core
categories:
  - 01.编程语言
  - 01.CSharp
date: 2017-08-31 15:26:07
---

## 1.介绍

ASP.NET Core 通过多环境控制 APP 的行为，例如 development，staging 和 production。环境变量决定了运行环境，从而根据不同环境采用不同配置。

<!--more-->

## 2.ASPNETCORE_ENVIRONMENT 环境变量

- Development 开发环境
- Staging 预发布、部署上线前的最终测试环境、生产环境的物理镜像
- Production 生产环境（安全性、高性能、稳健性）
  - 开启缓存
  - 客户端资源 `bundled`，`minified` 或 `CDN`
  - 关闭 `diagnostic ErrorPages`
  - 开启 `friendly error pages`
  - 开启 `production logging` 和 `monitoring`
  - ...

## 3.注意事项

- Windows 不区分大小写，Linux 默认区分大小写。
- 设置：右键项目属性-调试-环境变量，另在 `~\Properties\launchSettings.json` 可看到具体配置。
  - launchSettings.json 存储的变量可访问到，不安全，禁止存放加密信息，使用 `Secret Manager` 存放加密信息。 
- 本机设置
  - 临时：`set ASPNETCORE_ENVIRONMENT=Development`
  - 永久：环境变量-ASPNETCORE_ENVIRONMENT=Development

## 参考文章

1 [多环境工作](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/environments)