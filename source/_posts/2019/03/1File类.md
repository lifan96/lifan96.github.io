---
title:File 类
date: 2019-03-10 09:23:13
categories: Java
---

## File 类概述

> `java.io.File` 类是文件和目录路径名的抽象表示，主要用于文件和目录的创建、查找和删除等操作。

java把电脑中的文件和文件夹(目录)封装为了一个File类,我们可以使用File类对文件和文件夹进行操作
我们可以使用File类的方法
  创建一个文件/文件夹
  删除文件/文件夹
  获取文件/文件夹
  判断文件/文件夹是否存在
  对文件夹进行遍历
  获取文件的大小
  File类是一个与系统无关的类,任何的操作系统都可以使用这个类中的方法

重点:记住这三个单词
  file:文件
  directory:文件夹/目录
  path:路径

## File类的静态成员变量

static String pathSeparator 与系统有关的路径分隔符，为了方便，它被表示为一个字符串。
static char pathSeparatorChar 与系统有关的路径分隔符。（路径分隔符）

- windows为 ;   

- linux为 :

static String separator 与系统有关的默认名称分隔符，为了方便，它被表示为一个字符串。
static char separatorChar 与系统有关的默认名称分隔符。（文件名称分隔符）

- windows为 \
- linux 为 /

```
操作路径:路径不能写死了
	C:\develop\a\a.txt  windows
	C:/develop/a/a.txt  linux
    "C:"+File.separator+"develop"+File.separator+"a"+File.separator+"a.txt"
```

## 相对路径与绝对路径

- 绝对路径:是一个完整的路径，以盘符(c:,D:)开始的路径
- 相对路径:是一个简化的路径，相对指的是相对于当前项目的根目录

注意:
    1.路径是不区分大小写
    2.路径中的文件名称分隔符windows使用反斜杠,反斜杠是转义字符,两个反斜杠代表一个普通的反斜杠

## File类的构造方法

- File(String pathname) 通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例。
  参数:
              String pathname:字符串的路径名称
              路径可以是以文件结尾,也可以是以文件夹结尾
              路径可以是相对路径,也可以是绝对路径
              路径可以是存在,也可以是不存在
              创建File对象,只是把字符串路径封装为File对象,不考虑路径的真假情况
- File(String parent, String child) 根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。
  参数:把路径分成了两部分String parent:父路径
           String child:子路径
   好处:
           父路径和子路径,可以单独书写,使用起来非常灵活;父路径和子路径都可以变化
- File(File parent, String child) 根据 parent 抽象路径名和 child 路径名字符串创建一个新 File 实例。
  参数:把路径分成了两部分
              File parent:父路径
              String child:子路径
   好处:
               父路径和子路径,可以单独书写,使用起来非常灵活;父路径和子路径都可以变化
               父路径是File类型,可以使用File的方法对路径进行一些操作,再使用路径创建对象

## 常用方法

### 获取功能的方法

- `public String getAbsolutePath() `：返回此File的绝对路径名字符串(获取构造方法中传递的路径)。

- ` public String getPath() ` ：将此File转换为路径名字符串(toString()就是调用的getPath()方法)。 

- `public String getName()`  ：返回由此File表示的文件或目录的名称。  

- `public long length()`  ：返回由此File表示的文件的长度(获取的是构造方法指定的文件大小，以字节为单位)。 

  注意：文件夹是没有大小概念的，不能获取文件夹的大小

  ​	如果构造方法给出的路径不存在，那么length方法返回0

### 判断功能的方法

- public boolean exists()` ：此File表示的文件或目录是否实际存在。

- `public boolean isDirectory()` ：此File表示的是否为目录(用于判断构造方法中给定的路径是否以文件夹结尾)。

- `public boolean isFile()` ：此File表示的是否为文件(用于判断构造方法中给定的路径是否以文件结尾)。

  注意：后两个方法使用前提，路径必须是存在的，否则都返回false

### 创建删除功能的方法

- public boolean createNewFile()` ：当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。 

  注：1. 此方法只能创建文件，不能创建文件夹

  ​        2.创建文件的路径存在，否则会抛出异常

- `public boolean delete()` ：删除由此File表示的**文件或目录**。  

- `public boolean mkdir()` ：创建由此File表示的目录(创建单级空文件夹)。

- `public boolean mkdirs()` ：创建由此File表示的目录，包括任何必需但不存在的父目录(创建单级或多级文件夹)。

  注：1. 后两个方法只能创建文件夹，不能创建文件

  ​        2.路径不存在，调用方法不会报错，同时还会创建文件夹

### 目录的遍历 

- public String[] list() ：返回一个String数组，表示该File目录中的所有子文件或目录。

- `public File[] listFiles()` ：返回一个File数组，表示该File目录中的所有的子文件或目录。  

  注意：1. list方法和listFiles方法遍历是构造方法中给出的目录

  ​           2. 如果构造方法中给出的目录的路径不存在，会抛出空指针异常

  ​           3. 如果构造方法中给出的路径不是一个目录，也会抛出空指针异常

### 文件过滤优化

在File类中有两个和ListFiles重载的方法,**方法的参数传递的就是过滤器**

- File[ ] listFiles(FileFilter filter)
  java.io.FileFilter接口:用于抽象路径名(File对象)的过滤器。
          作用:用来过滤文件(File对象)
          抽象方法:用来过滤文件的方法
          boolean accept(File pathname) 测试指定抽象路径名是否应该包含在某个路径名列表中。
           参数:

  ​         File pathname:使用ListFiles方法遍历目录,得到的每一个文件对象

- File[ ] listFiles(FilenameFilter filter)
  java.io.FilenameFilter接口:实现此接口的类实例可用于过滤器文件名。
          作用:用于过滤文件名称
          抽象方法:用来过滤文件的方法
          boolean accept(File dir, String name) 测试指定文件是否应该包含在某一文件列表中。
              参数:

  ​             File dir:构造方法中传递的被遍历的目录
  ​             String name:使用ListFiles方法遍历目录,获取的每一个文件/文件夹的名称

  注意:两个过滤器接口是没有实现类的,需要我们自己写实现类,重写过滤的方法accept,在方法中自己定义过滤的规则

