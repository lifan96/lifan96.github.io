---
title: servlet相关
date: 2019-07-25 16:48:13
categories: Java
---

## 快速入门

1. 创建JavaEE项目

2. 定义一个类，**实现Servlet接口**

3. 实现接口中的方法

4. 配置Servlet（在web.xml中配置，web-app标签中）

   ```xml
   <!--配置 servlet-->
       <servlet>
           <servlet-name>demo1</servlet-name>
           <servlet-class>cn.lifan.web.servlet.ServletDemo1</servlet-class>
       </servlet>
       
       <servlet-mapping>
           <servlet-name>demo1</servlet-name>
           <url-pattern>/demo1</url-pattern>
       </servlet-mapping>
   ```

## 执行原理

1. 当服务器接收到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet的中资源路径
2. 查找web.xml文件，是否有对应的 <url-parttern>标签体内容
3. 如果有，则会 找到对应的<servlet-calss>全类名
4. tomact将字节码文件加载进内存，并创建其对象
5. 调用其方法

## Servlet 中的生命周期

1. Servlet被创建时执行：执行init方法，只执行一次

   - **Servlet 什么时候被创建？**

     - 默认情况下，第一次访问时，Servlet被创建

     - 可配置执行Servlet配置的时机

       - 在<servlet>下配置

         - **第一次被访问时**，创建

           <load-on-startup>的值为负数

         - 在**服务器启动时**，创建

           <load-on-startup>的值为0或正整数

     - **Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例**

       - 多个用户同时访问时，可能存在线程安全问题
       - 解决办法：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要对修改值

2. 提供服务：执行service方法，执行多次

   - 每次访问Servlet时，Service方法都会被调用一次。

3. 被销毁：执行destroy方法，只执行一次 

   - Servlet被销毁时执行。服务器关闭时，Servlet被销毁
   - 只有服务器正常关闭时，才会执行destroy方法。
   - **destroy方法在Servlet被销毁之前执行**，一般用于释放资源

## Servlet 3.0

**支持注解配置。可以不需要web.xml了**

步骤：

1. 创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml
2. 定义一个类，实现Servlet接口
3. 复写方法.
4. 在类上使用@WebServlet注解，进行配置
   - @WebServlet("资源路径")

## Servlet体系结构

1. GenericServlet 抽象类（儿子）：将Servlet接口中做了默认空实现，只将service()方法作为抽象

   - 定义servlet类时，可以继承GenericServlet，实现 service()方法即可

2. HttpServlet 抽象类（孙子）：对 http协议的一种封装，简化操作

   - 定义类继承HttpServlet
- 复写doGet/doPost方法

## Servlet相关配置

1. urlPatterns:Servlet访问路径

   - 一个Servlet可以定义多个访问路径：@WebServlet({"/d4","/dd4"}

   - 路径定义规则

     **/xxx**

     /xxx/xxx：多层路径，目录结构

     *.do

