---
title: java-JSP
comments: true
tags:
  - Java
categories: Java
date: 2018-04-18 22:05:19
---
## 1 介绍

JSP（Java Server Pages），一种动态网页开发技术，类似于 ASP。通常以`<%`开头，以`%>`结尾。

<!--more-->
## 2 特点（与CGI对比）

- 性能更加优越，因为JSP可以直接在HTML网页中动态嵌入元素而不需要单独引用CGI文件。
- 服务器调用的是已经编译好的JSP文件，而不像CGI/Perl那样必须先载入解释器和目标脚本。
- JSP 基于Java Servlet API，因此，JSP拥有各种强大的企业级Java API，包括JDBC，JNDI，EJB，JAXP等等。
- JSP页面可以与处理业务逻辑的 Servlet 一起使用，这种模式被Java servlet 模板引擎所支持。

## 3 JSP 流程

![JSP 位置](/images/posts/jsp-arch.jpg)
![JSP 流程](/images/posts/jsp-processing.jpg)

- 浏览器发送一个 HTTP 请求给服务器。
- Web 服务器识别出这是一个对 JSP 网页的请求，并且将该请求传递给 JSP 引擎。通过使用 URL或者 .jsp 文件来完成。
- JSP 引擎从磁盘中载入 JSP 文件，然后将它们转化为 Servlet。这种转化只是简单地将所有模板文本改用 println() 语句，并且将所有的 JSP 元素转化成 Java 代码。
- JSP 引擎将 Servlet 编译成可执行类，并且将原始请求传递给 Servlet 引擎。
- Web 服务器的某组件将会调用 Servlet 引擎，然后载入并执行 Servlet 类。在执行过程中，Servlet 产生 HTML 格式的输出并将其内嵌于 HTTP response 中上交给 Web 服务器。
- Web 服务器以静态 HTML 网页的形式将 HTTP response 返回到您的浏览器中。
- Web 浏览器处理 HTTP response 中动态产生的HTML网页，就好像在处理静态网页一样。

## 4 JSP 生命周期

![JSP 生命周期](/images/posts/jsp_life_cycle.jpg)

- **编译阶段**：servlet容器编译servlet源文件，生成servlet类。若未修改，则跳过。
  - 解析JSP文件。
  - 将JSP文件转为servlet。
  - 编译servlet。
- **初始化阶段**：加载与JSP对应的servlet类，创建其实例，并调用它的初始化方法
```java
public void jspInit(){
  //JSP初始化代码
}
```
- **执行阶段**：调用与JSP对应的servlet实例的服务方法
```java
void _jspService(HttpServletRequest request,HttpServletResponse response){
  //服务端处理代码
}
```
- **销毁阶段**：调用与JSP对应的servlet实例的销毁方法，然后销毁servlet实例
```java
public void jspDestroy(){
  //清理代码
}
```

## 5 JSP 语法

### 5.1 脚本程序

可包含任意量的Java语句、变量、方法或表达式。格式：
```jsp
<% 代码片段 %>
```
或
```jsp
<jsp:scriptlet>
  代码片段
</jsp:scriptlet>
```

### 5.2 头部支持中文

```jsp
<%@ page language="java" contentType="text/html;charset=UTF-8" pageEncoding="UTF-8" %>
```

### 5.3 声明

一个声明语句可以声明一个或多个变量、方法，供后面的Java代码使用。
```jsp
<%! declaration;[ declaration;]+ ... %>
```
或
```jsp
<jsp:declaration>
  代码片段
</jsp:declaration>
```

### 5.4 表达式

一个JSP表达式中包含的脚本语言表达式，先被转化成String，然后插入到表达式出现的地方。
`注意：`不能以分号来结束。

```jsp
<%= 表达式 %>
```
或
```jsp
<jsp:expression>
   表达式
</jsp:expression>
```

### 5.5 注释

```jsp
<%--注释--%>
```

### 5.6 指令

设置与整个JSP页面相关的属性。

```jsp
<%@ directive attribute="value" %>
```
指令|描述
----|----
<%@ page ... %>|定义页面的依赖属性，比如脚本语言、error页面、缓存需求等等
<%@ include ... %>|包含其他文件
<%@ taglib ... %>|引入标签库的定义，可以是自定义标签

### 5.7 行为

使用XML语法结构来控制servlet引擎。它能够动态插入一个文件，重用JavaBean组件，引导用户去另一个页面，为Java插件产生相关的HTML等等。
行为标签只有一种语法格式，它严格遵守XML标准。

```jsp
<jsp:action_name attribute="value" />
```
语法|描述
----|----
jsp:include|用于在当前页面中包含静态或动态资源
jsp:useBean|寻找和初始化一个JavaBean组件
jsp:setProperty|设置 JavaBean组件的值
jsp:getProperty|将 JavaBean组件的值插入到 output中
jsp:forward|从一个JSP文件向另一个文件传递一个包含用户请求的request对象
jsp:plugin|用于在生成的HTML页面中包含Applet和JavaBean对象
jsp:element|动态创建一个XML元素
jsp:attribute|定义动态创建的XML元素的属性
jsp:body|定义动态创建的XML元素的主体
jsp:text|用于封装模板数据

### 5.8 隐含对象

对象|描述
----|----
request|HttpServletRequest类的实例
response|HttpServletResponse类的实例
out|PrintWriter类的实例，用于把结果输出至网页上
session|HttpSession类的实例
application|ServletContext类的实例，与应用上下文有关
config|ServletConfig类的实例
pageContext|PageContext类的实例，提供对JSP页面所有对象以及命名空间的访问
page|类似于Java类中的this关键字
Exception|Exception类的对象，代表发生错误的JSP页面中对应的异常对象

### 5.9 控制流语句

#### 5.9.1 判断语句

```jsp

<% if(flag){ %>
  <p>True</p>
<% }else{ %>
  <p>False</p>
<% } %>
```

#### 5.9.2 循环语句

```jsp
<% for ( index = 1; index <= 3; index++){ %>
  <p>
    <%= index %> 
  </p>
<% } %>
```

### 5.10 运算符

JSP支持所有Java逻辑和算术运算符。

### 5.11 字面量

- 布尔值(boolean)：true 和 false;
- 整型(int)：与 Java 中的一样;
- 浮点型(float)：与 Java 中的一样;
- 字符串(string)：以单引号或双引号开始和结束;
- Null：null。

## 参考

1 [博客](http://www.venux.cn)

## 注意

本文主要用于记录个人笔记，方便查看不明了之处，故可能摘抄许多文章，如有冒犯，请联系我删除。另由于个人查看，故可能忽略许多知识点，请自行查看相关资料，谢谢。