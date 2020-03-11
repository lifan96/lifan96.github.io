---
title: Java 语言基础05
date: 2018-08-05 18:28:04
categories: Java
---

# 异常

## 异常概念

> 在程序运行的过程中，会发生各种非正常状况，比如程序运行时磁盘空间不足，网络连接中断，被装载的类不存在。针对这种情况，在Java语言中，引入了异常，以异常类的形式对这些非正常情况进行封装，通过异常处理机制对程序运行时发生的各种问题进行处理。

![image](https://wx3.sinaimg.cn/large/80ceacb8ly1fu5y1awhtnj20ex07rgmd.jpg)

> Throwable 有两个直接子类Error 和 Exception，其中Error代表程序中产生的错误，Exception代表程序中产生的异常。

- Error 类称为错误类，它表示Java 运行时产生的系统内部错误或资源耗尽的错误，是比较严重的，仅靠修改程序本身是不能恢复执行的。

- Exception 类称为异常类，它表示程序本身可以处理的错误，在开发Java程序中进行的异常处理，都是针对Exception类及其子类。在Exception 类的众多子类中有一个特殊的**RuntimeException类，该类及其子类用于表示运行时异常**，除了此类，Exception 类下所有其他的子类都用于表示编译时异常。

- Throwable 类中的常用方法

  ![image](https://wx2.sinaimg.cn/large/80ceacb8ly1fu5y9wks7nj20m103rq3u.jpg)

## 异常处理

- try ... catch

  > Java 中提供一种对异常进行处理的方式——异常捕获

  ```java
  try{
      //程序代码块
  }catch(ExceptionType(Exception 类及其子类) e){
      //对ExceptionType的处理
  }
  ```

  其中在try 代码块中编写可能发生异常的Java 语句，catch 代码块中编写针对异常进行处理的代码。当try 代码块的程序发生了异常，系统会将这个异常的信息封装成一个异常对象，并将这个对象传递给catch代码块。catch 代码块需要一个参数指明它所能够接受的异常类型，这个参数的类型必须是Exception类或其子类。

  ---

- finally

  > 在程序中，有时候我们希望语句无论程序是否发生异常都要执行，这个时候在try ... catch语句后，加一个 finally 代码块。

  **注：**

  **不论程序是否发生异常还是使用 return 语句结束，finally语中的语句都会执行。用途：例如释放系统资源。**

  **在try ... catch中如果执行了System.exit(0)语句，finally中的语句就不会执行。System.exit(0)表示退出当前的Java虚拟机，Java虚拟机停止了，任何代码都不能再执行。**

  ---

- throws

  > 如果去调用一个别人写的方法时，是否知道别人写的方法是否会异常呢？这就很难做出判断。针对这种情况，Java中允许在方法的后面使用 throws 关键字对外声明该方法有可能发生的异常，这样调用者在调用方法时，就明确地知道该方法有异常，并且必须在程序中对异常进行处理，否则无法编译通过。

  ```java
  修饰符 返回值类型 方法名([参数1，参数2...])throws ExceptionType1[,ExceptionType2...]{
      
  }
  ```

  从上述语法格式中可以看出，throws关键字需要写在方法声明的后面，throws后面需要声方法中发生异常的类型，通常将这种做法称为**方法声明抛一个异常。**

## 异常分类

1. 编译时异常

   在Java中，Exception 类除了RuntimeException 类及其子类都是编译时异常。编译时异常的特点是Java 编译器会对其进行检查，如果出现异常就必须对异常进行处理，否则程序无法通过编译。

   **处理编译时期的异常的两种方式：**

   - 使用 try ... catch 语句对异常进行捕获。
   - 使用 throws 关键字声明抛出异常，调用者对其处理。

   ---

2. 运行时异常

   RuntimeException 类及其子类都是运行时异常。运行时异常特点是Java编译器不会对其检查，也就是说，当程序中出现这类异常时，即使没有使用 try ... catch 语句捕获或使用 throws 关键字声明抛出，程序也能编译通过，运行时异常一般是由程序中的逻辑错误引起的，在程序运行时无法恢复。

## 自定义异常

> Java允许用户自定义异常，但自定义的异常类必须继承自 Exception 或其子类。

   ```java
//下面的代码是自定义一个异常类继承自 Exception
public class MyException extends Exception{
    public MyException(){
        super();           //调用 Exception 无参的构造方法
    }
    
    public MyException(String message){
        super();		 //调用 Exception 有参的构造方法
    }
}
   ```

在实际开发中，如果没有特殊的要求，自定义的异常类只需继承 Exception 类，在构造方法中使用 super() 语句调用Exception 的构造方法即可。

使用自定义异常使用 throw 关键字，throw 关键字用于在方法中抛出异常的实例对象。

```java
throw Exception异常对象
```

