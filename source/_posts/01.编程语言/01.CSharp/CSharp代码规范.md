---
title: 'C#代码规范'
comments: true
tags:
  - 'C#'
categories:
  - 01.编程语言
  - 01.CSharp
date: 2018-05-25 18:06:26
---

## 1.	规范制定原则

- 方便代码的交流和维护。
- 不影响编码的效率，不与大众习惯冲突。
- 使代码更美观、阅读更方便。
- 使代码的逻辑更清晰、更易于理解。

## 2.	术语定义

### 2.1 Pascal 大小写

将标识符的首字母和后面连接的每个单词的首字母都大写。可以对三字符或更多字符的标识符使用Pascal 大小写。例如： BackColor。

### 2.2 Camel 大小写

标识符的首字母小写，而每个后面连接的单词的首字母都大写。例如：backColor。

## 3. 代码外观

### 3.1 列宽

控制在 120 字符左右。

### 3.2 换行

-	在逗号后换行。
-	在操作符前换行。
-	规则1优先于规则2。

### 3.3	缩进 

缩进应该是每行一个Tab(4个空格)，不要在代码中使用Tab字符。
`VS设置`：工具->选项->文本编辑器->C#->制表符->插入空格

### 3.4	空行

空行是为了将逻辑上相关联的代码分块，以便提高代码的可阅读性。

- 在以下情况下使用两个空行
  - 接口和类的定义之间。
  - 枚举和类的定义之间。
  - 类与类的定义之间.

- 在以下情况下使用一个空行
  - 方法与方法、属性与属性之间。
  - 方法中变量声明与语句之间。
  - 方法与方法之间。
  - 方法中不同的逻辑块之间。
  - 方法中的返回语句与其他的语句之间。
  - 属性与方法、属性与字段、方法与字段之间。
  - 注释与它注释的语句间不空行，但与其他的语句间空一行。

### 3.5 程序注释

#### 3.5.1 文件注释

```C#
//===========================================================
// Copyright (c) $年份 $公司名称.  
// 版权所有.
//===========================================================
```

#### 3.5.2 对象注释（类、接口、枚举、结构等）

```C#
/// <summary>
/// $功能描述
/// 作者：$作者
/// 日期：$创建日期
/// 版本：$版本号
/// </summary>
```

#### 3.5.3 其他注释（单行注释、多行注释、方法注释）

- 方法注释**必须**；
- 其他根据情况自行添加。

## 4. 命名规范

### 4.1 命名原则

- 使名称足够长以便有一定的意义，并且足够短以避免冗长。
- 唯一名称在编程上仅用于将各项区分开。
- 表现力强的名称是为了帮助人们阅读，提供人们可以理解的名称是有意义的。
- 请确保选择的名称符合适用语言的规则和标准。

### 4.2	命名空间

命名命名空间时的一般性规则是使用公司名称，后跟项目名称和可选的功能与设计。
`示例`：namespace CompanyName.ProjectName.ModuleName

### 4.3	类

-	使用 Pascal 大小写。
-	用名词或名词短语命名类。
-	使用全称避免缩写，除非缩写已是一种公认的约定，如URL、HTML。
-	不要使用类型前缀，如在类名称上对类使用 C 前缀。例如，使用类名称 FileStream，而不是 CFileStream。 

### 4.4	接口
 
-	用名词或名词短语，或者描述行为的形容词命名接口。例如，接口名称 IComponent 使用描述性名词。接口名称 ICustomAttributeProvider 使用名词短语。名称 IPersistable 使用形容词。 
-	使用 Pascal 大小写。 
-	少用缩写。 
-	给接口名称加上字母 I 前缀，以指示该类型为接口。在定义类/接口对（其中类是接口的标准实现）时使用相似的名称。两个名称的区别应该只是接口名称上有字母 I 前缀。
-	当类是接口的标准执行时，定义这一对类/接口组合就要使用相似的名称。两个名称的不同之处只是接口名前有一个I前缀。
         
### 4.5 属性 (Attribute)

- 将后缀 Attribute 添加到自定义属性类。
    
### 4.6	枚举 (Enum)

- 对于 Enum 类型和值名称使用 Pascal 大小写。 
- 少用缩写。 
- 不要在 Enum 类型名称上使用 Enum 后缀。

### 4.7	参数

- 使用描述性参数名称。参数名称应当具有足够的描述性，以便参数的名称及其类型可用于在大多数情况下确定它的含义。 
- 对参数名称使用 Camel 大小写。 
- 使用描述参数的含义的名称，而不要使用描述参数的类型的名称。开发工具将提供有关参数的类型的有意义的信息。因此， 通过描述意义，可以更好地使用参数的名称。少用基于类型的参数名称，仅在适合使用它们的地方使用它们。 
- 不要使用保留的参数。保留的参数是专用参数，如果需要，可以在未来的版本中公开它们。相反，如果在类库的未来版本中需要更多的数据，请为方法添加新的重载。 
- 不要给参数名称加匈牙利语类型表示法的前缀。 
  
### 4.8	方法

-	使用动词或动词短语命名方法。 
-	使用 Pascal 大小写。

### 4.9	属性 (property)

-	使用名词或名词短语命名属性。 
-	使用 Pascal 大小写。 
-	不要使用匈牙利语表示法。

### 4.10	常量 (const)

- 所有单词大写，多个单词之间用 "_" 隔开。
       
### 4.11 字段(Field)

-	private、protected 使用 Camel 大小写。
- public 使用 Pascal 大小写。
- 为了区分字段和局部变量，建议在首字母前加一下划线_。
`ps`：C# 中通常字段只有 private，若需暴露，请使用属性。