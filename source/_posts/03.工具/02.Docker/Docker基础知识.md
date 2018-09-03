---
title: Docker基础知识
comments: true
tags:
  - Docker
categories:
  - 03.工具
  - 02.Docker
date: 2017-09-05 17:13:53
---

## 1. 介绍

Docker 使用 Google 公司推出的 Go 语言 进行开发实现，基于 Linux 内核的 cgroup，namespace，以及 AUFS 类的 Union FS 等技术，对进程进行封装隔离，属于 操作系统层面的虚拟化技术。由于隔离的进程独立于宿主和其它的隔离的进程，因此也称其为容器。

## 2. 基本概念

- 镜像（Image）
- 容器（Container）
- 仓库（Repository）