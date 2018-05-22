---
title: Markdown笔记
comments: true
date: 2017-08-31 15:01:02
tags: Markdown
categories: 工具
---
## 1.什么是Markdown

Markdown是一种在web显示带样式风格文本的方式。你能通过它控制文本的字体样式、插入图片、插入列表等。通常，Markdown使用一些特殊的非字母符号来作为语法规则，如`#`等。你能在Github上大部分地方使用Markdown。比如：

* [Gists](https://gist.github.com/)
* Issues的评论、Pull Requests
* .md或.markdown后缀名的文件

<!--more-->

## 2.规范

```
<span id="anchorTest">锚点测试</span>

1. 这是一个文本；
2. **粗体**；
3. *斜体*；
4. [我的Github](https://github.com/venux)
5. 列表
    * 无序列表1
    - 无序列表2
        - 无序列表21
        - 无序列表22
6. 图片![Image](https://avatars2.githubusercontent.com/u/7089227?v=3&s=460)
7. 引用

>Hello,World!-Coder

# H1
## H2
### H3
#### H4
##### H5
###### H6

I think you should use an `<addr>` element here instead.
```

## 3.Github特殊风格

### 语法高亮

```javascript
function Test(args){
    if(args){
        console.log(args);
    }	
}
```

```C#
public class Test
{
    static void Main()
    {
        Console.WriteLine("Hello,World!");		
    }
}
```

### 任务列表

- [x] 1. 已完成任务，支持列表，@mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [ ] 2. 未完成任务

### 表格

表头一|表头2
-----|-----
11|12
21|22

### SHA引用

5e0b770018f87bd7fafecb7b3920cda8a30d4740

### Issue引用

#1

### 圈人

@venux @CDLL

### 自动识别网址

http://www.cnblogs.com

### 删除线

~~删除~~

### Emoji

:+1:

### 锚点

[锚点测试](#anchorTest)
