---
title: Python 语言基础04
date: 2018-07-20 16:53:18
categories: Python
---

# Python 的特性

## list
>Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。

```python
>>> classmates = ['Michael','Bob','Tracy']
>>> classmates
['Michael','Bob','Tracy']
```

- 变量 classmates 就是一个 list 。用**len()** 函数可以获得list**元素的个数**:
```python
>>> len(classmates)
3
```

- 用索引来访问list中每一个位置的元素，记得**索引是从 0 开始的**。当索引超出范围，Python会报一个IndexError 错误，所以，要确保索引不要越界，记得最后一个元素的索引是**len(classmates) - 1**。
```python
>>> classmates[0]
'Michael'
```

- 除了计算索引位置外，还可用 -1 做索引，直接获取最后一个元素，以此类推，可以获取倒数第二个、第三个：
```python
>>> classmates[-1]
'Tracy'
```

- list 是一个可变的有序表，可以使用函数 **append()** 往 list 中追加元素到**末尾**:
```python
>>> classmates.append('Adam')
>>> classmates
['Michael','Bob','Tracy','Adam']
```

- 使用函数 **insert()** 将元素插入到指定位置，比如索引为 1 的位置:
```python
>>> classmates.insert(1,'Jack')
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
```

- 要删除list **末尾的元素**，用 **pop()** 方法：
```python
>>> classmates.pop()
'Adam'
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy']
```

- 要删除指定位置的元素，用 **pop(i)** 方法，其中 i 是索引位置：
```python
>>> classmates.pop(1)
'Jack'
>>> classmates
['Michael', 'Bob', 'Tracy']
```

- 要把某个元素替换成别的元素，可以直接赋值给对应的索引的位置：
```python
>>> classmates[1] = 'Sarah'
>>> classmates
['Michael', 'Sarah', 'Tracy']
```

- list 里面的元素的数据类型也可以不同，比如：
```python
>>> L = ['Apple', 123, True]
```

- list 元素也可以是另一个 list（list的嵌套），比如：
```python
>>> s = ['python', 'java', ['asp', 'php'], 'scheme']
>>> len(s)
4
```
拆开写：
```python
>>> p = ['asp', 'php']
>>> s = ['python', 'java', p, 'scheme']
#如果想拿到 ‘php’ 可以写成p[1] 或者 s[2][1]，因此 s 可以看成是一个二维数组。
```

- 如果list中一个元素也没有，就是一个**空的list，它的长度为0**。

---

## tuple
>另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就**不能修改**。

```python
>>> classmates = ('Michael','Bob','Tracy')
```

**!!!注：**classmates这个tuple不能变了，**它没有append(),insert()这样的方法**，其他获取元素的方法和list是一样的，但不能赋值成另外的元素。

- 不可变的tuple有什么意义？？？</br>
  因为tuple不可变，所以代码更加安全。如果可能，能用tuple替代list就尽量用tuple。

- tuple的陷阱：当定义一个tuple时，在定义的时候，tuple的元素就必须确定下来。如果要定义一个空的tuple，可以写成（）；但是，要定义一个只有1个元素的tuple：

  ```python
  >>> t = (1)
  >>> t
  1
  ```

  定义的不是tuple，是1这个数！这是因为括号()既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义，因此，Python规定，这种情况下，按小括号进行计算，计算结果自然是1。 

  所以，**只有1个元素的tuple**定义时必须加一个**逗号,**，来消除歧义： 
  ```python
  >>> t = (1,)
  >>> t
  (1,)
  ```

## 小结
>list和tuple是Python内置的有序集合，一个可变，一个不可变。根据需要来选择使用它们。
