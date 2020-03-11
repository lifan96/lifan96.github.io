---
title:List&Set集合相关
date: 2019-01-30 09:23:13
categories: Java
---

# 第一部分 List接口

## List接口的特点

> java.util.List接口 extends Collection接口

1.有序的集合,存储元素和取出元素的顺序是一致的(存储123 取出123)
2.有索引,包含了一些带索引的方法
3.允许存储重复的元素

## List 接口中带索引的方法（特有）

- public void add(int index, E element): 将指定的元素，添加到该集合中的指定位置上。

- public E get(int index):返回集合中指定位置的元素。

- public E remove(int index): 移除列表中指定位置的元素, 返回的是被移除的元素。

- public E set(int index, E element):用指定元素替换集合中指定位置的元素,返回值的更新前的元素。

注意:
  操作索引的时候,一定要防止索引越界异常
  IndexOutOfBoundsException:索引越界异常,集合会报
  ArrayIndexOutOfBoundsException:数组索引越界异常
  StringIndexOutOfBoundsException:字符串索引越界异常

## List集合遍历方式

1. 使用普通的for循环
2. 使用迭代器
3. 使用增强for

### LinkedList集合的特点

1.底层是一个链表结构:查询慢,增删快
2.里边包含了大量操作首尾元素的方法
**注意:使用LinkedList集合特有的方法,不能使用多态**

- public void addFirst(E e):将指定元素插入此列表的开头。
- public void addLast(E e):将指定元素添加到此列表的结尾。
- public void push(E e):将元素推入此列表所表示的堆栈。
- public E getFirst():返回此列表的第一个元素。
- public E getLast():返回此列表的最后一个元素。
- public E removeFirst():移除并返回此列表的第一个元素。
- public E removeLast():移除并返回此列表的最后一个元素。
- public E pop():从此列表所表示的堆栈处弹出一个元素。
- public boolean isEmpty()：如果列表不包含元素，则返回true。

---

---

# 第二部分 Set接口

> java.util.Set接口 extends Collection接口

## Set接口的特点

1.**不允许存储重复的元素**
2.没有索引,没有带索引的方法,也**不能使用普通的for循环遍历**

### HashSet集合

> java.util.HashSet集合 implements Set接口

1.不允许存储重复的元素
2.没有索引,没有带索引的方法,也**不能使用普通的for循环遍历**
3.**是一个无序的集合,存储元素和取出元素的顺序有可能不一致**
4.**底层是一个哈希表结构(查询的速度非常的快)**

HashSet存储自定义类型元素
set集合报错元素唯一:存储的元素(String,Integer,...Student,Person...),必须重写hashCode方法和equals方法
要求:同名同年龄的人,视为同一个人,只能存储一次

### LinkedHashSet集合

> java.util.LinkedHashSet集合 extends HashSet集合

LinkedHashSet集合特点:底层是一个哈希表(数组+链表/红黑树)+链表:多了一条链表(记录元素的存储顺序),**保证元素有序**

## 哈希值
哈希值:是一个十进制的整数,由系统随机给出(就是对象的地址值,是一个逻辑地址,是模拟出来得到地址,不是数据实际存储的物理地址)
在Object类有一个方法,可以获取对象的哈希值，int hashCode() 返回该对象的哈希码值。
**hashCode方法的源码:**
  public native int hashCode();
  native:代表该方法调用的是本地操作系统的方法


