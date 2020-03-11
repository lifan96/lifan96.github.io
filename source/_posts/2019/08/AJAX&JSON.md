---
title: Ajax&Json
date: 2019-08-05 18:23:13
categories: Java
---

## AJAX

1. 概念：ASynchronous JavaScript And XML	**异步的JavaScript 和 XML**

   - 异步和同步：客户端和服务器端相互通信的基础上

   ```
   同步：客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作。
   异步：客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作。
   
   详细解释：
   Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。 通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
   传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。
   
   好处：提升用户体验
   ```

2. 实现方式：

   - 原生JS实现方式（了解）

   - JQuery实现方式

     - $.ajax()

       ```javascript
       <script>
               function fuc() {
               //使用$.ajax()发送异步请求
                   $.ajax({
                       url:"ajaxServlet", //请求路径
                       type:"post", //请求方式，默认get
                       //data:"username=jack&age", //请求参数
                       data:{"username":"jack","age":23},
                       success:function (data) {
                       	alert(data)
                       },//响应成功后的回调函数
                       error:function () {
                           alert("出错了...")
                       },//表示如果请求响应出现错误，会执行的回调函数
                       dataType:"text",//设置接收到的数据的格式
                   });
               }
           </script>
       ```

     - $.get()：发送get请求

       ```
       * 语法：$.get(url, [data], [callback], [type])
       	* 参数：
       		* url：请求路径
       		* data：请求参数
       		* callback：回调函数
       		* type：响应结果的类型
       ```

     - $.post()：发送post请求

        ```
        * 语法：$.post(url, [data], [callback], [type])
        	* 参数：
              	* url：请求路径
              	* data：请求参数
              	* callback：回调函数
              	* type：响应结果的类型
        ```

## JSON

1. 概念：JavaScript Object Notation		JavaScript对象表示法
   * json现在**多用于存储和交换文本信息的语法**
   * 进行数据的传输
   * JSON 比 XML 更小、更快，更易解析。
   
2. 基本规则
   * 数据在名称/值对中：json数据是由键值对构成的
   * 键用引号(单双都行)引起来，也可以不使用引号
   ```
   值得取值类型：
   1. 数字（整数或浮点数）
   2. 字符串（在双引号中）
   3. 逻辑值（true 或 false）
   4. 数组（在方括号中）{"persons":[{},{}]}
   5. 对象（在花括号中） {"address":{"province"："陕西"....}}
   6. null
   ```
   * 数据由逗号分隔：多个键值对由逗号分隔
   * 花括号保存对象：使用{ }定义 json 格式
   * 方括号保存数组：[]
   
3. 获取数据

   - json对象.键名

   - json对象["键名"]

   - 数组对象[索引]

   - 遍历

     ```javascript
     <script>
             var person = {"name":"张三",age:23,'gender':true};
             var ps = [{"name": "张三", "age": 23, "gender": true},
                 {"name": "李四", "age": 24, "gender": true},
                 {"name": "王五", "age": 25, "gender": false}];
     
             for (var key in person){
                 //alert(key + ":" + person.name);
                 alert(key + ":" + person[key])
             }
     
             for (var i = 0; i< ps.length;i++){
                 var p = ps[i];
                 for (var key in p){
                     alert(key + ":" + p[key]);
                 }
             }
         </script>
     ```

3. JSON数据和Java对象的相互转换

   - 常见的JSON解析器：Jsonlib，Gson，fastjson，jackson
   
   - JSON转换为Java对象
   
     ```
     使用步骤：
         * 导入jackson的相关jar包
         * 创建Jackson核心对象 ObjectMapper
         * 调用ObjectMapper的相关方法进行转换
         	* readValue(json字符串数据，Class)
     ```
   
   - Java对象转换JSON
   
     ```
     使用步骤：
     	* 导入jackson的相关jar包
         * 创建Jackson核心对象 ObjectMapper
         * 调用ObjectMapper的相关方法进行转换
     ```
   
   - 转换方法
   
     ```
     * writeValue(参数1，obj):
     	参数1：
     	    File：将obj对象转换为JSON字符串，并保存到指定的文件中
     	    Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
     	    OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中
     * writeValueAsString(obj):将对象转为json字符串
     ```
   
   - 注解
   
     - @JsonIgnore：排除属性。
     - @JsonFormat：属性值得格式化
       - @JsonFormat(pattern = "yyyy-MM-dd")
   
   - 复杂java对象转换
   
     - List：数组
     - Map：对象格式一致
   
   