---
title: Tomcat启动相关问题
date: 2019-07-25 15:23:13
categories: Java
---

## 可能遇到的问题

1. 黑窗口一闪而过：
				
	- 原因： 没有正确配置JAVA_HOME环境变量
	
	- 解决方案：正确配置JAVA_HOME环境变量
	
2. 启动报错：

      - 暴力：找到占用的端口号，并且找到对应的进程，杀死该进程

        - netstat -ano

      - 温柔：修改自身的端口号 conf/server.xml

        ```xml
         <Connector port="8888" protocol="HTTP/1.1"
        	               connectionTimeout="20000"
        	               redirectPort="8445" />
        ```
        
      - 一般会将tomcat的默认端口号修改为80。80端口号是http协议的默认端口号。

      - 好处：在访问时，就不用输入端口号

## 部署

1. 直接将项目放到webapps目录下即可。

   - 简化部署：将项目打成一个war包，再将war包放置到webapps目录下。
     				   war包会自动解压缩

2. 配置conf/server.xml文件

   在<Host>标签体中配置
   <Context docBase="D:\hello" path="/hehe" />

   * docBase:项目存放的路径
   * path：虚拟目录

3. 在conf\Catalina\localhost创建任意名称的xml文件。

