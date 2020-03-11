---
title: JDBC相关问题
date: 2019-07-29 09:23:13
categories: Java
---

## 导入驱动jar包

1. 复制mysql-connector-java-5.1.37-bin.jar到项目的libs目录下
2. **右键-->Add As Library**

## 各个对象

1. DriverManager：驱动管理对象
		* 功能：
		
		① 注册驱动：**告诉程序该使用哪一个数据库驱动jar**
		static void registerDriver(Driver driver) :注册与给定的驱动程序 DriverManager 。 
		写代码使用：  Class.forName("com.mysql.jdbc.Driver");
		通过查看源码发现：在com.mysql.jdbc.Driver类中存在静态代码块

		```java
		static {
			        try {
			            java.sql.DriverManager.registerDriver(new Driver());
			        } catch (SQLException E) {
			            throw new RuntimeException("Can't register driver!");
			        }
		}
		```
		
		**注意：mysql 5之后的驱动jar包可以省略注册驱动的步骤。**
	
	​     ② 获取数据库连接：
	
	​		方法：static Connection getConnection(String url, String user, String password) 
	
	​			参数：
	
	​				url：指定连接的路径
	
	​				语法：jdbc:mysql://ip地址(域名):端口号/数据库名称
	
	​				例子：jdbc:mysql://localhost:3306/db3
	
	​					**细节：如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以简								写为：jdbc:mysql:///数据库名称**
	
	​				user：用户名
	
	​				password：密码 
	
2. Connection：数据库连接对象

    - 功能：

      ① 获取执行sql 的对象

    - Statement createStatement()

    * PreparedStatement prepareStatement(String sql)  

      ②管理事务：
    * 开启事务：setAutoCommit(boolean autoCommit) ：调用该方法设置参数为false，即开启事务
    * 提交事务：commit() 
    * 回滚事务：rollback() 

3. Statement：执行sql的对象

     ① 执行sql

    - boolean execute(String sql) ：可以执行任意的sql 了解 
    - int executeUpdate(String sql) ：执行DML（insert、update、delete）语句、DDL(create，alter、drop)语句
      - 返回值：影响的行数，可以通过这个影响的行数判断DML语句是否执行成功 返回值>0的则执行成功，反之，则失败。
   -  ResultSet executeQuery(String sql)  ：执行DQL（select)语句
   
4. ResultSet：结果集对象,封装查询结果

     - boolean next(): 游标向下移动一行，判断当前行是否是最后一行末尾(是否有数据)，如果是，则返回false，如果不是则返回true

     * getXxx(参数):获取数据
     		- Xxx：代表数据类型   如： int getInt() ,	String getString()
     	
     	* 参数：
     		1. int：代表列的编号,从1开始   如： getString(1)
     		2. String：代表列名称。 如： getDouble("balance")
     	
     * **结果集对象也需要关闭资源**
     
5. **PerparedStatement :执行sql对象**

     ① SQL注入问题：在拼接sql时，有一些sql的特殊关键字参与字符串的拼接。会造成安全性问题

     - 输入用户任意，输入密码 'a' or 'a' = 'a'  (false or true)

     ② 解决SQL注入问题：使用 PreparedStatement 对象来解决

     ③ 预编译的SQL：参数使用 ？作为占位符

     ④ 给 ？赋值：

     方法：setxxx(参数1，参数2)

     						- 参数1：？的位置 从1开始
     						- 参数2：？的值

     

     ## JDBC事务

     ### 操作

     - 开启事务：setAutoCommit(boolean autoCommit)：参数设置为false，即开始，默认为关闭
       - 在执行sql之前开启事务
     - 提交事务：commit()
       - 当所有sql都执行万提交事务
     - 回滚事务：rollback()
       - 在catch中回滚事务

     ## 数据库连接池

     > 当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问完之后，会将连接对象归还给容器。

     好处：

     	1. 节约资源
      	2. 用户访问高效

     标准接口：DataSource 

     - 方法：
       - 获取连接：getConnection()
       - 归还连接：Connection.close()。如果连接对象Connection是从连接池中获取的，那么调用Connection.close()方法，则不会再关闭连接了。而是归还连接
     - 数据库厂商实现
       - C3P0：数据库连接池技术
       - Druid：数据库连接池实现技术，由阿里巴巴提供的

     ### C3P0数据库连接池技术

     步骤：

     1. 导入jar包
        - c3p0-0.9.5.2.jar
        - mchange-commons-java-0.2.12.jar
        - mysql-connector-java-5.1.37-bin.jar（切记不能忘了导入这个）
     2. 定义配置文件
        - 名称： c3p0.properties 或者 c3p0-config.xml
        - 路径：直接将文件放在src目录下即可。
     3. 创建核心对象 
        - 数据库连接池对象 ComboPooledDataSource
     4. 获取连接： getConnection

     注意：

     1. 使用默认配置

        ```java
        DataSource ds = new ComboPooledDataSource();
        ```

     2. 使用指定名称配置

        ```java
        DataSource ds = new ComboPooledDataSource("otherc3p0");
        ```

        

     ### Druid数据库连接池技术

     步骤：

     1.  导入jar包
        - druid-1.0.9.jar
     2. 定义配置文件
        - properties形式
        - 可以叫任意名称，可以放在任意目录下
     3. 加载配置文件，使用Properties类
     4. 获取数据库连接池对象：通过工厂类获取  DruidDataSourceFactory
     5. 获取连接：getConnection

     定义工具类：

     1. 定义一个类 JDBCUtils
     2. 提供静态代码块加载配置文件，初始化连接池对象
     3. 提供方法
        - 获取连接方法：通过数据库连接池获取连接
        - 释放资源
        - 获取连接池的方法 

     

     ## Spring JDBC

     步骤：

     1. 导入jar包

     2. 创建JdbcTemplate对象，依赖于数据源DataSource

        ```java
        JdbcTemplate template = new JdbcTemplate(ds);
        ```

     3. 调用JdbcTemplate的方法来完成CRUD的操作

        - update()：执行DML语句。增、删、改语句
        - queryForMap()：查询结果将结果集封装为map集合，将列名作为key，将值作为value 将这条记录封装为一个map集合 。**注意：这个方法查询的结果集长度只能是1（真能查询一条记录）**
        - queryForList()：查询结果将结果集封装为list集合
        - query()：查询结果，将结果封装为JavaBean对象
          - query的参数：RowMapper
            - 一般我们使用BeanPropertyRowMapper实现类。可以完成数据到JavaBean的自动封装
            - new BeanPropertyRowMapper<类型>(类型.class)
        - queryForObject：查询结果，将结果封装为对象
          - 一般用于聚合函数的查询

     

     

     

     

     

     

