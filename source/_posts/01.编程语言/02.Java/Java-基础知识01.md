---
title: Java基础知识01
comments: true
tags:
  - Java
  - JavaSE
categories:
  - 01.编程语言
  - 02.Java
date: 2018-03-25 22:41:06
---
## 1 Hello World 示例

```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
```
`ps:`
 - Java 中类名（CamelCase 风格）要与文件名保持一致；
 - Java 中方法名 camelCase 风格；
 - main 主函数参数默认为 String []；

<!--more-->

## 2 Java 标识符

- 所有的标识符都应该以字母（A-Z或者a-z）,美元符（$）、或者下划线（_）开始

## 3 Java 变量

- 局部变量
- 类变量（静态变量）
- 成员变量（非静态变量）

## 4 Java 关键字

关键字|描述
-----|-----
abstract|抽象方法，抽象类的修饰符
assert|断言条件是否满足
boolean|布尔数据类型
break|跳出循环或者label代码段
byte|8-bit 有符号数据类型
case|switch语句的一个条件
catch|try搭配捕捉异常信息
char|16-bit Unicode字符数据类型
class|定义类
const|未使用
continue|不执行循环体剩余部分
default|switch语句中的默认分支
do|循环语句，循环体至少会执行一次
double|64-bit双精度浮点数
else|if条件不成立时执行的分支
enum|枚举类型
extends|表示一个类是另一个类的子类
final|表示一个值在初始化之后就不能再改变了或表示方法不能被重写，或者一个类不能有子类
finally|为了完成执行的代码而设计的，主要是为了程序的健壮性和完整性，无论有没有异常发生都执行代码。
float|32-bit单精度浮点数
for|for循环语句
goto|未使用
if|条件语句
implements|表示一个类实现了接口
import|导入类
**instanceof**|测试一个对象是否是某个类的实例
int|32位整型数
interface|接口，一种抽象的类型，仅有方法和常量的定义
long|64位整型数
**native**|表示方法用非java代码实现
new|分配新的类实例
package|一系列相关类组成一个包
private|表示私有字段，或者方法等，只能从类内部访问
protected|表示字段只能通过类或者其子类访问子类或者在同一个包内的其他类
public|表示共有属性或者方法
return|方法返回值
short|16位数字
static|表示在类级别定义，所有实例共享的
**strictfp**|浮点数比较使用严格的规则
super|表示基类
switch|选择语句
**synchronized**|表示同一时间只能由一个线程访问的代码块
this|表示调用当前实例或者调用另一个构造函数
throw|抛出异常
**throws**|定义方法可能抛出的异常
**transient**|修饰不要序列化的字段
try|表示代码块要做异常处理或者和finally配合表示是否抛出异常都执行finally中的代码
void|标记方法不返回任何值
**volatile**|标记字段可能会被多个线程同时访问，而不做同步
while|while循环

## 5 类&对象

- 对象：对象是类的一个实例，有状态和行为。
- 类：类是一个模板，它描述一类对象的行为和状态。
- 局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。
- 成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。
- 类变量：类变量也声明在类中，方法体之外，但必须声明为static类型。

## 6 源文件

- 一个源文件中只能有一个 public 类
- 一个源文件可以有多个非 public 类
- 源文件的名称应该和 public 类的类名保持一致
- 如果一个类定义在某个包中，那么 package 语句应该在源文件的首行。
- 如果源文件包含 import 语句，那么应该放在 package 语句和类定义之间。如果没有 package 语句，那么 import 语句应该在源文件中最前面。
- import 语句和 package 语句对源文件中定义的所有类都有效。

## 7 基本数据类型

八种基本类型：六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。
*PS:*字符串不属于基本类型。

### 7.1 byte（java.lang.Byte）

- byte数据类型是8位、有符号的，以二进制补码表示的整数；
- 最小值是-128（-2^7）；
- 最大值是127（2^7-1）；
- 默认值是0；
- byte类型用在大型数组中节约空间，主要代替整数，因为byte变量占用的空间只有int类型的四分之一；

### 7.2 short（java.lang.Short）

- short数据类型是16位、有符号的以二进制补码表示的整数
- 最小值是-32768（-2^15）；
- 最大值是32767（2^15 - 1）；
- Short数据类型也可以像byte那样节省空间。一个short变量是int型变量所占空间的二分之一；
- 默认值是0；

### 7.3 int（java.lang.Integer）

- int数据类型是32位、有符号的以二进制补码表示的整数；
- 最小值是-2,147,483,648（-2^31）；
- 最大值是2,147,483,647（2^31 - 1）；
- 一般地整型变量默认为int类型；
- 默认值是0；

### 7.4 long（java.lang.Long）

- long数据类型是64位、有符号的以二进制补码表示的整数；
- 最小值是-9,223,372,036,854,775,808（-2^63）；
- 最大值是9,223,372,036,854,775,807（2^63 -1）；
- 这种类型主要使用在需要比较大整数的系统上；
- 默认值是0L；

### 7.5 float（java.lang.Float）

- float数据类型是单精度、32位、符合IEEE 754标准的浮点数；
- float在储存大型浮点数组的时候可节省内存空间；
- 默认值是0.0f；
- **浮点数不能用来表示精确的值**，如货币；

### 7.6 double（java.lang.Double）

- double数据类型是双精度、64位、符合IEEE 754标准的浮点数；
- 浮点数的默认类型为double类型；
- **double类型同样不能表示精确的值**，如货币；

### 7.7 boolean

- boolean数据类型表示一位的信息；
- 只有两个取值：true和false；
- 这种类型只作为一种标志来记录true/false情况；
- 默认值是false；

### 7.8 char（java.lang.Character）

- char类型是一个单一的16位Unicode字符；
- 最小值是’\u0000’（即为0）；
- 最大值是’\uffff’（即为65,535）；
- char数据类型可以储存任何字符；

### 7.9 void（java.lang.Void）

实际上，JAVA中还存在另外一种基本类型void，它也有对应的包装类 java.lang.Void，不过我们无法直接对它们进行操作。

## 8 引用类型

- 引用类型变量由类的构造函数创建，可以使用它们访问所引用的对象。这些变量在声明时被指定为一个特定的类型。变量一旦声明后，类型就不能被改变了。
- 对象、**数组**、**字符串**都是引用数据类型。
- 所有引用类型的默认值都是null。
- 一个引用变量可以用来引用与任何与之兼容的类型。

## 9 常量（final）

- 常量就是一个固定值。
- 通常使用大写字母表示常量。
- **字符串**是常量。

## 10 局部变量

- 局部变量声明在方法、构造方法或者语句块中；
- 局部变量是在栈上分配的。
- 局部变量没有默认值，所以**局部变量被声明后，必须经过初始化，才可以使用**。

## 11 实例变量

- 实例变量声明在一个类中，但在方法、构造方法和语句块之外；
- 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；

## 12 类变量（静态变量）

- 类变量也称为静态变量，在类中以static关键字声明，但必须在方法、构造方法和语句块之外。
- 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
- 静态变量除了被声明为常量外很少使用。**常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。**
- **静态变量储存在静态存储区**。经常被声明为常量，很少单独使用static声明变量。
- **静态变量在程序开始时创建，在程序结束时销毁**。
- 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
- 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以- 在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
- 静态变量可以通过：ClassName.VariableName的方式访问。
- **类变量被声明为public static final类型时，类变量名称必须使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。**

## 13 访问控制修饰符

- default：默认的，在同一包内可见，不使用任何修饰符。
  - 接口里的变量都隐式声明为public static final,而接口里的方法默认情况下访问权限为public。
- private：私有的，在同一类内可见。
- public：共有的，对所有类可见。
- protected 受保护的，对**同一包内的类和所有子类**可见（**注意**：此处对应C#的protected internal，而C#中protected仅仅对所有程序集的子类可见，而对包内的类不可见）。
  - Protected访问修饰符不能修饰类和接口，方法和成员变量能够声明为protected，但是接口的成员变量和成员方法不能声明为protected。

## 14 访问控制和继承

- 父类中声明为public的方法在子类中也必须为public。
- 父类中声明为protected的方法在子类中要么声明为protected，要么声明为public。不能声明为private。
- 父类中声明为private的方法，不能够被继承。

## 15 非访问修饰符

- static
  - 用来创建类方法和类变量。
- final
  - 用来修饰类、方法和变量，**final修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的**。
  - final变量能被显式地初始化并且只能初始化一次。**被声明为final的对象的引用不能指向不同的对象。但是final对象里的数据可以被改变。**也就是说final对象的引用不能改变，但是里面的值可以改变。
  - final修饰符通常和static修饰符一起使用来创建类常量。
  - 类中的Final方法可以被子类继承，但是不能被子类修改。声明final方法的主要目的是防止该方法的内容被修改。
  - final类不能被继承，没有类能够继承final类的任何特性。（即C#的sealed）
- abstract
  - 用来创建抽象类和抽象方法。
  - 一个类不能同时被abstract和final修饰。
  - 抽象类可以包含抽象方法和非抽象方法。
  - 抽象方法不能被声明成final和static。任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。
- synchronized
  - synchronized关键字声明的方法同一时间只能被一个线程访问。synchronized修饰符可以应用于四个访问修饰符。
- Transient
  - 序列化的对象包含被transient修饰的实例变量时，java虚拟机(JVM)跳过该特定的变量。该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。
- volatile
  - volatile修饰的成员变量在每次被线程访问时，都强迫从共享内存中重读该成员变量的值。而且，当成员变量发生变化时，强迫线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。一个volatile对象引用可能是null。

## 16 位运算符

操作符|描述
----|----
**&**|按位与操作符，当且仅当两个操作数的某一位都非0时候结果的该位才为1。
**&#124;**|按位或操作符，只要两个操作数的某一位有一个非0时候结果的该位就为1。
**^**|按位异或操作符，两个操作数的某一位不相同时候结果的该位就为1。	
**〜**|按位补运算符翻转操作数的每一位。	
**<<**|按位左移运算符。左操作数按位左移右操作数指定的位数。
**>>**|按位右移运算符。左操作数按位右移右操作数指定的位数。
**>>>**|按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。

## 17 instanceOf 

该运算符用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）。
```java
String name = 'James';
boolean result = name instanceOf String; // 由于name是Strine类型，所以返回true
```

## 18 for增强（即C#的foreach）

`·`要用于数组(Java5，之后不清楚是否有扩展，待确认)`

```java
int [] numbers = {10, 20, 30, 40, 50};

for(int x : numbers ){
  System.out.print( x );
  System.out.print(",");
}
```

## 19 switch

- switch语句中的变量类型只能为byte、short、int或者char。`(不清楚后续版本是否有扩展，待确认)`
- case语句中的值的数据类型必须与变量的数据类型相同，而且只能是常量或者字面常量。
- switch语句可以包含一个default分支，**该分支必须是switch语句的最后一个分支**（C#中不一定是最后一个）。

## 20 Number类（java.lang）

![图一](/images/posts/Java_Number.jpg)

## 21 String类

- **字符串属于对象**
- **和C#不同的是，Java中只有String，而没有string！！！**
- **String类是不可改变的，所以你一旦创建了String对象，那它的值就无法改变了。**
- **字符串长度使用length(),即方法而不是C#的属性length。**

## 22 StringBuffer和StringBuilder

- StringBuilder的方法不是线程安全的（不能同步访问）,而StringBuffer是。
- StringBuilder相较于StringBuffer有速度优势，多数情况下建议使用StringBuilder类。
- 在应用程序要求线程安全的情况下，则必须使用StringBuffer类。

## 23 数组

### 23.1 数组

![图一](/images/posts/Java_Array.jpg)

### 23.2 Arrays 类(java.util.Arrays)

- 所有方法都是静态的
- 给数组赋值：通过fill方法。
- 对数组排序：通过sort方法,按升序。
- 比较数组：通过equals方法比较数组中**元素值**是否相等。
- 查找数组元素：通过binarySearch方法能对排序好的数组进行二分查找法操作

## 24 时间

### 24.1 Date 类(java.util.Date)

System.currentTimeMillis()计算时间

### 24.2 SimpleDateFormat：格式化日期

字母|描述|示例
----|----|----
G|纪元标记|AD
y|四位年份|2001
M|月份|July or 07
d|一个月的日期|10
h|A.M./P.M.(1~12)格式小时|12
H|一天中的小时(0~23)|22
m|分钟数|30
s|秒数|55
S|微妙数|234
E|星期几|Tuesday
D|一年中的日子|360
F|一个月中第几周的周几|2 (second Wed. in July)
w|一年中第几周|40
W|一个月中第几周|1
a|A.M./P.M. 标记|PM
k|一天中的小时(1~24)|24
K|A.M./P.M. (0~11)格式小时|10
z|时区|Eastern Standard Time
'|文字定界符|Delimiter
"|单引号|`

### 24.3 Calendar

- 抽象类
- getInstance()获取实例


常量|描述
----|----
Calendar.YEAR|年份
Calendar.MONTH|月份
Calendar.DATE|日期
Calendar.DAY_OF_MONTH|日期，和上面的字段意义完全相同
Calendar.HOUR|12小时制的小时
Calendar.HOUR_OF_DAY|24小时制的小时
Calendar.MINUTE|分钟
Calendar.SECOND|秒
Calendar.DAY_OF_WEEK|星期几

### 24.4 GregorianCalendar

## 25 正则（java.util.regex包）

- Pattern类：pattern对象是一个正则表达式的编译表示。Pattern类没有公共构造方法。要创建一个Pattern对象，你必须首先调用其公共静态编译方法，它返回一个Pattern对象。该方法接受一个正则表达式作为它的第一个参数。
- Matcher类：Matcher对象是对输入字符串进行解释和匹配操作的引擎。与Pattern类一样，Matcher也没有公共构造方法。你需要调用Pattern对象的matcher方法来获得一个Matcher对象。
- PatternSyntaxException：PatternSyntaxException是一个非强制异常类，它表示一个正则表达式模式中的语法错误。

字符|说明
----|----
\|`将下一字符标记为特殊字符、文本、反向引用或八进制转义符。例如，"n"匹配字符"n"。"\n"匹配换行符。序列"\\"匹配"\"，"\("匹配"("。`
^|`匹配输入字符串开始的位置。如果设置了 RegExp 对象的 Multiline 属性，^ 还会与"\n"或"\r"之后的位置匹配。`
$|`匹配输入字符串结尾的位置。如果设置了 RegExp 对象的 Multiline 属性，$ 还会与"\n"或"\r"之前的位置匹配。`
*|`零次或多次匹配前面的字符或子表达式。例如，zo* 匹配"z"和"zoo"。* 等效于 {0,}。`
+|`一次或多次匹配前面的字符或子表达式。例如，"zo+"与"zo"和"zoo"匹配，但与"z"不匹配。+ 等效于 {1,}。`
?|`零次或一次匹配前面的字符或子表达式。例如，"do(es)?"匹配"do"或"does"中的"do"。? 等效于 {0,1}。`
{n}|`n 是非负整数。正好匹配 n 次。例如，"o{2}"与"Bob"中的"o"不匹配，但与"food"中的两个"o"匹配。`
{n,}|`n 是非负整数。至少匹配 n 次。例如，"o{2,}"不匹配"Bob"中的"o"，而匹配"foooood"中的所有 o。"o{1,}"等效于"o+"。"o{0,}"等效于"o*"。`
{n,m}|`M 和 n 是非负整数，其中 n <= m。匹配至少 n 次，至多 m 次。例如，"o{1,3}"匹配"fooooood"中的头三个 o。'o{0,1}' 等效于 'o?'。注意：您不能将空格插入逗号和数字之间。`
?|`当此字符紧随任何其他限定符（*、+、?、{n}、{n,}、{n,m}）之后时，匹配模式是"非贪心的"。"非贪心的"模式匹配搜索到的、尽可能短的字符串，而默认的"贪心的"模式匹配搜索到的、尽可能长的字符串。例如，在字符串"oooo"中，"o+?"只匹配单个"o"，而"o+"匹配所有"o"。`
.|`匹配除"\r\n"之外的任何单个字符。若要匹配包括"\r\n"在内的任意字符，请使用诸如"[\s\S]"之类的模式。`
(pattern)|`匹配 pattern 并捕获该匹配的子表达式。可以使用 $0…$9 属性从结果"匹配"集合中检索捕获的匹配。若要匹配括号字符 ( )，请使用"\("或者"\)"。`
(?:pattern)|`匹配 pattern 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配。这对于用"or"字符 (&#124;) 组合模式部件的情况很有用。例如，'industr(?:y&#124;ies) 是比 'industry&#124;industries' 更经济的表达式。`
(?=pattern)|`执行正向预测先行搜索的子表达式，该表达式匹配处于匹配 pattern 的字符串的起始点的字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?=95&#124;98&#124;NT&#124;2000)' 匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。`
(?!pattern)|`执行反向预测先行搜索的子表达式，该表达式匹配不处于匹配 pattern 的字符串的起始点的搜索字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?!95&#124;98&#124;NT&#124;2000)' 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。`
x&#124;y|`匹配 x 或 y。例如，'z&#124;food' 匹配"z"或"food"。'(z&#124;f)ood' 匹配"zood"或"food"。`
[xyz]|`字符集。匹配包含的任一字符。例如，"[abc]"匹配"plain"中的"a"。`
[^xyz]|`反向字符集。匹配未包含的任何字符。例如，"[^abc]"匹配"plain"中"p"，"l"，"i"，"n"。`
[a-z]|`字符范围。匹配指定范围内的任何字符。例如，"[a-z]"匹配"a"到"z"范围内的任何小写字母。`
[^a-z]|`反向范围字符。匹配不在指定的范围内的任何字符。例如，"[^a-z]"匹配任何不在"a"到"z"范围内的任何字符。`
\b|`匹配一个字边界，即字与空格间的位置。例如，"er\b"匹配"never"中的"er"，但不匹配"verb"中的"er"。`
\B|`非字边界匹配。"er\B"匹配"verb"中的"er"，但不匹配"never"中的"er"。`
\cx|`匹配 x 指示的控制字符。例如，\cM 匹配 Control-M 或回车符。x 的值必须在 A-Z 或 a-z 之间。如果不是这样，则假定 c 就是"c"字符本身。`
\d|`数字字符匹配。等效于 [0-9]。`
\D|`非数字字符匹配。等效于 [^0-9]。`
\f|`换页符匹配。等效于 \x0c 和 \cL。`
\n|`换行符匹配。等效于 \x0a 和 \cJ。`
\r|`匹配一个回车符。等效于 \x0d 和 \cM。`
\s|`匹配任何空白字符，包括空格、制表符、换页符等。与 [ \f\n\r\t\v] 等效。`
\S|`匹配任何非空白字符。与 [^ \f\n\r\t\v] 等效。`
\t|`制表符匹配。与 \x09 和 \cI 等效。`
\v|`垂直制表符匹配。与 \x0b 和 \cK 等效。`
\w|`匹配任何字类字符，包括下划线。与"[A-Za-z0-9_]"等效。`
\W|`与任何非单词字符匹配。与"[^A-Za-z0-9_]"等效。`
\xn|`匹配 n，此处的 n 是一个十六进制转义码。十六进制转义码必须正好是两位数长。例如，"\x41"匹配"A"。"\x041"与"\x04"&"1"等效。允许在正则表达式中使用 ASCII 代码。`
\num|`匹配 num，此处的 num 是一个正整数。到捕获匹配的反向引用。例如，"(.)\1"匹配两个连续的相同字符。`
\n|`标识一个八进制转义码或反向引用。如果 \n 前面至少有 n 个捕获子表达式，那么 n 是反向引用。否则，如果 n 是八进制数 (0-7)，那么 n 是八进制转义码。`
\nm|`标识一个八进制转义码或反向引用。如果 \nm 前面至少有 nm 个捕获子表达式，那么 nm 是反向引用。如果 \nm 前面至少有 n 个捕获，则 n 是反向引用，后面跟有字符 m。如果两种前面的情况都不存在，则 \nm 匹配八进制值 nm，其中 n 和 m 是八进制数字 (0-7)。`
\nml|`当 n 是八进制数 (0-3)，m 和 l 是八进制数 (0-7) 时，匹配八进制转义码 nml。`
\un|`匹配 n，其中 n 是以四位十六进制数表示的 Unicode 字符。例如，\u00A9 匹配版权符号 (©)。`

## 26 方法

- **方法是通过值传递参数**

```java
public class TestPassByValue {
   public static void main(String[] args) {
      int num1 = 1;
      int num2 = 2;

      System.out.println("Before swap method, num1 is " + num1 + " and num2 is " + num2);

      // 调用swap方法
      swap(num1, num2);
      System.out.println("After swap method, num1 is " + num1 + " and num2 is " + num2);
   }
   /** 交换两个变量的方法 */
   public static void swap(int n1, int n2) {
      System.out.println("\tInside the swap method");
      System.out.println("\t\tBefore swapping n1 is " + n1 + " n2 is " + n2);
      // 交换 n1 与 n2的值
      int temp = n1;
      n1 = n2;
      n2 = temp;

      System.out.println("\t\tAfter swapping n1 is " + n1 + " n2 is " + n2);
   }
}
```
*结果如下：*
```
Before swap method, num1 is 1 and num2 is 2
Inside the swap method
Before swapping n1 is 1 n2 is 2
After swapping n1 is 2 n2 is 1
After swap method, num1 is 1 and num2 is 2
```

## 27 可变参数

typeName... parameterName，必须放置在最后一个（即C#的param int arr）

## 28 finalize方法（即C#的析构函数）

- 在对象被垃圾收集器析构(回收)之前调用，它用来清除回收对象。
- System.gc(); //调用Java垃圾收集器

## 29 流（java.io包）

![Stream](/images/posts/Java_Stream.jpg)

### 29.1 读取控制台输入

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```

### 29.2 获取或设置JVM当前工作目录

```java
System.getProperty("user.dir");
System.setProperty("user.dir", "C:\\myDir");
```

### 29.3 文件分隔符

常量**File.separator**，用于解决Windows在路径名中使用反斜杠（\）作为名称分隔符，而UNIX使用正斜杠（/）的问题。

## 30 Scan(java.util.SCanner)

主要用于获取用户的输入。
```java
Scanner s = new Scanner(System.in); 
```

## 31 异常

### 31.1 异常类型

- 检查性异常：最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- 运行时异常： 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- 错误： 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

### 31.2 异常层次

- 所有的异常类是从java.lang.Exception类继承的子类。
- Exception类是Throwable类的子类。除了Exception类外，Throwable还有一个子类Error 。

![Exception](/images/posts/Java_Exception.jpg)

### 31.3 非检查性异常

异常|描述
----|----
ArithmeticException|当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。
ArrayIndexOutOfBoundsException|用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。
ArrayStoreException|试图将错误类型的对象存储到一个对象数组时抛出的异常。
ClassCastException|当试图将对象强制转换为不是实例的子类时，抛出该异常。
IllegalArgumentException|抛出的异常表明向方法传递了一个不合法或不正确的参数。
IllegalMonitorStateException|抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。
IllegalStateException|在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。
IllegalThreadStateException|线程没有处于请求操作所要求的适当状态时抛出的异常。
IndexOutOfBoundsException|指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。
NegativeArraySizeException|如果应用程序试图创建大小为负的数组，则抛出该异常。
NullPointerException|当应用程序试图在需要对象的地方使用 null 时，抛出该异常
NumberFormatException|当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。
SecurityException|由安全管理器抛出的异常，指示存在安全侵犯。
StringIndexOutOfBoundsException|此异常由 String 方法抛出，指示索引或者为负，或者超出字符串的大小。
UnsupportedOperationException|当不支持请求的操作时，抛出该异常。

### 31.4 检查性异常类

异常|描述
----|----
ClassNotFoundException|应用程序试图加载类时，找不到相应的类，抛出该异常。
CloneNotSupportedException|当调用 Object 类中的 clone 方法克隆对象，但该对象的类无法实现 Cloneable 接口时，抛出该异常。
IllegalAccessException|拒绝访问一个类的时候，抛出该异常。
InstantiationException|当试图使用 Class 类中的 newInstance 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。
InterruptedException|一个线程被另一个线程中断，抛出该异常。
NoSuchFieldException|请求的变量不存在
NoSuchMethodException|请求的方法不存在

### 31.5 throws/throw关键字

```java
import java.io.*;
public class className
{
   public void deposit(double amount) throws RemoteException
   {
      // Method implementation
      throw new RemoteException();
   }
   //Remainder of class definition
}
```

### 31.6 自定义异常

- 所有异常都必须是Throwable的子类。
- 检查性异常：继承Exception类。
- 运行时异常：继承RuntimeException 类。

### 31.7 异常和错误

- JVM(Java虚拟机)异常：由JVM抛出的异常或错误。例如：NullPointerException类，ArrayIndexOutOfBoundsException类，ClassCastException类。
- 程序级异常：由程序或者API程序抛出的异常。例如IllegalArgumentException类，IllegalStateException类。

## 38 继承(is-a)

可用`a instanceof b`校验。 

- extends：继承类
- implements：继承接口

## 39 重写（override）&重载（overload）

区别点|重载|重写
----|----|----
参数列表|必须修改|一定不能修改
返回类型|可以修改|一定不能修改
异常|可以修改|可以减少或删除，一定不能抛出新的或者更广的异常
访问|可以修改|一定不能做更严格的限制（可以降低限制）

## 40 多态（is-a）

- 同一个行为具有多个不同表现形式或形态的能力。
- 多态性是对象多种表现形式的体现。

## 41 接口（interface）

- 接口是隐式抽象的，当声明一个接口的时候，不必使用abstract关键字。
- 接口中每一个方法也是隐式抽象的，声明时同样不需要abstract关键子。
- 接口中的方法都是公有的。
- 标识接口：没有任何方法和属性的接口.它仅仅表明它的类属于一个特定的类型,供其他代码来测试允许做一些事情。

## 42 包

### 42.1 package

- 包声明应该在源文件的第一行，每个源文件只能有一个包声明，这个文件中的每个类型都应用于它。
- 如果一个源文件中没有使用包声明，那么其中的类，函数，枚举，注释等将被放在一个无名的包（unnamed package）中。

### 42.2 import

- 文件中可以包含任意数量的import声明。import声明必须在包声明之后，类声明之前。
- 静态导入
```java
import static java.lang.Math.*;
import static java.lang.System.out;
```

### 42.3 CLASSPATH

类目录的绝对路径叫做class path。设置在系统变量CLASSPATH中。编译器和java虚拟机通过将package名字加到class path后来构造.class文件的路径。<path- two>\classes是class path，package名字是com.apple.computers,而编译器和JVM会在 <path-two>\classes\com\apple\compters中找.class文件。
一个class path可能会包含好几个路径。多路径应该用分隔符分开。默认情况下，编译器和JVM查找当前目录。JAR文件按包含Java平台相关的类，所以他们的目录默认放在了class path中。

## 43 Object

名称|含义
----|----
public String toString()|它是实现在Object类中，我们可以自定义它。它返回对象的字符串表示形式。通常，它用于调试目的。
public boolean equals(Object obj)|它在Object类中实现，我们可以自定义它。它用于比较两个对象的相等性。
public int hashCode()|它在Object类中实现，我们可以自定义它。它返回对象的哈希码（整数）值。
protected Object clone() throws CloneNotSupportedException|它不在Object类中实现，我们可以通过覆盖克隆方法来自定义它。它用于创建对象的副本。
protected void finalize() throws Throwable|它不是在Object类中实现，我们可以自定义它。它在对象被销毁之前被垃圾收集器调用。
public final Class getClass()|它在Object类中实现，我们不能自定义它。它返回对对象的Class对象的引用。
public final void notify()|它是在Object类中实现的，我们不能自定义它。此方法通知对象的等待队列中的一个线程。
public final void notifyAll()|它是在Object类中实现的，我们不能自定义它。此方法通知对象的等待队列中的所有线程。
public final void wait() throws InterruptedException<br/>public final void wait(long timeout) throws InterruptedException<br/>public final void wait (long timeout, int nanos) throws InterruptedException|它是在Object类中实现的，我们不能自定义它。使对象的等待队列中的线程等待，无论是否超时。

### 43.1 hashCode

- 如果两个对象使用equals()方法相等，则它们必须具有相同的哈希码。
- 如果x.hashCode()等于y.hashCode()，则x.equals(y)不必返回true。
- **快速实现 hashCode方法**：读取 equals() 使用的所有字段的 hash 码，然后对它们进行按位异或（^）操作。

### 43.2 equals

这里是equals()方法的实现的规范。假设x，y和z是三个对象的非空引用。
- 自反性。表达式x.equals(x)应该返回true。
- 对称性。如果x.equals(y)返回true，y.equals(x)必须返回true。
- 传递性。如果x.equals(y)返回true，y.equals(z)返回true，则x.equals(z)必须返回true。
- 一致性。如果x.equals(y)返回true，它应该保持返回true，直到x或y的状态被修改。如果x.equals(y)返回false，它应该保持返回false，直到x或y的状态被修改。
- 与空引用的比较：任何类的对象不应等于空引用。表达式x.equals(null)应始终返回false。
- 与hashCode()方法的关系：如果x.equals(y)返回true，x.hashCode()必须返回与y.hashCode()相同的值。

### 43.3 toString

当需要对象的字符串表示时，Java会自动调用toString()方法。
```java
String str = "Hello" + new Point(10, 20);
```
等同于
```java
String str = "Hello" + new Point(10, 20).toString();
```

### 43.4 clone（浅拷贝）

Java不提供克隆(复制)对象的自动机制。克隆对象意味着逐位复制对象的内容。要支持克隆操作，请在类中实现clone()方法。
```java
public Object clone() {
  MyClass copy = null;
  try {
    copy = (MyClass) super.clone();
  } catch (CloneNotSupportedException e) {
    e.printStackTrace();
  }
  return copy;
}
```

### 43.5 finalize

finalize()方法将在类的对象销毁之前由垃圾回收器调用。

### Immutables(不可变)

在创建状态后无法更改其状态的对象称为不可变对象。一个对象不可变的类称为不可变类。不变的对象可以由程序的不同区域共享而不用担心其状态改变。不可变对象本质上是线程安全的。
```java
public  class  IntWrapper {
    private  final  int  value;

    public IntWrapper(int value) {
        this.value = value;
    }
    public int  getValue() {
        return value;
    }
}
```

### 43.7 Objects类(实用程序类)

主要用于处理对象。由静态方法组成。 Objects类中的大多数方法都会优雅地处理空值。

方法|描述
----|----
int compare(T a, T b, Comparator c)|如果参数相同，则返回0，否则返回c.compare(a，b)。因此，如果两个参数都为null，则返回0。
boolean deepEquals(Object a, Object b)|检查两个对象是否相等。如果两个参数都相等，则返回true。否则，它返回false。如果两个参数都为null，则返回true。
boolean equals(Object a, Object b)|比较两个对象是否相等。如果两个参数相等，则返回true。否则，它返回false。如果两个参数都为null，则返回true。
int hash(Object... values)|为所有指定的对象生成哈希码。它可以用于计算对象的哈希码，该哈希码基于多个实例字段。
int hashCode(Object o)|返回指定对象的哈希码值。如果参数为null，则返回0。
boolean isNull(Object obj)|如果指定的对象为null，isNull()方法返回true。否则，它返回false。您还可以使用比较运算符==检查对象是否为null，例如，obj == null返回obj的true为null。
boolean nonNull(Object obj)|执行与isNull()方法相反的检查。
T requireNonNull(T obj)|检查参数是否为null。如果参数为null，它会抛出一个NullPointerException异常。此方法设计用于验证方法和构造函数的参数。
T requireNonNull(T obj, String message)|第二个版本可以指定当参数为null时抛出的NullPointerException的消息。
T requireNonNull(T obj, Supplier messageSupplier)|第三个版本的方法将一个Supplier作为第二个参数。
String toString(Object o)<br/>String toString(Object o, String nullDefault)|如果参数为null，则toString()方法返回一个“null”字符串。对于非空参数，它返回通过调用参数的toString()方法返回的值。

## 注意

本文主要用于记录个人不明了之处，故可能忽略许多知识点，如有需要，请自行查找相关资料，谢谢。