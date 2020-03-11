---
title: Java 面向对象04
date: 2018-08-27 17:51:33
tags:
categories: Java
copyright:
---

# 多态

> 由于参数类型不同而导致执行效果各异的现象就是多态。

## 多态的实现

> 在Java中为了实现多态，允许使用一个父类类型的变量来引用一个子类类型的对象，根据被引用子类对象特征的不同，得到不同的运行结果。

```java
//定义接口 Animal
interface Animal{
    void shout();        //定义抽象shout()方法
}
//定义Cat类实现Animal接口
class Cat implements Animal{
    //实现sout()方法
    public void shout(){
        System.out.println("喵喵......");
    }
}
//定义Dog类实现Animal接口
class Dog implements Animal{
    //实现shout()方法
    public void shout(){
        System.out.println("汪汪.....");
    }
}
//定义测试类
public class Example{
    public static void main(String[] args){
        Animal an1 = new Cat();   //创建Cat对象，使用Animal类型的变量an1引用
        Animal an2 = new Dog();   //创建Dog对象，使用Animal类型的变量an2引用
        animalShout(an1);         //调用animalShout()方法，将an1作为参数传入
        animalShout(an2);         //调用animalShout()方法，将an2作为参数传入
    }
    //定义静态的animalShout()方法，接受一个Animal类型的参数
    public static void animalShout(Animal an){
        an.shout();               //调用实际参数的shout()方法
    }
}
```

## 对象的类型转换

> 当子类对象当作父类使用时不需要任何显式地声明，需要注意的是，此时不能通过父类变量去调用子类中的某些方法。

- Java 提供了一个关键字instanceof,它可以判断一个对象是否为某个类（或接口）的实例或者子类实例。

> 对象（或者对象引用变量） instanceof 类（或接口）

---

# 关键字

## final 关键字

- final 修饰的变量（成员变量和局部变量）是常量，只能赋值一次。
- final 修饰的方法不能被子类重写。
- final 修饰的类不能被继承。

## static 关键字

- 静态变量

> 在定义一个类时，只是在描述某类事物的特征和行为，并没有产生具体的数据。只有通过new关键字创建该类的实例对象后，系统才会为每个对象分配空间，存储各自数据。某些特定的数据在内存中只有一份，而且能够被一个类的所有实例对象所共享。

**在Java类中，可以使用static 关键字来修饰成员变量，该变量称作静态变量。静态变量被所有实例共享，可以使用“类名.变量名”的形式来访问或赋值。**

**注：static 关键字只能用于修饰成员变量，不能用于修饰局部变量。**

- 静态方法

> 在不创建对象的情况下就可以调用某个方法，也可以说是使该方法不必和对象绑在一起。只需在类中定义的方法前加上static关键字即可，这种方法为静态方法。静态方法可以使用“类名.方法名”的 方式来访问。

**注：在一个静态方法中只能访问用 static 修饰的成员，原因在于没有被 static 修饰的成员需要先创建对象才能访问，而静态方法在被调用时可以不创建任何对象。**

- 静态代码块

> 在Java中，使用一对大括号包围起来的若干行代码被称为一个代码块，用static 关键字修饰的代码块称为静态代码块。

**当类被加载时，静态代码块会执行，由于类只加载一次，因此静态代码块只执行一次。**

- 单例模式

> 单例模式是Java中的一种设计模式，它是指在设计一个类时，需要保证在整个程序运行期间针对该类只存在一个实例对象，就好像我们生存的世界只有一个月亮。

```java
class Single{
    //自己创建一个对象
    private static Single INSTANCE = new Single(); 
    private Single(){}                   //私有化构造方法
    public static Single getInstance(){  //提供返回该对象的静态方法
        return INSTANCE;
    }
}
```

- 类的构造方法使用 private 修饰，声明为私有，这样就不能在类的外部使用new关键字来创建实例对象了。
- 在类的内部创建一个该类的实例对象，并使用静态变量INSTANCE引用该对象，由于变量应该禁止外界直接访问，因此使用private修饰，声明为私有成员。
- 为了让类的外部能够获得类的实例对象，需要定义一个静态方法 getInstance(),用于返回该类实例INSTANCE。由于方法是静态的，外界可以通过：类名.方法名的方式来访问。