---
title: Python 语言基础03
date: 2018-07-19 12:02:14
categories: Python
---

>基础语法分为两块，包含条件判断和循环两块。条件判断主要是if语句的相关使用。循环主要是while模块的使用。

# 条件判断

在Python程序中，用 if 语句实现：
![image1](https://wx4.sinaimg.cn/large/80ceacb8ly1ftf20ds8lrj204u086aai.jpg)
**注意不要少了冒号 ：**

### if 语句完整结构：
```python
if <条件判断1>:
	<执行1>
#elif 为 else if 的缩写
elif <条件判断2>:
	<执行2>
elif <条件判断3>:
	<执行3>
else:
	<执行4>
```
### if 语句特点：
**条件判断从上向下匹配，当满足条件时执行对应的块内语句，后续的elif和else都不再执行。**

**!!!注：**因为 input() 返回的数据类型是 str ， str 不能直接和整数比较，必须先把 str 转换成整数。Python提供了 int() 函数来完成这件事情。

---

# 循环

**循环是让计算机做重复任务的有效的方法。**

- 第一种循环：for ... in 循环，比如计算1-10的整数之和，可以用一个sum变量做累加。

```python
sum = 0
for x in [1,2,3,4,5,6,,7,8,9,10]:
	sum = sum + x
print(sum)
```
- 第二种循环：while 循环，只要满足条件，就不断循环，条件不满足时退出循环。比如计算100以内所有奇数之和。

```python
sum = 0
n = 99
while n > 0:
	sum = sum + n
	n= n - 2
print(sum)
```
　　在循环内部变量n不断自减，直到变为-1时，不再满足while条件，循环退出。
　　
# break 和 comtinue

>break语句可以在循环过程中直接退出循环，而continue语句可以提前结束本轮循环，并直接开始下一轮循环。这两个语句通常都必须配合if语句使用。**要特别注意**，不要滥用break和continue语句。break和continue会造成代码执行逻辑分叉过多，容易出错。
