---
title: Java 语言基础02
date: 2018-07-29 13:36:31
categories: Java
---

# 数据类型

## 1.基本数据类型

> Java 是一种强类型语言（每一个变量必须声明一种类型）。在Java中，一共有8种数据类型，其中有4种整型、2种浮点型、1种用于表示Unicode编码的字符单元的字符类型char和一种表示真值的boolean类型。

### 1.1.整型（表示没有小数部分的数值，允许为负数）

![image](https://wx2.sinaimg.cn/large/80ceacb8ly1ftqok9zd9bj20ng047t9t.jpg)

- int 最常用
- long 类型，数值后有一个**后缀L**，用于表示比如星球上的居住人数。
- byte 和 short 类型用于特定场合。比如，底层的文件处理或者需要控制占用存储空间量的大数组。

---

### 1.2.浮点类型（表示有小数部分的数值）

![image](https://wx2.sinaimg.cn/large/80ceacb8ly1ftqoqxm1bgj20mx02owff.jpg)

- double 表示这种类型的数值精度是 float 类型的两倍（双精度数值），绝大部分应用程序采用这种数据类型。

- float类型（单精度数值），数值后有一个**后缀F**，在很多情况下，精度难以满足，所以有很少的情况适合使用float类型。

  **注:**没有后缀 F 的默认为 double 类型。

---

### 1.3.char 类型（表示单个字符，通常用来表示字符常量，用单引号' '括起来）


### 1.4.boolean 类型

- boolean 类型有两个值：false 和 true，用来判断逻辑条件。整型值和布尔值之间不能转换。

---

## 2.字符串（String）

> Java 字符串就是Unicode 字符序列。Java 没有内置的字符串类型，而是预先定义了一个类String，每个**用双引号括起来的字符串**都是String类的一个实例。

### 2.1.子串

- String 类的 substring 方法可以从一个较大的字符串提取一个子串。

  ```java
  String greeting = "Hello";
  String s = greeting.substring(0,3);
  System.out.println(s);//输出：Hel
  ```

### 2.2.拼接

- Java 语言允许使用 + 号连接（拼接）两个字符串。

  ```java
  String a = "Hello ";
  String b = "World!";
  String message = a + b;
  System.out.println(message);//输出：Hello World!
  ```

- 当一个字符串与一个非字符串的值进行拼接时，**后者**被转换成字符串。

### 2.3.不可变字符串

- Sring 类没有提供用于修改字符串的方法。由于不能修改，所以在Java文档中将String 类对象称为不可变字符串。

### 2.4.检测字符串是否相等

- 可以用 **equals**方法检测两个字符串是否相等。对于表达式：s.equals(t)，如果字符串s与字符串t相等，则返回true，否则，返回false。

  **注：**不能使用 == 运算符号检测两个字符串是否相等！这个运算符只能确定两个字符串是否放在同一个位置上（同一地址）。

### 2.5.空串与Null串

- 空串 “ ” 是长度为0的字符串。可以使用代码检查一个字符串是否为空：

  ```java
  if(str.length() == 0)
  //或
  if(str.equals(""))
  ```

  空串是一个Java对象，有自己的串长度（0）和内容（空）。

- String还可以放一个特殊的值，名为 null，这表示没有任何对象与该变量有关。要检查一个字符串是否为 null ，要使用以下条件：

  ```java
  if(str == null)
  ```

- 要检查一个字符串既不是 null 也不是空串，需要使用以下条件：

  ```java
  if(str != null && str.length() != 0)
  ```


