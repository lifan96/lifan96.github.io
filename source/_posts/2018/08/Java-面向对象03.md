---
title: Java 面向对象03
date: 2018-08-26 18:13:32
tags:
categories: Java
copyright:
---

---

# 类的继承

## 继承的实现extends

![image](https://wx1.sinaimg.cn/large/80ceacb8ly1fun9snri09j208504nt8y.jpg)

> 在 Java中，类的继承是指在一个现有类的基础上去构建一个新的类，构建出来的新类被称作子类，现有类被称作父类，子类会自动拥有父类所有可继承的属性和方法。

- 在程序中，如果想**声明一个类继承另一个类，需要使用 extends 关键字。**

```java
//声明一个 Animal 类
class Animal{
    String name;               //定义name属性
    //定义动物叫的方法
    void shout(){
        System.out.println("动物发出叫声");
    }
}
//定义 Dog 类继承Animal 类
class Dog extends Animal{
    //定义一个打印 name 的方法
    public void printName(){
        System.out.println("name="+name);
    }
}
//定义一个测试类
public class Example{
    public static void main(String[] args){
        Dog dog = new Dog();           //创建一个Dog类的实例对象
        dog.name="沙皮狗"；             //为Dog类的 name 属性进行赋值
        dog.printName()；              //为Dog类的 getInfo()方法
        dog.shout();                  //调用Dog类继承来的 shout()方法
    }
}
```

**注：**

**① 在Java中，类只支持单继承，不允许多重继承，也就是一个类只能拥有一个直接父类。**

**② 多个类可以继承一个父类。**

**③在Java中，多层继承是可以的，即一个类的父类可以再去继承另外的父类，例如 C类继承自 B类，而B类又可以去继承 A类，这时，C类也可以称作 A类的子类。**

**④在Java中，子类和父类是一种相对概念，也就是说一个类是某个类父类的同时，也可以是另一个类的子类。**

---

## 重写父类的方法

> 在继承关系中，子类会自动继承父类中定义的方法，但有时在子类中需要对继承的方法进行一些修改，即对父类的方法进行重写。

- 在子类中重写的方法需要和父类被重写的方法具有**相同的方法名、参数列表以及返回值类型**。
- 子类重写父类方法时，不能使用比父类中被重写的方法更严格的访问权限。如父类中的方法是public 的，子类的方法就不能是 private 的。

---

## 抽象类 abstract class

> 当定义一个类时，常常需要定义一些方法来描述该类的行为特征，但有时这些方法实现的方式是无法确定的。例如 Animal 类，shout()方法用于表示动物的叫声，但针对不同的动物，叫声也是不同的，因此在 shout() 方法中无法准确描述动物的叫声。针对这种情况，Java允许在定义方法时不写方法体，**不包括方法体的方法为抽象方法，抽象方法必须使用 abstract 关键字来修饰。**

```java
abstract void shout();         //定义抽象方法 shout()
```

> 当一个类中包含了抽象方法，该类必须使用 abstract 关键字来修饰，使用 abstract 关键字修饰的类为抽象类。

```java
//定义抽象类 Animal
abstract class Animal{
    //定义抽象方法 shout()
    abstract int shout();
}
```

**注意：**

**① 包含抽象方法的类必须声明为抽象类，但抽象类可以不包含任何抽象方法，只需使用 abstract 关键字来修饰即可。**

**② 抽象类是不可以被实例化的，因为抽象类中可能包含抽象方法，抽象方法没有方法体，不可以被调用。**

**③ 如果想调用抽象类中定义的方法，需要创建一个子类，在子类中将抽象类中的抽象方法进行实现。**

```java
//定义抽象类 Animal
abstract class Animal{
    //定义抽象方法 shout()
    abstract void shout();
}
//定义一个Dog类继承抽象类Animal
class Dog extends Animal{
    //实现抽象方法 shout()
    void shout(){
        System.out.println("汪汪......");
    }
}
//定义测试类
public class Example{
    public static void main(String[] args){
        Dog dog = new Dog();   //创建Dog类的实例对象
        dog.shout();           //调用dog对象实现的shout()方法
    }
}
```

## 接口

> 如果一个抽象类中的所有方法都是抽象的，则可以将这个类用另外一种方式来定义，叫接口。

- 在定义接口时，需要使用interface关键字来声明。

```java
interface Animal{
    int ID=1;      //定义全局常量
    void breathe(); //定义抽象方法
    void run();
}
```

- 在接口中定义的方法和变量都包含一些默认修饰符。接口中定义的方法默认使用“public abstarct”来修饰，即抽象方法。接口中的变量默认使用“public static fianl”来修饰，即全局常量。
- 由于接口中的方法都是抽象方法，因此不能通过实例化对象的方式来调用接口中的方法。这就需要定义一个类，并使用 implements 关键字实现接口中的所有方法。

```java
//定义了Animal接口
interface Animal{
    int ID=1;      //定义全局常量
    void breathe(); //定义抽象方法 breathe()
    void run();
}
//Dog类实现了Animal接口
class Dog implements Animal{
    //实现 breathe()方法
    public void breathe(){
        System.out.println("狗在呼吸");
    }
    //实现 run()方法
    public void run(){
        System.out.println("狗在跑");
    }
}

//定义测试方法
public class Example{
    public static void main(String[] args){
        Dog dog = new Dog(); //创建Dog类的实例对象
        dog.breathe();     //调用Dog类的breathe()方法
        dog.run();        //调用Dog类的run()方法
    }
}
```

- 在程序中，还可以定义一个接口使用 extends 关键字去继承另一个接口。

### 接口的特点

- 接口中的方法都是抽象的，不能实例化对象。
- 当一个类实现接口时，如果这个类是抽象类，则实现接口中的部分方法即可，否则需要实现接口中的所有方法。
- 一个类通过 implements 关键字实现接口时，可以实现多个接口，被实现的多个接口之间要用逗号隔开。
- 一个接口可以通过 extends 关键字继承多个接口，接口之间用逗号隔开。

```java
interface Running{
	...
}
interface Flying{
    ...
}
interface Eating extends Running,Flying{
    ...
}
```

- 一个类在继承另一个类的同时还可以实现接口，此时，extends 关键字必须位于 implements 关键字之前。

```java
class Dog extends Canidae implements Animal{ //先继承后实现
    ...
} 
```

