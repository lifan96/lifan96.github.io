---
title: Response
date: 2019-07-29 20:19:13
categories: Java
---

## HTTP协议

1. 请求消息：客户端发送给服务器端的数据
	* 数据格式：
		- 请求行
		
		- 请求头
		
		- 请求空行
		
		- 请求体
	
2. 响应消息：服务器端发送给客户端的数据

   - 数据格式：

     - 响应行

       - 组成：协议和版本  响应状态码   状态码描述

       - 响应状态码：服务器告诉客户端浏览器请求和响应的一个状态

         - 1XX：服务器就收客户端消息，但没有接受完成，等待一段时间后，发送1xx多状态码

         - 2XX：成功。代表：200

         - 3XX：重定向。代表：302(重定向)，304(访问缓存)

         - 4XX：客户端错误

           404（请求路径没有对应的资源） 

           405：请求方式没有对应的doxxx方法

         - 5XX：服务器端错误。代表：500(服务器内部出现异常)

     - 响应头

       - 格式：头名称 ：值
       - 常见响应头：
         - Content-Type：服务器告诉客户端本次响应体数据格式以及编码格式
         - Content-disposition：服务器告诉客户端以什么格式打开响应体数据
           - in-line:默认值,在当前页面内打开
           - attachment;filename=xxx：以附件形式打开响应体。文件下载

     - 响应空行

     - 响应体：传输的数据

## Response

### 功能：设置响应消息

1. 设置响应行

   - 格式：HTTP/1.1 200 ok
   - 设置状态码：setStatus(int sc) 

2. 设置响应头

   - setHeader(String name, String value) 

3. 设置响应体

   - 步骤：

     ① 获取输出流

     - 字符输出流：PrintWriter getWriter()
     - 字节输出流：ServletOutputStream getOutputStream()

     ② 使用输出流，将数据输出到客户端浏览器

### 重定向

1. 方式一

   ```java
   //1. 设置状态码为302
   response.setStatus(302);
   //2.设置响应头location
   response.setHeader("location","/day15/responseDemo2");
   ```

2. 方式二

   ```java
   response.sendRedirect("/day15/responseDemo2");
   ```

### 转发和重定向之间的区别

重定向的特点：**redirect**

1. 地址栏发生变化
2. 重定向可以访问其他站点(服务器)的资源
3. 重定向是两次请求。**不能使用request对象来共享数据**

转发的特点：**forward**

1. 转发地址栏路径不变
2. 转发只能访问当前服务器下的资源
3. 转发是一次请求，可以使用request对象来共享数据

### 服务器输出字符数据到浏览器

步骤：

1. 获取**字符输出流**
2. 输出数据

注意：

**乱码问题：**

- PrintWriter pw = response.getWriter();获取的流的默认编码是ISO-8859-1

- 设置该流的默认编码

- 告诉浏览器响应体使用的编码

  ```java
  //简单的形式，设置编码，是在获取流之前设置
  response.setContentType("text/html;charset=utf-8");
  ```

### 服务器输出字节数据到浏览器

步骤：

1. 获取**字节输出流**

   ```java
   ServletOutputStream sos = response.getOutputStream();
   ```

2. 输出数据

   ```java
   sos.write("你好".getBytes("utf-8"));
   ```


## ServletContext对象

1. 概念：代表整个web应用，可以和程序的容器(服务器)来通信，一个web项目只包含一个

2. 获取：

   - 通过 request  对象获取

     request.getServletContext();

   - 通过 HttpServlet 获取

     this.getServletContext();

3. 获取MIME类型：

   - MIME类型：在互联网通信过程中定义的一种文件数据类型

     - 格式： 大类型/小类型   text/html		image/jpeg
     - 获取：String getMimeType(String file) 
4. 域对象：共享数据

     - setAttribute(String name,Object value)
     - getAttribute(String name)
     - removeAttribute(String name)
     - **ServletContext对象范围：所有用户所有请求的数据**

5. 获取文件的真实(服务器)路径

     - 方法：String getRealPath(String path) 