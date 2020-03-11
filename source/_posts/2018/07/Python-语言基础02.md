---
title: Python 语言基础02
date: 2018-07-17 12:30:18
categories: Python
---

## 字符串和编码

![image1](https://wx3.sinaimg.cn/large/80ceacb8ly1ftblmcf9kij20gg06a0ss.jpg)

- 在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。

- 用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件：

![image2](https://ws1.sinaimg.cn/large/80ceacb8ly1ftblnpacltj208j07qdg8.jpg)

- 浏览网页的时候，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器：

![image3](https://wx2.sinaimg.cn/large/80ceacb8ly1ftblp0mtntj208e07edg3.jpg)

### Python的字符串

>在最新的Python 3版本中，字符串是以**Unicode编码**的，也就是说，Python的字符串支持多语言。

对于单个字符的编码：

- ord() 函数获取字符的整数表示。
```python
>>> ord('A')
65
>>> ord('中')
20013
```

- chr() 函数把编码转换成对应的字符。
```python
>>> chr(66)
'B'
>>> chr(25991)
'文'
```
---

>由于 Python 的字符串类型是`str`，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把`str`变为以字节为单位的`bytes`。 

- Python 对 bytes 类型的数据用**带b前缀**的单引号或双引号表示：x = b'ABC'

- 以Unicode表示的`str`通过 encode() 方法可以编码为指定的 bytes。
```python
>>> 'ABC'.encode('ascii')
b'ABC'
>>> '中文'.encode('utf-8')
b'\xe4\xb8\xe6\x96\x87'
```

### **!!!注**：</br>
1.纯英文的 str 可以用 ASCII 编码为 bytes，内容是一样的。</br>
2.含有中文的 str 可以用 UTF-8 编码为bytes，但无法用 ASCII 编码，因为中文编码超出了 ASCII 编码的范围，Python会报错。

---

>反过来，如果我们从网络或磁盘上读取了字节流，那么读到的数据就是 bytes  。要把 bytes 变为str ，就需要用 decode() 方法。

```python
>>>b'ABC'.decode('ascii')
'ABC'
>>>b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
'中文'
```
### **!!!注**：</br>
1.如果 bytes 中包含无法解码的字节，decode() 方法会报错。</br>
2.如果 bytes 中只有一小部分无效字节，可以传入errors='ignore' 忽略错误的字节。

---

### 其他
- 要计算 str 包含**多少个字符**，可以用 len() 函数。</br>

- 要计算 bytes 包含**多少个字节**，可以用 len() 函数。</br>

- 在操作字符串时，我们经常遇到 str 和 bytes 的互相转换。为了避免乱码问题，应当始终坚持使用 UTF-8 编码对 str 和 bytes 进行转换。</br>

- 由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；

第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

申明了UTF-8编码并不意味着你的.py文件就是UTF-8编码的，必须并且要确保文本编辑器正在使用UTF-8 without BOM编码。

---

## 格式化

![image3](https://wx3.sinaimg.cn/large/80ceacb8ly1ftbncmjqnvj20c206f0st.jpg)

在Python中，采用的格式化方式和C语言是一致的，用%实现，举例如下：

```python
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

常见的占位符有：

| 占位符 | 替换内容 |
| :---------:|:---------:|
| %d |整数|
| %f |浮点数|
| %s |字符串|
| %x |十六进制整数|

### **!!!注**：</br>
1.格式化整数和浮点数还可以指定是否补0和整数与小数的位数。

2.如果你不太确定应该用什么，%s 永远起作用，它会把任何数据类型转换为字符串。

3.有些时候，字符串里面的%是一个普通字符怎么办？这个时候就需要转义，用%%来表示一个%。

### format()
>另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}……，不过这种方式写起来比%要麻烦得多。
```python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```

