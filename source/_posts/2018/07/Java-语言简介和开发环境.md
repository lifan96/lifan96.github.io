---
title: Java 语言简介和开发环境
date: 2018-07-15 11:42:50
categories: Java
---
### Java 语言简介

Java是一种高级计算机语言，它是由SUN公司（已被Oracle公司收购）于1995年5月推出的一种一个编写**跨平台**应用软件、完全**面向对象**的程序设计语言。

Java语言**简单易用、安全可靠**，主要面向Internet编程，自问世以来，与之相关的技术和应用发展的非常快。如今，Java技术无处不在。

Java三个开发方向

- Java  SE(Java Platform Standard Edition)标准版，是为开发普通桌面和商务应用程序提供的解决方案。Java SE是三个平台中最核心的部分，Java EE 和 Java ME 都是从Java SE 的基础上发展而来，**Java SE平台中包括了Java最核心的类库**，如集合、IO、数据库连接以及网络编程等。

- Java EE(Java Platform Enterprise Edition)企业版，是为开发企业级应用程序提供的解决方案。Java EE可以被看做一个技术平台，该平台用于开发、装配以及部署企业级应用程序，其中主要包括Servlet、JSPJavaBean、JDBC、EJB、WebService等技术。

- Java ME(Java Platform Micro Edition)小型版，是为了开发电子消费产品和嵌入式设备提供解决方案。


**Java语言的特点**：简单、面向对象、安全、跨平台、支持多线程。

### 开发环境搭建

SUN公司提供了一套Java开发环境，简称**JDK**(Java Development Kit),它是整个Java的核心，其中包括Java编译器、Java运行工具、Java文档生成工具、Java打包工具等。

除了JDK，还提供了一种**JRE**(Java Runtime Environment)工具，它是Java 运行环境。JRE中只包含Java运行工具，**JRE = JVM + API**，且**JDK工具中自带了一个JRE工具**，开发人员只用在计算机上**[安装JDK即可](http://www.oracle.com/technetwork/java/javase/downloads/index.html)**。

#### JDK目录介绍

JDK安装完毕后，会在硬盘上生成一个目录，该目录被称为JDK安装目录。

- bin 目录：该目录存放一些可执行程序，如javac.exe（Java 编译器）、java.exe（Java 运行工具）等等。

- db 目录：db目录是一个小型的数据库。装一个数据库软件，选择直接使用JavaDB即可。

- jre 目录：意为Java程序运行时环境。它包含Java虚拟机，运行时的类包、Java应用启动器以及一个bin目录。**不包含开发环境中的开发工具。**

- include 目录：由于JDK是通过C和C++实现的，因此在启动时需要引入一些C语言的头文件，该目录就是存放这些东西的。

- src.zip 文件：压缩文件，其中存放Java核心类的源代码，通过该文件可以查看Java基础类的源代码。

#### 特别注意：
> - **javac.exe** 是Java的编译工具，它可以将编写好的Java文件编译成字节码文件（可执行的Java程序）。Java源文件的扩展名为 **.java**,编译后生成的Java字节码文件的扩展名为**.class**。
>
> - **java.exe** 是Java运行工具，它会启动一个**Java虚拟机（JVM）**进程，Java虚拟机相当于一个虚拟的操作系统，它专门负责运行Java 编译器生成的字节码文件（.class 文件）

####  path 环境变量

>path环境变量是系统环境变量的一种，它是用于保存一系列的路径，每个路径之间以分号分隔。

设置path环境变量步骤（win10）：此电脑-->右键属性-->高级系统设置-->环境变量-->系统环境变量-->找到Path，将javac命令所在目录（JDK下bin目录）路径粘贴到其中-->设置完毕，打开命令行窗口输入javac，命令行会显示帮助信息。

![image](https://wx2.sinaimg.cn/large/80ceacb8ly1ftah5z7ugdj20r60e7dgw.jpg)

#### classpath 环境变量

>classpath 环境变量也用于保存一系列路径，它和 path 环境变量的查看与配置方式完全相同。当 Java 虚拟机需要运行一个类时，会在classpath环境变量中锁定路径下寻找所需的 class 文件。**注**：从JDK5.0开始，如果classpath 环境变量没有进行设置，Java虚拟机会自动将其设置为“.” ，也就是当前目录。

### 编辑器
- [notepad++](https://notepad-plus.en.softonic.com/)/[Editpuls](https://www.editplus.com/download.html)/[UltraEdit](http://www.ultraedit.com/downloads/uex.html): 文本编辑器，入门推荐

- [Eclipse](https://www.eclipse.org/downloads/)：IDE，插件式，通用灵活，中期可用

- [Inteilj Idea](http://www.jetbrains.com/idea/)：IDE，功能强大，新宠，Java EE 和 Java web 开发必备

