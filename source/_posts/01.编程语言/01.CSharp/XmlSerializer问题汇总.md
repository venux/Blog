---
title: 'XmlSerializer问题汇总'
comments: true
tags:
  - 'C#'
  - '疑难杂症'
categories:
  - 01.编程语言
  - 01.CSharp
date: 2018-09-06 18:06:26
---

## 1. 字符串编码问题

问题描述：使用 StringWriter 进行 XML 序列化时，生成的 XML 编码为 UTF-16，需改为 UTF-8。
解决方案：
```C#
public sealed class Utf8StringWriter : StringWriter
{
    public override Encoding Encoding => Encoding.UTF8;
}
```
参考：
- [using-stringwriter-for-xml-serialization](https://stackoverflow.com/questions/1564718/using-stringwriter-for-xml-serialization)

## 2. null 不序列化问题

问题描述：部分属性值为 null，序列化成 XML 时，不生成相应的属性 XML。 
解决方案：
```C#
public sealed class Utf8StringWriter : StringWriter
{
    public override Encoding Encoding => Encoding.UTF8;
}
```
参考：
- [Suppress Null Value Types from Being Emitted by XmlSerializer](https://stackoverflow.com/questions/1296468/suppress-null-value-types-from-being-emitted-by-xmlserializer)