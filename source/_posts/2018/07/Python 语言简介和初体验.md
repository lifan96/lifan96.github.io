---
title: Python 语言简介和初体验
date: 2018-07-11 14:02:06
categories: Python
comments: false
---

> 文章纯手打，如果文章哪里有错别字还请谅解！
---

### Python语言介绍：	

- **面向对象，解释型计算机程序设计**

- **设计哲学**：优雅，明确，简单，可读性强

- **优点**：功能强大，开发效率高，应用广泛，易上手，语法简洁

- **缺点**：

  ①运行速度慢    和C语言相比，因为Python是解释型的语言，代码会在执行时会一行一行地翻译成CPU能理解的机器码
  ![image01](https://wx3.sinaimg.cn/large/80ceacb8ly1ftac0qb0eqj20am05274d.jpg)

  C语言，运行前直接编译成CPU能执行的机器码

  ②代码不能加密

   **用途**：网页开发、可视化（GUI）界面开发、网络、系统编程、数据分析、及其学习、网络爬虫、科学计算	
- **著名网站**：雅虎地图、谷歌中很多组成部分、Youtube、豆瓣网

- **与其他语言比较**：

```java
//Java
	public class Main{
	
		public static void main(String[] args){
		
		System.out.println("Hello World");
		
		}
	}
```
```python
#Python
#!/usr/bin/python
print("Hello World")
```
![image2](https://wx3.sinaimg.cn/large/80ceacb8ly1ftac6vgrd4j20by050t8w.jpg)
---

## 安装Python和配置环境： 

1.安装Python

**注**：确认设备为32位还是64位操作系统，注意平台分为AMD和Intel，特别要注意勾上	Add Python 3.6 to PATH，然后点“Install Now”即可完成安装。

2.启动Python

- 启动方式：Python图形化界面

- Windows:启动命令提示符窗口->输入python->退出exit()并回车

- Mac&&Linux:-打开终端->运行python3

3.Python Interpreter(Python解释器)

- python.exe 为python解释器

4.环境变量

- 将解释器的路径加入系统环境变量的path中

---

### 使用文本编辑器 

用文本编辑器写Python程序，然后保存为后缀为.py的文件，就可以用Python直接运行程序了。

**Python交互模式和直接运行.py文件有什么区别？**

- 直接输入 python 直接进入交互模式，相当于启动了Python解释器，但是等你一行一行输入源码，每输入一行就执行一行。
- 直接运行.py 文件相当于启动了Python解释器，然后一次性执行多行代码。

![image3](https://wx2.sinaimg.cn/large/80ceacb8ly1ftacckvcyaj208w06oweh.jpg)

### 输入和输出
- 输出

　　用print()在括号中加上字符串，就可以想屏幕上输出指定的文字。
``` python
print('Hello World!')
```
　　print()函数也可以接受多个字符串，用逗号","隔开，就可以连成一串输出。
```python
print('My name','is','xxx')
#输出结果
My name is xxx
```
　　print()会依次打印每个字符串，遇到逗号","就会输出一个空格。
```python
print('This is','my','book')
#输出结果
This is my book
```
　　print()也可以打印整数，或者计算结果：
```python
print(300)
300
print(100 + 200)
300
```
- 输入

　　Python提供了一个input(),可以让用户输入字符串，并存放到一个变量里。
```python
name = input() #输入任意字符，按下回车完成输入
name #输入变量名name，查看变量内容
Michael
```
　　input()可以让你显示一个字符串来提示用户。

```python
name = input('please enter your name: ')
please enter your name:
print('hello,', name)
```

### 小结
> 1.认识Python
> 2.学会如何把Python安装到计算机中，并且熟练打开和退出Python交互式环境。
>   - 在Windows上运行Python时，请先启动命令行，然后运行python。
>   - 在Mac和Linux上运行Python时，请打开终端，然后运行python3。
>
> 3.在Python交互式模式下，可以直接输入代码，然后执行，并立刻得到结果。
> 　命令行模式下，可以直接运行.py文件。
> 4.输入是Input，输出是Output，因此，我们把输入输出统称为Input/Output，或者简写为IO。


