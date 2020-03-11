---
title: Redis
date: 2019-08-06 15:49:13
categories: Java
---

## Redis 数据结构

redis存储的是：key,value格式的数据，其中key都是字符串，value有5种不同的数据结构

1. 字符串类型 string
2. 哈希类型 hash ： map格式  
3. 列表类型 list ： linkedlist格式。**支持重复元素**
4. 集合类型 set  ：**不允许重复元素**
5. 有序集合类型 sortedset：**不允许重复元素，且元素有顺序**

### 字符串String 

1. 存储：set key value
2. 获取： get key
3. 删除： del key

### 哈希类型 hash

1. 存储： hset key field value
2. 获取： hget key field：获取指定的field对应的值
   - hgetall key ：获取所有的field和value
3. 删除： hdel key field

### 列表类型 list

1. 添加：可以添加一个元素到列表的头部（左边）或者尾部（右边）
   - lpush key value：将元素加入列表左边
   - rpush key value：将元素加入列表右边
2. 获取：lrange key start end：范围获取
3. 删除：
   - lpop key：删除列表最左边的一个元素，并将元素返回
   - rpop key：删除列表最右边的一个元素，并将元素返回

### 集合类型 set

1. 存储：sadd key value
2. 获取：smembers key:获取set集合中所有元素
3. 删除：srem key value:删除set集合中的某个元素

### 有序集合类型 sortedset

1. 存储：zadd key score value
2. 获取：zrange key start end [withscores]
3. 删除：zrem key value

## 通用命令

1. keys * : 查询所有的键
2. type key ： 获取键对应的value的类型
3. del key：删除指定的key value

## 持久化

1. redis是一个内存数据库，当redis服务器重启，获取电脑重启，数据会丢失，我们可以将redis内存中的数据持久化保存到硬盘的文件中。

2. redis持久化机制：

   - RDB：

     ```
     * 默认方式，不需要进行配置，默认就使用这种机制
     * 在一定的间隔时间中，检测key的变化情况，然后持久化数据
     1.编辑redis.windows.conf 文件
     	# after 900 sec (15 min) if at least 1 key changed
     	save 900 1
     	# after 300 sec (5 min) if at least 10 keys changed
     	save 300 10
     	# after 60 sec if at least 10000 keys changed
     	save 60 10000
     2.重新启动redis服务器，并指定配置文件名称
     	* redis目录下打开cmd，输入redis-server.exe redis.windows.conf
     ```

   - AOF：

     ```
     * 日志记录的方式，可以记录每一条命令的操作。可以每一次命令操作后，持久化数据
     1.编辑redis.windows.conf 文件
     	appendonly no(关闭aof)--->appendonly yes (打开aof)
     	# appendfsync always ： 每一次操作都进行持久化
     	appendfsync everysec ： 每隔一秒进行一次持久化
     	# appendfsync no	 ： 不进行持久化
     2.重新启动redis服务器，并指定配置文件名称
     	* redis目录下打开cmd，输入redis-server.exe redis.windows.conf
     ```

## Jedis

1. Jedis: 一款java操作redis数据库的工具

2. 使用步骤：

   - 下载jedis的jar包
   - 使用

   ```java
   //1.获取连接
   Jedis jedis = new Jedis("localhost",6379);
   //2.操作
   jedis.set("username","zhangsan");
   //3.关闭连接
   jedis.close();
   ```

3. Jedis中的方法与各种数据结构的操作名字一致

### Jedis 连接池

1. 使用
   - 创建JedisPool连接池对象
   - 调用方法 getResource()方法获取Jedis连接

---

---

## 面试相关

1. 为什么Redis能这么快？

   100000+QPS（QPS，每秒内查询的次数）

   - 完全基于内存，绝大部分请求是纯粹的内存操作，执行下率高
   - 数据结构简单，对数据操作也简单
   - 采用单线程

2. 多路I/O复用模型

   - FD：File Description，文件描述符

     一个打开的文件通过唯一的描述符进行引用，该描述符是打开文件的元数据到文件本身的的映射

   - Select系统调用

     ![批注 2019-08-09 110044](https://wx3.sinaimg.cn/large/80ceacb8ly1g5tako0hg9j2098074aa3.jpg)

3. **从海量key里查询出某一固定前缀的Key**

   - **摸清数据规模，即问清楚边界**
   - **KEYS pattern：查找所有符合给定模式pattern的key**
     - KEYS指令一次性返回所有匹配的key
     - 键的数量过大会使服务卡顿
   - **SCAN cursor [MATCH pattern] [COUNT count]**
     - 基于游标的迭代器（cursor），需要基于上一次的游标延续之前的迭代过程
     - 以0作为游标开始一次新的迭代，直到命令返回游标0完成一次遍历
     - 不保证每次执行都返回某个给定数量的元素，支持模糊查询
     - 一次返回的数量不可控，只能是大概率符合count参数
   - **使用封装的相关jar包，如jedis，里面的方法进行查询**

4. 如何通过Redis实现分布式锁

   分布式锁需要解决的问题

   - 互斥性
   - 安全性
   - 死锁
   - 容错

   **SETNX key value：如果key不存在，则创建并赋值**

   - 时间复杂度：O(1)
   - 返回值：设置成功，返回1；设置失败，返回0

   **如何解决SETNX长期有效的问题**

   **EXPIRE key seconds**

   - 设置key的生存时间，当key过期时（生存时间为0），会被自动删除
   - **缺点：原子性得不到满足**

   **SET key value [Ex seconds] [PX milliseconds] [NX|XX]**

   - Ex seconds：设置键的过期时间（秒）
   - PX milliseconds：设置键的过期时间（毫秒）
   - NX：只在键不存在时，才对建进行设置操作
   - XX：只在键已经存在时，才对键进行设置操作
   - SET操作成功完成时，返回OK，否则返回nil

   **大量的key同时过期的注意事项**

   解放方案：在设置key的过期时间的时候，给key加上随机值

5. 如何使用Redis做异步队列

   **使用List作为队列，RPUSH生产消息，LPOP消费消息**

   - 缺点：没有等待队列里有值就直接消费
   - 弥补：可以通过在应用层引入Sleep机制去调用LPOP重试
   
   **BLPOP key [key...] timeout：阻塞直到队列有消息或者超时**
   
   - 缺点：只能供一个消费者消费
   
   **pub/sub：主题订阅者模式**
   
   - 订阅者（pub）发送消息，订阅者（sub）接受消息
   - 订阅者可以订阅任意数量的频道（Topic）
   - 缺点：消费的发布是无状态的，无法保证可达
   
6. 使用Pipeline的好处
   
   - 批量执行指令，节省多次IO往返的时间
   
   - 有顺序依赖的指令建议分批发送
   
7. **Redis的同步机制**
   
   主从同步原理
   
   **全同步过程**
   
   - Salve发送sync命令道Master
   - Master启动一个后台进程，将Redis中的数据快照保存到文件中
   - Master将保存数据快照期间接收到的写命令缓存起来
   - Master完成写文件操作后，将该文件发送给Salve
   - 使用新的AOF文件替换掉就的AOF文件
   - Master将这期间收集的增量写命令发送给Salve端
   
   **增量同步过程**
   
   - Master接收到用户的操作指令，判断是否需要传播到Slave
   - 将操作记录追加到AOF文件
   - 将操作传播到其他Salve：
     1. 对齐主从库
     2. 往响应缓冲写入指令
   - 将缓存中的数据发送给Salve
   
8. Redis的集群原理
   
   - 分片：按照某种规则去划分数据，分散存储在多个节点上
   
   - 常规的按照哈希划分无法实现节点的动态增减
   
     - 一致性哈希算法：对2^32取模，将哈希值空间组织成虚拟的圆环
   
     - 将数据key使用相同的函数Hash计算出Hash值
   
   - 引入虚拟节点解决数据倾斜的问题
   
   
   
   
   
   

