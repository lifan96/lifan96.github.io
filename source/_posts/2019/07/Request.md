---
title: Request
date: 2019-07-25 10:23:13
categories: Java
---

## Request和Response对象原理

1. Tomcat服务器会根据请求url中的资源路径，创建对应的ServletDemo1的对象
2. Tomcat服务器，会创建request和 response对象，request对象中封装请求数据
3. Tomcat将request和response两个对象传递给service方法，并且调用service方法
4. 程序员通过request对象获取请求数据，通过response对象来设置响应消息数据
5. 服务器再给浏览器做出响应之前，会从response对象中拿程序员设置的响应数据

## Request

1. 继承体系结构

   ServletRequest（接口）

   ​         |  继承

   HttpServletRequest（接口）

   ​          | 实现

   org.apache.catalina.connector.RequestFacade@202c2dc1（Tomcat中）

2. 获取请求消息

   - **获取请求行数据**

     方法：

     - 获取请求方式

       ```java
       String getMethod()
       ```

     - **获取虚拟目录：/day14**

       ```java
       String getContextPath()
       ```

     - 获取Servlet路径：/demo1

       ```java
       String getServletPath()
       ```

     - 获取Get请求参数：name=zhansan

       ```java
       String getQueryString()
       ```

     - **获取请求URI**

       ```java
       String getRequestURI() // /day14/demo1
       StringBUffer getRequestURL() // http://localhost:8080/day14/demo1
       ```

     - 获取协议版本：HTTP/1.1

       ```java
       String getProtocol()  //父类中
       ```

     - 获取客户机的IP

       ```java
       String getRemoteAddr() //父类中
       ```

   - **请求头数据**

     方法：

     - **String getHeader(String name)：通过请求头的名称获取请求头的值**
     - Enumeration<String> getHeaderNames()：获取所有请求头名称

    - **获取请求体数据**
   
        - **只有POST请求方式，才有请求体**，在请求体中封装了POST请求的请求参数
        - 步骤：
          - 获取流对象
            - **BufferedReader getReader()：获取字符输入流，只能操作字符数据-**ServletInputStream getInputStream()：获取字节输入流，可以操作所有所有类型的数据
          - 再从流对象中拿数据
        
        ```java
        String line = null;
                while ((line = br.readLine()) != null){
                    System.out.println(line);
                }
        ```
   
3. 其他功能
   
   - **获取请求参数通用方式**（get和post通用）
     
     - **String getPrarmeter(String name)：根据请求参数名称获取请求参数值**
     - String[] getPrarmeterValues(String name)：根据请求参数名称获取请求参数值的数组
     - Enumeration<String> getParameterNames()：获取所有请求参数名称
     - Map<String,String[ ]> getParameterMap()：获取所有参数的map集合
     
   - **请求转发**
   
     步骤 ：
   
     - 通过request对象获取请求转发器对象：RequestDispatcher getRequestDispatcher (String Path)
     
     - 通过RequestDispatcher 对象调用方法转发：forward(ServletRequest request ,ServletResponse response)
     
     - **特点：**
     
       - 浏览器地址状态栏路径不发生变化
     
       - 只能转发到当前服务器内部资源中
     
       - **转发是一次请求**
     
    - **共享数据**
   
      request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
   
      方法：
   
      - setAttribute(String name,Object obj)：存储数据
      - Object getAttribute(String name)：通过键获取值
      - removeAttribute(String name)：通过键移除键值对
   - 获取ServletContext：
   
     ServletContext getServletContext()

```
 ### 中文乱码问题
     
 - get方式：Tomcat 8 已经将中文乱码问题解决
     
 - post方式：会乱码
     
   解决：在获取参数前，设置编码 request.setCharacterEncoding("UTF-8");
```

​    


   ## BeanUtils工具类

   简化数据封装，用于封装JavaBean的

   1. JavaBean：标准的Java类
   	- 要求：	
       - 类必须被public修饰
            	  - 必须提供空参的构造器
                   - 成员变量必须使用private修饰
                   - 提供公共setter和getter方法
   2. 功能：封装数据

   




