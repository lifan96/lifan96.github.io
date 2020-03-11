---
title: Java 面向对象02
date: 2018-08-23 12:52:26
categories: Java
copyright:
---

---

# 内部类

## 成员内部类

> 在一个类中除了可以定义成员变量、成员方法，还可以定义类，这样的类被称作**成员内部类**。**在成员内部类中可以访问外部类的所有成员。**

```java
class Outer{
    private int num = 4; //定义类的成员变量
    //下面的代码定义了一个成员方法，方法中访问内部类
    public void test(){
        Inner inner = new Inner();
        inner.show();
    }
    //下面的代码定义了一个成员内部类
    class Inner{
        void show(){
            //在成员内部类的方法中访问外部类的成员变量
            System.out.println("num = "+num);
        }
    }
}
public class Example{
    public static void main(String[] args){
        Outer outer = new Outer; //创建外部类对象
        outer.test();            //调用test()方法
    }
}
```

如果想通过外部类去访问内部类，则需要通过外部类对象去创建内部类对象。

> 外部类名**.**内部类名 变量名 = new 外部类名()**.**new 内部类名();

```java
public class Example{
    public static void main(String[] args){
        Outer.Inner inner = new Outuer().new Inner();//创建内部类对象
        inner.show();                                //调用 test() 方法
    }
}
```

**注：如果内部类被声明为私有，外界将无法访问。**

---

## 静态内部类

> 可以使用 static 关键字来修饰一个成员内部类，该内部类被称作静态内部类。它可以在不创建外部类对象的情况下被实例化。

> 外部类名**.**内部类名 变量名 = new 外部类名**.**内部类名();

```java
class Outer{
    private static int num = 6;
    //下面的代码定义了一个静态内部类
    static class Inner{
        void show(){
            System.out.println("num = "+num);
        }
    }
}
class Example{
    public static void main(String[] args){
        Outer.Inner inner = new Outer.Inner();//创建内部类对象
        inner.show();                         //调用内部类的方法
    }
}
```

**注：① 在静态内部类中只能访问外部类的静态成员。
② 在静态内部类中可以定义静态的成员，而在非静态的内部类中不允许定义静态的成员。**

---

## 方法内部类

> 方法内部类是指在成员方法中定义的类，它**只能在当前方法中被使用**。

```java
class Outer{
    private int num = 4;                         //定义成员变量
    public void test(){
        //下面是方法中定义的内部类
        class Inner{
            void show(){
                System.out.println("num = "+num);//访问外部类成员
            }
        }
        Inner in = new Inner();                   //创建内部类对象
        in.show();                                //调用内部类的方法
    }
}
public class Example{
    public static void main(String[] args){
        Outer outer = new Outer();               //创建外部类对象
        outer.test();                            //调用 test() 方法
    }
}
```

---

## 匿名内部类

> 匿名内部类是实现接口的一种简便写法。

```java
new 父类(参数列表) 或 父接口(){
    //匿名内部类实现部分
}
```

---

---

