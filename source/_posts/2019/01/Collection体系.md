---
title:Collection体系
date: 2019-01-31 09:23:13
categories: Java
---

![批注 2019-08-20 094655](https://wx4.sinaimg.cn/large/80ceacb8ly1g65xt2ljuhj20jw088q3e.jpg)

## HashMap

1. Java 8 以前：数组+链表

![批注 2019-08-20 103405](https://wx4.sinaimg.cn/large/80ceacb8ly1g65xv88xirj20fi06vq34.jpg)

数组默认大小16，也就是存着16个链表的头结点。链表长度会随着元素的增多而边长，时间复杂度由O(1)变成O(n)。



2. Java 8 及以后：数组+链表+红黑树

   ![批注 2019-08-20 103805](https://ws3.sinaimg.cn/large/80ceacb8ly1g65xzdh1jpj20dp07aq32.jpg)

使用常量TREEIFY_THRESHOLD来决定使用链表还是红黑树，性能从O(n)提高到O(logn)

3. HashMap：put方法的逻辑
   - 如果HashMap未被初始化过，则初始化
   - 对key求hash值，然后计算下标
   - 如果没有碰撞，直接放入桶中
   - 如果碰撞了，以链表党的方式连接到后面
   - 如果链表长度超过阀值，就把链表转成红黑树
   - 如果链表长度低于6，就把红黑树转回链表
   - 如果节点已经存在就替换旧值
   - 如果桶满了（容量16*加载因子0.75），就需要resize（扩容2倍后重排）
4. HashMap：get方法
   - 使用键对象的hashCode，通过hash算法，找到key的位置
   - 调用key的equals方法获取值
5. 如何减少碰撞
   - 扰动函数：促使元素位置分布均匀，减少碰撞几率
   - 使用final对象，并采用合适的equals()和hashCode()方法
6. 扩容问题
   - 多线程环境下，调整大小会存在条件竞争，容易造成死锁
   - rehashing是一个比较耗时的过程

## 如何优化HashTable？

- 通过锁细粒度化，将整个锁拆解成多个锁进行优化
  - 早期ConcurrentHashMap：通过分段锁Segment来实现（数组+链表）
  - 当前ConcurrentHashMap：CAS+synchronized使锁更细化（数组+链表+红黑树）

 

## ConcurrentHashMap

1. put方法
   - 判断Node[]数组是否初始化，没有则进行初始化操作
   - 通过hash定位数组的索引坐标，是否有Node节点，如果没有则使用CAS进行添加（链表的头结点），添加失败则进入下次循环
   - 检查到内部正在扩容，就帮助它一块扩容
   - 如果f!=null，则使用synchronized锁住f元素（链表/红黑二叉树的头元素）
     - 如果是Node（链表结构）则执行链表的添加操作
     - 如果是TreeNode（树型结构）则执行树添加操作
   - 判断链表长度已经达到临界值8，将链表转换为树结构

总结：比起Segment，锁拆得更细

- 首先使用无锁操作CAS插入头结点，失败则循环重试
- 若头结点已存在，则尝试获取头结点的同步锁，在进行操作

*注意事项：*

- size()方法和mappingCount()方法的异同，两者计算是否准确？
- 多线程环境下如何进行扩容?

## 三者的区别



- HashMap 线程不安全，数组+链表+红黑树
- HashTable 线程安全，锁住整个对象，数组+链表
- ConcurrentHashMap 线程安全，是对HashTable的锁粒度优化，CAS+同步锁，数组+链表+红黑树
- HashMap 的key、value均可为null，而其他的两个类不可以