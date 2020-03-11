---
title:Map相关
date: 2019-01-30 09:23:13
categories: Java
---

## Map集合的特点

> java.util.Map<k,v>集合

1.Map集合是一个双列集合,一个元素包含两个值(一个key,一个value)
2.Map集合中的元素,key和value的数据类型可以相同,也可以不同
3.Map集合中的元素,**key是不允许重复的**,value是可以重复的
4.Map集合中的元素,key和value是一 一对应

### HashMap集合特点

> java.util.HashMap<k,v>集合 **implements** Map<k,v>接口

1.HashMap集合底层是哈希表:查询的速度特别的快
  JDK1.8之前:数组+单向链表
  JDK1.8之后:数组+单向链表|红黑树(链表的长度超过8):提高查询的速度
2.HashMap集合是一个**无序的集合**,存储元素和取出元素的顺序有可能不一致

#### LinkedHashMap的特点

> java.util.LinkedHashMap<k,v>集合 **extends** HashMap<k,v>集合

1.LinkedHashMap集合底层是哈希表+链表(保证迭代的顺序)
2.LinkedHashMap集合是一个**有序的集合**,存储元素和取出元素的顺序是一致的

### Hashtable的特点

> java.util.Hashtable<K,V>集合 implements Map<K,V>接口

Hashtable:底层也是一个哈希表,是一个**线程安全**的集合,是**单线程集合,速度慢**
HashMap:底层是一个哈希表,是一个**线程不安全**的集合,是**多线程的集合,速度快**

HashMap集合(之前学的所有的集合):可以存储null值,null键
Hashtable集合,不能存储null值,null键

## 方法

1. boolean containsKey(Object key) 判断集合中是否包含指定的键。
     包含返回true,不包含返回false
2. public V get(Object key) 根据指定的键，在Map集合中获取对应的值。
     返回值:
     key存在,返回对应的value值
     key不存在,返回null
3. public V remove(Object key): 把指定的键 所对应的键值对元素 在Map集合中删除，返回被删除元素的值。
     返回值:V
     key存在,v返回被删除的值
     key不存在,v返回null
4. public V put(K key, V value):  把指定的键与指定的值添加到Map集合中。
     返回值:v
     存储键值对的时候,key不重复,返回值V是null
     **存储键值对的时候,key重复,会使用新的value替换map中重复的value, 返回被替换的value值**

## Map遍历方式

### 通过键找值的方式

Map集合中的方法:
Set<K> keySet() 返回此映射中包含的键的 Set 视图。
实现步骤:
1.使用Map集合中的方法keySet(),把Map集合所有的key取出来,存储到一 个Set集合中

2.遍历Set集合,获取Map集合中的每一个key
    使用迭代器/增强for遍历Set集合

3.通过Map集合中的方法get(key),通过key找到value

### 使用Entry对象遍历

Map集合中的方法:
Set<Map.Entry<K,V>> entrySet() 返回此映射中包含的映射关系的 Set 视图。

实现步骤:
1.使用Map集合中的方法entrySet(),把Map集合中多个Entry对象取出来,存储到一个Set集合中
Set<Map.Entry<String, Integer>> set = map.entrySet();

2.遍历Set集合,获取每一个Entry对象

3.使用Entry对象中的方法getKey()和getValue()获取键与值

## JDK1.9新特性

List接口,Set接口,Map接口:里边增加了一个静态的方法of,可以给集合一次性添加多个元素
static <E> List<E> of(E... elements)
使用前提:当集合中存储的元素的个数已经确定了,不在改变时使用
**注意**:
1.of方法只适用于List接口,Set接口,Map接口,不适用于接口的实现类
2.**of方法的返回值是一个不能改变的集合,集合不能再使用add,put方法添加元素,会抛出异常**
3.Set接口和Map接口在调用of方法的时候,不能有重复的元素,否则会抛出异常

```java
List<String> list = List.of("a", "b", "a", "c", "d");
Set<String> set = Set.of("a", "b", "c", "d");
Map<String, Integer> map = Map.of("张三", 18, "李四", 19, "王五", 20);

```