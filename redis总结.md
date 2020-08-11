# redis总结

## Nosql简介

> NoSQL(NoSQL = Not Only SQL )，意即“不仅仅是SQL”, 泛指非关系型的数据库
>
> Nosql(13年-15)这个技术门类,早期就有人提出,发展至2009年趋势越发高涨。
>
> RDBMS  关系型数据库管理系统  mysql  oracle  sql
>
> NOSQL  不仅仅是sql 泛指 非关系型数据库  redis mongo hbase

+ 为什么会出现Nosql技术
> 11 淘宝  京东   12306 全年每天并发  mysql oracle 磁盘 票  29限时抢购 秒杀  排行榜  Nosql redis随着互联网web2.0(3.0)(web.xml 2.5 3.0)网站的兴起，传统的关系数据库在应付web2.0网站，特别是超大规模和高并发的web2.0纯动态网站已经显得力不从心，暴露了很多难以克服的问题。微信(朋友圈文字,朋友圈图片 朋友圈 小视频)如图片(Blob CLob)，音频，视频传统的关系型数据库只能存储结构化数据，对于非结构化的数据支持不够完善，nosql这个技术门类的出现，更好的解决了这些问题，它告诉了世界不仅仅是sql。
### Nosql的分类

#### 键值(Key-Value)存储数据库

+ 性能较高  限时  秒杀  排行榜

> ​    这一类数据库主要会使用到一个哈希表，这个表中有一个特定的键和一个指针指向特定的数据。
>
> ​	Key/value模型对于IT系统来说的优势在于简单、易部署。  
>
> ​	但是如果DBA只对部分值进行查询或更新的时候，Key/value就显得效率低下了。
>
> ​	举例如：Tokyo Cabinet/Tyrant, Redis(基于内存)(SSDB(基于硬盘) key-value), Voldemort, 
>
> ​    Oracle BDB. SSDB 磁盘 性能不差于redis   Redis 基于内存
+ 适用场景
> 1、数据模型比较简单；  key  value  mongo 复杂数据
	2、需要灵活性更强的IT系统；nosql  效率高  
	3、对数据库性能要求较高；   nosql
	4、不需要高度的数据一致性； nosql  事务 原子性
#### 列存储数据库

+ 大数据  Hadoop  RouteKey 列 对应大量数据
> 这部分数据库通常是用来应对分布式存储的海量数据。
	键仍然存在，但是它们的特点是指向了多个列。这些列是由列家族来安排的。
	如：Cassandra, HBase( routeKey 设计key), Riak.

#### 文档型数据库

+ JSON {key:value}事务替代关系型数据库  引擎内存
> 文档型数据库的灵感是来自于Lotus Notes办公软件的，而且它同第一种键值存储相类似该类型的数据模型是版本化的文档，半结构化的文档以特定的格式存储，比如JSON。文档型数据库可 以看作是键值数据库的升级版，允许之间嵌套键值。而且文档型数据库比键值数据库的查询效率更高。
	如：CouchDB, MongoDb(4.x). 国内也有文档型数据库SequoiaDB，已经开源。

#### 图形(Graph)数据库

+  (图片 音频 视频) 文件服务器
> 图形结构的数据库同其他行列以及刚性结构的SQL数据库不同，它是使用灵活的图形模型，并且能够扩展到多个服务器上。
	NoSQL数据库没有标准的查询语言(SQL)，因此进行数据库查询需要制定数据模型。许多NoSQL数据库都有REST式的数据接口或者查询API。
	如：Neo4J, InfoGrid, Infinite Graph.


## redis简介

### 什么是redis

> Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker.
>
> Redis 开源  遵循BSD  基于内存数据存储 被用于作为 数据库 缓存  消息中间件
>
> Redis 是一个开源的,遵循BSD许可,基于内存的,键值对型的Nosql型数据库
>
> 总结:	redis是一个内存型的数据库  redis数据都是在内存  ===>持久化到硬盘

### redis的特点

>  Redis是一个高性能key/value内存型数据库  key value
>
>  Redis支持丰富的数据类型如(String,list,set,zset,hash) value得类型
>
>  Redis支持持久化  内存中数据持久化到硬盘  数据库特性
>
> Redis单线程,单进程 慢(不支持并发  并发时多个线程串行) 分布式锁

### redis与memcahed

> 共同点
>
> 无论是Memcahed还是Redis底层都是使用C语言编写,都是基于key-value(键值对存储) 内存存储
>
>  不同点
>
> Memcahed支持的数据类型,比较简单(String,Object) 字符串 对象
>
>  Redis支持的数据类型比较丰富(String,List,set,zset,hash) string list set zset hash 
>
> Memcahed默认一个值的最大存储不能超过1M value
>
> Redis一个值的最大存储1G key  value
>
>  Memcahed中存储的数据不能持久化,一旦断电,立即丢失 key value
>
> Redis中存储的数据可以持久化
>
>  Memcahed 多线程,支持并发访问 数据安全 大量锁线程锁
>
> Redis 单线程,并发时串行执行,将单进程单线程效率发挥到最大  
>
>  Memcahced自身不支持集群环境 (使用中间件)
>
> Redis从3.0版本之后自身开始提供集群环境支持(集群环境)

## redis的安装与配置

#### 安装redis

```shell
[root@VM_0_9_centos ~]# wget http://download.redis.io/releases/redis-5.0.8.tar.gz
[root@VM_0_9_centos ~]# tar -zxvf redis-5.0.8.tar.gz
[root@VM_0_9_centos ~]# yum install -y gcc
[root@VM_0_9_centos ~]# make            //如果出现致命错误 make MALLOC=libc
[root@VM_0_9_centos ~]# make install PREFIX=/usr/local/redis          //指定安装目录
[root@VM_0_9_centos ~]# cd /usr/local/redis/bin
[root@VM_0_9_centos bin]# ./redis-service                     //启动服务
[root@VM_0_9_centos bin]# ./redis-cli -p 6379 -h 127.0.0.1       //启动客户端

```

#### 配置redis.conf

```shell
[root@VM_0_9_centos ~]# cd /usr/local/redis/
[root@VM_0_9_centos redis]# vim redis.conf 

 daemonize no      //Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程
 port 6379        //端口号
 timeout 300      //当连接闲置多久后断开连接  0表示关闭
 databases 16    //指定数据库
 
 //分别表示900秒（15分钟）内有1个更改，300秒（5分钟）内有10个更改以及60秒内有10000个更改。
 save 900 1
 save 300 10
 save 60 10000
 
 //数据库文件名
 dbfilename dump.rdb
 
 //设置密码
 requirepass root
 
 //开启远程访问
 bind 127.0.01  注释掉 
 
 [root@VM_0_9_centos bin]# ./redis-service ../redis.conf   带着配置文件开启redis
 [root@VM_0_9_centos redis]# ps aux|grep redis
root     11757  0.0  0.1 141904  2256 ?        Ssl  15:59   0:14 ./redis-server *:1996
root     23708  0.0  0.1 126404  1964 pts/0    S+   21:54   0:00 vi redis.conf
root     24981  0.0  0.0 112708   976 pts/1    R+   22:28   0:00 grep --color=auto redis
```



## redis常用命令

### 操作数据库命令

```markdown
	说明 :  使用redis的默认配置器动redis服务后,默认会存在16个库,编号从0-15
	可以使用select 库的编号 来选择一个redis的库

	1.清空当前的库   FLUSHDB
	2.清空全部的库   FLUSHALL
```



### 操作key的命令

##### DEL

```markdown
	语法 :  DEL key [key ...] 
	作用 :  删除给定的一个或多个key 。不存在的key 会被忽略。
	可用版本： >= 1.0.0
	时间复杂度：
	O(N)，N 为被删除的key 的数量。	
	删除单个字符串类型的key ，时间复杂度为O(1)。
	删除单个列表、集合、有序集合或哈希表类型的key ，时间复杂度为O(M)，M为以上数据结构内的元素数量。
	返回值： 被删除key 的数量。
```

##### EXISIS

```markdown
	语法:  EXISTS key
	作用:  检查给定key 是否存在。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值： 若key 存在，返回1 ，否则返回0 。
```

##### EXPIRE

```markdown
	语法:  EXPIRE key seconds
	作用:  为给定key 设置生存时间，当key 过期时(生存时间为0 )，它会被自动删除。
	在Redis 中，带有生存时间的key 被称为『易失的』(volatile)。生存时间可以通过使用DEL 命令来删除整个key 来移		除，或者被SET 和GETSET 命令覆写(overwrite)，
	这意味着，如果一个命令只是修改(alter) 一个带生存时间的key 的值而不是用一个新的key 值来代替(replace) 它的	 话，那么生存时间不会被改变。
	比如说，对一个key 执行INCR 命令，对一个列表进行LPUSH 命令，或者对一个哈希表执行HSET 命令，这类操作都不会修		改key 本身的生存时间。
	另一方面，如果使用RENAME 对一个key 进行改名，那么改名后的key 的生存时间和改名前一样。RENAME 命令的另一种可	能是，尝试将一个带生存时间的key 改名成另一个带生存时间的another_key这时旧的another_key (以及它的生存时间) 	会被删除，然后旧的key 会改名为another_key ，因此，新的another_key 的生存时间也和原本的key 一样。使用		PERSIST 命令可以在不删除key 的情况下，移除key 的生存时间，让key 重新成为一个『持久的』(persistent) key 。	   更新生存时间可以对一个已经带有生存时间的key 执行EXPIRE 命令，新指定的生存时间会取代旧的生存时间。过期时间的精	   确度在Redis 2.4 版本中，过期时间的延迟在1 秒钟之内——也即是，就算key 已经过期，但它还是可能在过期之后一秒钟	 之内被访问到，而在新的Redis 2.6 版本中，延迟被降低到1 毫秒之内。Redis 2.1.3 之前的不同之处
	在Redis 2.1.3 之前的版本中，修改一个带有生存时间的key 会导致整个key 被删除，这一行为是受当时复制			(replication) 层的限制而作出的，现在这一限制已经被修复。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值：设置成功返回1 。
```

##### KEYS

```markdown
	语法 :  KEYS pattern
	作用 :  查找所有符合给定模式pattern 的key 。
	KEYS * 匹配数据库中所有key 。
	KEYS h?llo 匹配hello ，hallo 和hxllo 等。
	KEYS h*llo 匹配hllo 和heeeeello 等。
	KEYS h[ae]llo 匹配hello 和hallo ，但不匹配hillo 。
	特殊符号用 \ 隔开
	注意:  KEYS 的速度非常快，但在一个大的数据库中使用它仍然可能造成性能问题，如果你需要从一个数据集中查找特定的	  key ，你最好还是用Redis 的集合结构(set) 来代替。
	可用版本： >= 1.0.0
	时间复杂度： O(N)，N 为数据库中key 的数量。
	返回值： 符合给定模式的key 列表。
```

##### MOVE

```markdown
	语法 :  MOVE key db
	作用 :  将当前数据库的key 移动到给定的数据库db 当中。
	如果当前数据库(源数据库) 和给定数据库(目标数据库) 有相同名字的给定key ，或者key 不存在于当前数据库，那么		MOVE 没有任何效果。因此，也可以利用这一特性，将MOVE 当作锁(locking) 原语(primitive)。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值： 移动成功返回1 ，失败则返回0 。
```



##### PEXPIRE

```markdown
	语法 :  PEXPIRE key milliseconds
	作用 :  这个命令和EXPIRE 命令的作用类似，但是它以毫秒为单位设置key 的生存时间，而不像EXPIRE 命令那样，以秒	为单位。
	可用版本： >= 2.6.0
	时间复杂度： O(1)
	返回值：设置成功，返回1  key 不存在或设置失败，返回0
```



##### PEXPIREAT

```markdown
	语法 :  PEXPIREAT key milliseconds-timestamp
	作用 :  这个命令和EXPIREAT 命令类似，但它以毫秒为单位设置key 的过期unix 时间戳，而不是像EXPIREAT那样，以秒	为单位。
	可用版本： >= 2.6.0
	时间复杂度： O(1)
	返回值：如果生存时间设置成功，返回1 。当key 不存在或没办法设置生存时间时，返回0 。(查看EXPIRE 命令获取更多信	  息)
```



##### TTL

```markdown
	语法 :   TTL key
	作用 :   以秒为单位，返回给定key 的剩余生存时间(TTL, time to live)。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值：
	当key 不存在时，返回-2 。
	当key 存在但没有设置剩余生存时间时，返回-1 。
	否则，以秒为单位，返回key 的剩余生存时间。
	Note : 在Redis 2.8 以前，当key 不存在，或者key 没有设置剩余生存时间时，命令都返回-1 。
```



##### PTTL

```markdown
	语法 :  PTTL key
	作用 :  这个命令类似于TTL 命令，但它以毫秒为单位返回key 的剩余生存时间，而不是像TTL 命令那样，以秒为单位。
	可用版本： >= 2.6.0
	复杂度： O(1)
	返回值： 当key 不存在时，返回-2 。当key 存在但没有设置剩余生存时间时，返回-1 。
	否则，以毫秒为单位，返回key 的剩余生存时间。
	注意 : 在Redis 2.8 以前，当key 不存在，或者key 没有设置剩余生存时间时，命令都返回-1 。
```



##### RANDOMKEY

```markdown
	语法 :  RANDOMKEY
	作用 :  从当前数据库中随机返回(不删除) 一个key 。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值：当数据库不为空时，返回一个key 。当数据库为空时，返回nil 。
```



##### RENAME

```markdown
	语法 :  RENAME key newkey
	作用 :  将key 改名为newkey 。当key 和newkey 相同，或者key 不存在时，返回一个错误。当newkey 已经存在时，	  RENAME 命令将覆盖旧值。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值： 改名成功时提示OK ，失败时候返回一个错误。
```



##### TYPE

```markdown
	语法 :  TYPE key
	作用 :  返回key 所储存的值的类型。
	可用版本： >= 1.0.0
	时间复杂度： O(1)
	返回值：
	none (key 不存在)
	string (字符串)
	list (列表)
	set (集合)
	zset (有序集)
	hash (哈希表)
```



### key value数据的类型

#### String类型

|    命令     |                    说明                    | 操作示例 |
| :---------: | :----------------------------------------: | -------- |
|     set     |             设置一个key/value              |          |
|     get     |           根据key获得对应的value           |          |
|    mset     |           一次设置多个key value            |          |
|    mget     |           一次获得多个key的value           |          |
|   getset    |       获得原始key的值，同时设置新值        |          |
|   strlern   |         获得对应key存储value的长度         |          |
|   append    |          为对应key的value追加内容          |          |
|  getrange   |         截取value的内容,索引0开始          |          |
|    setex    |       设置一个key存活的有效期（秒）        |          |
|   psetex    |      设置一个key存活的有效期（毫秒）       |          |
|    setnx    |        存在不做任何操作,不存在添加         |          |
|   msetnx    | 可以同时设置多个key,只有有一个存在都不保存 |          |
|    decr     |            进行数值类型的-1操作            |          |
|   decrby    |         根据提供的数据进行减法操作         |          |
|    incr     |            进行数值类型的+1操作            |          |
|   incrby    |         根据提供的数据进行加法操作         |          |
| incrbyfloat |          根据提供的数据加入浮点数          |          |

#### List类型

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-14_233908.png)

|     命令     |                 说明                 | 示例 |
| :----------: | :----------------------------------: | :--: |
|    lpush     |    将某个值加入到一个key列表头部     |      |
|    lpushx    |  同lpush,但是必须要保证这个key存在   |      |
|    rpush     |    将某个值加入到一个key列表末尾     |      |
|    rpushx    |  同rpush,但是必须要保证这个key存在   |      |
|     lpop     |      返回和移除列表的第一个元素      |      |
|     rpop     |       返回和移除列表的末尾元素       |      |
| lrange 0 - 1 |      获取某一个下标区间内的元素      |      |
|     llen     |           获取列表元素个数           |      |
|     lset     | 设置某一个指定索引的值(索引必须存在) |      |
|    lindex    |     获取某一个指定索引位置的元素     |      |
|     lrem     |             删除重复元素             |      |
|    ltrim     |      保留列表中特定区间内的元素      |      |
|   linsert    |   在某一个元素之前，之后插入新元素   |      |



#### Set类型

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-15_101625.png)

| 命令        | 说明                                   | 演示 |
| ----------- | -------------------------------------- | ---- |
| sadd        | 为集合添加元素                         |      |
| smembers    | 显示集合中所有元素 无序                |      |
| scard       | 返回集合中元素的个数                   |      |
| spop        | 随机返回一个元素 并将元素在集合中删除  |      |
| smove       | 从一个集合中向另一个集合移动元素       |      |
| srem        | 从集合中删除一个元素                   |      |
| sismember   | 判断一个集合中是否含有这个元素         |      |
| srandmember | 随机返回元素                           |      |
| sdiff       | 去掉第一个集合中其它集合含有的相同元素 |      |
| sinter      | 求交集                                 |      |
| sunion      | 求和集                                 |      |



#### Zset类型

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-15_103057.png)

| 命令          | 说明                         | 演示 |
| ------------- | ---------------------------- | ---- |
| zadd          | 添加一个有序集合元素         |      |
| zcard         | 返回集合的元素个数           |      |
| zrange        | 返回一个范围内的元素 升序    |      |
| zrevrange     | 返回一个范围内的元素 降序    |      |
| zrangebyscore | 按照分数查找一个范围内的元素 |      |
| zrank         | 返回排名                     |      |
| zrevrank      | 倒序排名                     |      |
| zscore        | 显示某一个元素的分数         |      |
| zrem          | 移除某一个元素               |      |
| zincrby       | 给某个特定元素加分           |      |

#### Hash类型

![](C:\Users\Administrator\Desktop\markdown\images\2020-04-15_105142.png)

| 命令         | 说明                    | 示例 |
| ------------ | ----------------------- | ---- |
| hset         | 设置一个key/value对     |      |
| hget         | 获得一个key对应的value  |      |
| hgetall      | 获得所有的key/value对   |      |
| hdel         | 删除某一个key/value对   |      |
| hexists      | 判断一个key是否存在     |      |
| hkeys        | 获得所有的key           |      |
| hvals        | 获得所有的value         |      |
| hmset        | 设置多个key/value       |      |
| hmget        | 获得多个key的value      |      |
| hsetnx       | 设置一个不存在的key的值 |      |
| hincrby      | 为value进行加法运算     |      |
| hincrbyfloat | 为value加入浮点值       |      |



### redis持久化

> redis提供了两种持久化方案，快照和AOF
+ 快照

  ```markdown
  	快照可以将某一时刻的所有数据都写入硬盘中,当然这也是redis的默认持久化方式,保存的文件是以.rdb形式结尾的文件因此这种方式也称之为RDB方式a)
  	快照持久化也是redis中的默认开启的持久化方案, 根据redis.conf中的配置,快照将被写入dbfilename指定的文件里面(默认是dump.rdb文件中)
  	根据redis.conf中的配置,快照将保存在dir选项指定的路径上
  ```

+ 创建快照的方式

  ```markdown
    	客户端可以使用BGSAVE命令来创建一个快照,当接收到客户端的BGSAVE命令时,redis会调用fork¹来创建一个子进程,然后子进程负责将快照写入磁盘中,而父进程则继续处理命令请求
    	客户端还可以使用SAVE命令来创建一个快照,接收到SAVE命令的redis服务器在快照创建完毕之前将不再响应任何其他的命令
    	SAVE命令并不常用,使用SAVE命令在快照创建完毕之前,redis处于阻塞状态,无法对外服务
     	如果用户在redis.conf中设置了save配置选项,redis会在save选项条件满足之后自动触发一次BGSAVE命令,如果设置多个save配置选项,当任意一个save配置选项条件满足,redis也会触发一次BGSAVE命令
     	当redis通过shutdown指令接收到关闭服务器的请求时,会执行一个save命令,阻塞所有的客户端,不再执行客户端执行发送的任何命令,并且在save命令执行完毕之后关闭服务器
  ```

    

+ AOF

  ```markdown
  	AOF可以将所有客户端执行的写命令记录到日志文件中
  	redis的默认配置中AOF持久化机制 是没有开启的,AOF持久化会将被执行的写命令写到AOF的文件末尾,以此来记录数据  发生的变化,因此只要redis从头到尾执行一次AOF文件所包含的所有写命令,就可以恢复AOF文件的记录的数据集.
		开启AOF持久化机制,需要修改redis.conf的配置文件
  	1 通过修改redis.conf配置中appendonly yes来开启AOF持久化
  	2 通过appendfilename指定日志文件名字(默认为:appendonly.aof)
  	3 通过appendfsync指定日志记录频率
  ```
  
+ appendfsync指定日志记录频率
  
    | 选项     | 同步频率                                          |
    | -------- | ------------------------------------------------- |
    | always   | 每个redis写命令都要同步写入硬盘,严重降低redis速度 |
    | everysec | 每秒执行一次同步显式的将多个写命令同步到磁盘      |
    | no       | 由操作系统决定何时同步                            |
    
    **三种记录频率的优缺点**
    
    ```markdown
    	Always：如果用户使用了always选项,那么每个redis写命令都会被写入硬盘,从而将发生系统崩溃时出现的数据丢失减到最少;遗憾的是,因为这种同步策略需要对硬盘进行大量的写入操作,所以redis处理命令的速度会受到硬盘性能的限制;
    	
    	注意：转盘式硬盘在这种频率下200左右个命令/s ; 固态硬盘(SSD) 几百万个命令/s;
    	
    	警告：使用SSD用户请谨慎使用always选项,这种模式不断写入少量数据的做法有可能会引发严重的写入放大问题,导致将固态硬盘的寿命从原来的几年降低为几个月
    	
    	Everysec：redis每秒一次的频率对AOF文件进行同步;redis每秒同步一次AOF文件时性能和不使用任何持久化特性时的性能相差无几,而通过每秒同步一次AOF文件,redis可以保证,即使系统崩溃,用户最多丢失一秒之内产生的数据(推荐使用这种方式) 
    	为了兼顾数据安全和写入性能,用户可以考虑使用everysec选项
    	
    	No：将完全有操作系统决定什么时候同步AOF日志文件,这个选项不会对redis性能带来影响但是系统崩溃时,会丢失不定数量的数据,另外如果用户硬盘处理写入操作不够快的话,当缓冲区被等待写入硬盘数据填满时,redis会处于阻塞状态,并导致redis的处理命令请求的速度变慢(不推荐使用)
    ```
    
    

### AOF重写

```markdown
	aof 的方式也同时带来了另一个问题。持久化文件会变的越来越大。例如我们调用incr test命令100次，文件中必须保存全部的100条命令，其实有99条都是多余的。因为要恢复数据库的状态其实文件中保存一条set test 100就够了。为了压缩aof的持久化文件Redis提供了AOF重写机制
	
	重写 aof 文件的两种方式:
	执行BGREWRITEAOF命令  不会阻塞redis的服务
	配置redis.conf中的auto-aof-rewrite-percentage选项
	
	
	BGREWRITEAOF 方式:
	收到此命令redis将使用与快照类似的方式将内存中的数据 以命令的方式保存到临时文件中，最后替换原来的文件。具体过     程如下:
	redis调用fork ，现在有父子两个进程 子进程根据内存中的数据库快照，往临时文件中写入重建数据库状态的命令
	
	父进程继续处理client请求，除了把写命令写入到原来的aof文件中。同时把收到的写命令缓存起来。这样就能保证如果子进程重写失败的话并不会出问题。
	
	当子进程把快照内容写入已命令方式写到临时文件中后，子进程发信号通知父进程。然后父进程把缓存的写命令也写入到临时文件。
	
	现在父进程可以使用临时文件替换老的aof文件，并重命名，后面收到的写命令也开始往新的aof文件中追加。
	
	注意 :  重写aof文件的操作，并没有读取旧的aof文件，而是将整个内存中的数据库内容用命令的方式重写了一个新的aof文件,替换原有的文件这点和快照有点类似。(AOF重写过程完成后会删除旧的AOF文件,删除一个体积达几十GB大的旧的AOF文件可能会导致系统随时挂起 )
	
	
	配置redis.conf中的auto-aof-rewrite-percentage选项:
	AOF重写也可以使用auto-aof-rewrite-percentage 200
	和auto-aof-rewrite-min-size 64mb来自动执行BGREWRITEAOF.

	说明: 如果设置auto-aof-rewrite-percentage值为100和auto-aof-rewrite-min-size 64mb,并且启用的AOF持久化时,那么当AOF文件体积大于64M,并且AOF文件的体积比上一次重写之后体积大了至少一倍(100%)时,会自动触发,如果重写过于频繁,用户可以考虑将auto-aof-rewrite-percentage设置为更大

Aof  64Mb--- 34M----  68M --50M--100M-70M->140M-> 120M--240M 200M---> 400M---10G---->20G
```



### 两种持久化方案总结

```markdown
	AOF持久化既可以将丢失的数据的时间降低到1秒(甚至不丢失任何数据),那么我们还有什么理由不是用AOF呢?
	注意 : 
	这个问题实际上并没有这么简单,因为redis会不断将执行的写命令记录到AOF文件中,所以随着redis运行,AOF文件的体积会不断增大,在极端情况下甚至会用完整个硬盘,还有redis重启重新执行AOF文件记录的所有写命令的来还原数据集,AOF文件体积非常大,会导致redis执行恢复时间过长  
    
	两种持久化方案既可以同时使用(aof),又可以单独使用,在某种情况下也可以都不使用,具体使用那种持久化方案取决于用户的数据和应用决定

	无论使用AOF还是快照机制持久化,将数据持久化到硬盘都是有必要的,除了持久化外,用户还应该对持久化的文件进行备份(最好备份在多个不同地方)
```



### JavaAPI调用redis

+ 连接池

```java
/*
*  工具类
* Redis连接池，其他类下，可以直接[导包]调用
* */

public class RedisPool {
    private static final JedisPool JEDIS_POOL;
    static {
        JedisPoolConfig config = new JedisPoolConfig();
        config.setMaxTotal(100);//设置最大连接数
        config.setMaxIdle(10);  //空闲时连接数
        JEDIS_POOL=new JedisPool(config,"49.234.18.34",6379); //设置连接池
    }
   
/*
    * 获得redis对象
    * */
    public static Jedis getJedis(){
        Jedis jedis=JEDIS_POOL.getResource();   //从连接池中拿到redis
        jedis.auth("root");
        return jedis;
    }
    public static void close(Jedis jedis){
        jedis.close();
    }
}
```

+ 测试

```java
public class RedisDemo {
    public static void main(String[] args) {
        Jedis jedis = RedisPool.getJedis();  //获得连接池
        if(jedis.exists("user")){    //jedis去redis检索key name 是否存在  如果存在就用 get 取出来
            String result = jedis.get("user");
            System.out.println("从redis里查出来的数据:"+result);
        }else {                             //如果没有就去数据库[mysql]查出来，并且把该值放到redis缓存中
            String result="I LOVE YOU";   //假装从MySQL中查出来的数据
            jedis.set("user",result);
            System.out.println("从数据库里查出来的数据为:"+result);
        }
        jedis.close();
    }
}
```

### SpringData集成redis

+ 引入依赖

```xml
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-data-redis</artifactId>
    </dependency>
```

+ 配置文件

```yaml
redis:
    database: 0
    password: root
    pool:
      max-active: 8
      max-idle: 8
      max-wait: -1
      min-idle: 0
    host: 49.234.18.34
    port: 1996
```

#### StringRedisTemplate 和 RedisTemplate 



> 两者的关系是StringRedisTemplate继承RedisTemplate。
> 两者的数据是不共通的；也就是说StringRedisTemplate只能管理StringRedisTemplate里面的数据
> RedisTemplate只能管RedisTemplate中的数据。
> SDR默认采用的序列化策略有两种，一种是String的序列化策略，一种是JDK的序列化策略。
> StringRedisTemplate默认采用的是String的序列化策略，保存的key和value都是采用此策略序列化保存的。
> RedisTemplate默认采用的是JDK的序列化策略，保存的key和value都是采用此策略序列化保存的



#### opsForValue(操作字符串)

```java
 @Resource
    private StringRedisTemplate stringRedisTemplate;

    /**
     * 新增一个字符串类型的值,key是键，value是值。
     *
     * set(K key, V value)
     */
    public void set() {
        // 存入永久数据
        stringRedisTemplate.opsForValue().set("test2", "1");
        // 也可以向redis里存入数据和设置缓存时间
        stringRedisTemplate.opsForValue().set("test1", "hello redis", 1000, TimeUnit.SECONDS);
    }

    /**
     * 批量插入，key值存在会覆盖原值
     *
     * multiSet(Map<? extends K,? extends V> map)
     */
    public void multiSet() {
        Map<String,String> map = new HashMap<>(16);
        map.put("testMultiSet1", "value0");
        map.put("testMultiSet2", "value2");
        stringRedisTemplate.opsForValue().multiSet(map);
    }

    /**
     *  批量插入，如果里面的所有key都不存在，则全部插入，返回true，如果其中一个在redis中已存在，全不插入，返回false
     *
     *  multiSetIfAbsent(Map<? extends K,? extends V> map)
     */
    public void multiSetIfAbsent() {
        Map<String,String> map = new HashMap<>(16);
        map.put("testMultiSet4", "value1");
        map.put("testMultiSet3", "value3");
        Boolean absent = stringRedisTemplate.opsForValue().multiSetIfAbsent(map);
        System.out.println(absent);
    }

    /**
     * 如果不存在则插入，返回true为插入成功,false失败
     *
     * setIfAbsent(K key, V value)
     */
    public void setIfAbsent() {
        Boolean absent = stringRedisTemplate.opsForValue().setIfAbsent("test", "hello redis");
        System.out.println(absent);
    }
    /**
     * 获取值,key不存在返回null
     *
     * get(Object key)
     */
    public void get() {
        System.out.println(stringRedisTemplate.opsForValue().get("testMultiSet1"));
    }

    /**
     * 批量获取，key不存在返回null
     *
     * multiGet(Collection<K> keys)
     */
    public void multiGet() {
        List<String> list = stringRedisTemplate.opsForValue().multiGet(Arrays.asList("test", "test2"));
        assert list != null;
        System.out.println(list.toString());
    }

    /**
     * 获取指定字符串的长度。
     *
     * size(K key)
     */
    public void getLength() {
        Long size = stringRedisTemplate.opsForValue().size("test");
        System.out.println(size);
    }

    /**
     * 在原有的值基础上新增字符串到末尾。
     *
     * append(K key, String value)
     */
    public void append() {
        Integer append = stringRedisTemplate.opsForValue().append("test3", "database");
        System.out.println(append);
    }

    /**
     * 获取原来key键对应的值并重新赋新值
     *
     * getAndSet(K key, V value)
     */
    public void getAndSet() {
        String set = stringRedisTemplate.opsForValue().getAndSet("test", "set test");
        System.out.println(set);
    }

    /**
     * 获取指定key的值进行减1，如果value不是integer类型，会抛异常，如果key不存在会创建一个，默认value为0
     *
     * decrement(k key)
     */
    public void decrement() {
        stringRedisTemplate.opsForValue().decrement("test2");
        stringRedisTemplate.opsForValue().decrement("test1");
    }

    /**
     * 获取指定key的值进行加1，如果value不是integer类型，会抛异常，如果key不存在会创建一个，默认value为0
     * 
     * increment(k key)
     */
    public void increment() {
        stringRedisTemplate.opsForValue().increment("test2");
        stringRedisTemplate.opsForValue().increment("test1");
    }

    /**
     * 删除指定key,成功返回true，否则false
     * 
     * delete(k key)
     */
    public void delete() {
        Boolean delete = stringRedisTemplate.opsForValue().getOperations().delete("test1");
        System.out.println(delete);
    }

    /**
     * 删除多个key，返回删除key的个数
     * 
     * delete(k ...keys)
     */
    public void deleteMulti() {
        Long delete = stringRedisTemplate.opsForValue().getOperations().delete(Arrays.asList("test1", "test2"));
        System.out.println(delete);
    }
}

```

#### opsForList(操作List)

```java
/**
 * @author Gjing
 **/
@Component
public class RedisList {
    @Resource
    private StringRedisTemplate stringRedisTemplate;

    /**
     * 在变量左边添加元素值。如果key不存在会新建，添加成功返回添加后的总个数
     * 
     * leftPush(K key, V value)
     */
    public void leftPush() {
        Long aLong = stringRedisTemplate.opsForList().leftPush("list", "a");
        System.out.println(aLong);
    }

    /**
     * 向左边批量添加参数元素，如果key不存在会新建，添加成功返回添加后的总个数
     * 
     * leftPushAll(K key, V... values)
     */
    public void leftPushAll() {
        Long pushAll = stringRedisTemplate.opsForList().leftPushAll("list", "e", "f", "g");
        System.out.println(pushAll);
    }

    /**
     * 向集合最右边添加元素。如果key不存在会新建，添加成功返回添加后的总个数
     * 
     * rightPush(K key, V value)
     */
    public void rightPush() {
        Long aLong = stringRedisTemplate.opsForList().rightPush("list2", "a");
        System.out.println(aLong);
    }


    /**
     * 如果存在集合则添加元素。
     * 
     * leftPushIfPresent(K key, V value)
     */
    public void leftPushIfPresent() {
        Long aLong = stringRedisTemplate.opsForList().leftPushIfPresent("list", "h");
        System.out.println(aLong);
    }

    /**
     * 向右边批量添加元素。返回当前集合元素总个数
     * 
     * rightPushAll(K key, V... values)
     */
    public void rightPushAll() {
        Long aLong = stringRedisTemplate.opsForList().rightPushAll("list2", "b", "c", "d");
        System.out.println(aLong);
    }

    /**
     * 向已存在的集合中添加元素。返回集合总元素个数
     * 
     * rightPushIfPresent(K key, V value)
     */
    public void rightPushIfPresent() {
        Long aLong = stringRedisTemplate.opsForList().rightPushIfPresent("list", "e");
        System.out.println(aLong);
    }

    /**
     * 获取集合长度
     * 
     * size(K key)
     */
    public void size() {
        Long size = stringRedisTemplate.opsForList().size("list2");
        System.out.println(size);
    }

    /**
     * 移除集合中的左边第一个元素。返回删除的元素，如果元素为空，该集合会自动删除
     * 
     * leftPop(K key)
     */
    public void leftPop() {
        String pop = stringRedisTemplate.opsForList().leftPop("list2");
        System.out.println(pop);
    }

    /**
     * 移除集合中左边的元素在等待的时间里，如果超过等待的时间仍没有元素则退出。
     * 
     * leftPop(K key, long timeout, TimeUnit unit)
     */
    public void leftPopWait() {
        String pop = stringRedisTemplate.opsForList().leftPop("list2", 10, TimeUnit.SECONDS);
        System.out.println(pop);
    }

    /**
     * 移除集合中右边的元素。返回删除的元素，如果元素为空，该集合会自动删除
     * 
     * rightPop(K key)
     */
    public void rightPop() {
        String pop = stringRedisTemplate.opsForList().rightPop("list2");
        System.out.println(pop);
    }

    /**
     * 移除集合中右边的元素在等待的时间里，如果超过等待的时间仍没有元素则退出。
     * 
     * rightPop(K key, long timeout, TimeUnit unit)
     */
    public void rightPopWait() {
        String pop = stringRedisTemplate.opsForList().rightPop("list2", 10, TimeUnit.SECONDS);
        System.out.println(pop);
    }

    /**
     * 移除第一个集合右边的一个元素，插入第二个集合左边插入这个元素
     * 
     * rightPopAndLeftPush(K sourceKey, K destinationKey)
     */
    public void rightPopAndLeftPush() {
        String s = stringRedisTemplate.opsForList().rightPopAndLeftPush("list2", "list3");
        System.out.println(s);
    }

    /**
     * 在集合的指定位置插入元素,如果指定位置已有元素，则覆盖，没有则新增，超过集合下标+n则会报错。
     * 
     * set(K key, long index, V value)
     */
    public void set() {
        stringRedisTemplate.opsForList().set("list2", 2, "w");
    }

    /**
     * 从存储在键中的列表中删除等于值的元素的第一个计数事件。count> 0：删除等于从左到右移动的值的第一个元素；
     * count< 0：删除等于从右到左移动的值的第一个元素；count = 0：删除等于value的所有元素
     * 
     * remove(K key, long count, Object value)
     */
    public void remove() {
        Long remove = stringRedisTemplate.opsForList().remove("list2", 2, "w");
        System.out.println(remove);
    }

    /**
     * 截取集合元素长度，保留长度内的数据。
     * 
     * trim(K key, long start, long end)
     */
    public void trim() {
        stringRedisTemplate.opsForList().trim("list2", 0, 3);
    }

    /**
     * 获取集合指定位置的值。
     * 
     * index(K key, long index)
     */
    public void index() {
        Object listValue = stringRedisTemplate.opsForList().index("list2", 3);
        System.out.println(listValue);
    }

    /**
     * 获取指定区间的值。
     * 
     * range(K key, long start, long end)
     */
    public void range() {
        List<String> list = stringRedisTemplate.opsForList().range("list", 0, -1);
        System.out.println(list);
    }

    /**
     * 删除指定集合,返回true删除成功
     * 
     * delete(K key)
     */
    public void delete() {
        Boolean delete = stringRedisTemplate.opsForList().getOperations().delete("list2");
        System.out.println(delete);
    }
}
```

#### opsForHash(操作hashMap)

```java
@Component
public class RedisHash {
    @Resource
    private StringRedisTemplate stringRedisTemplate;

    /**
     * 新增hashMap值
     * 
     * put(H key, HK hashKey, HV value)
     */
    public void put() {
        stringRedisTemplate.opsForHash().put("hash","hash-key","hash-value");
        stringRedisTemplate.opsForHash().put("hash","hash-key2","hash-value2");
    }

    /**
     * 以map集合的形式添加键值对
     * 
     * putAll(H key, Map<? extends HK,? extends HV> m)
     */
    public void putAll() {
        Map<String, String> map = new HashMap<>(16);
        map.put("hash-key3", "value3");
        map.put("hash-key4", "value4");
        stringRedisTemplate.opsForHash().putAll("hash", map);
    }

    /**
     * 如果变量值存在，在变量中可以添加不存在的的键值对，如果变量不存在，则新增一个变量，同时将键值对添加到该变量。添加成功返回true否则返回false
     * 
     * putIfAbsent(H key, HK hashKey, HV value)
     */
    public void putIfAbsent() {
        Boolean absent = stringRedisTemplate.opsForHash().putIfAbsent("hash", "hash-key", "value1");
        Boolean absent2 = stringRedisTemplate.opsForHash().putIfAbsent("hash", "hash-key5", "value5");
        System.out.println(absent);
        System.out.println(absent2);
    }

    /**
     * 获取指定变量中的hashMap值。
     * 
     * values(H Key)
     */
    public void values() {
        List<Object> values = stringRedisTemplate.opsForHash().values("hash2");
        System.out.println(values.toString());
    }

    /**
     * 获取变量中的键值对。
     * 
     * entries(H key)
     */
    public void entries() {
        Map<Object, Object> entries = stringRedisTemplate.opsForHash().entries("hash");
        System.out.println(entries.toString());
    }

    /**
     * 获取变量中的指定map键是否有值,如果存在该map键则获取值，没有则返回null。
     * 
     * get(H key, Object hashKey)
     */
    public void get() {
        Object value = stringRedisTemplate.opsForHash().get("hash", "hash-key");
        System.out.println(value);
    }

    /**
     * 获取变量中的键。
     * 
     * keys(H key)
     */
    public void keys() {
        Set<Object> keys = stringRedisTemplate.opsForHash().keys("hash");
        System.out.println(keys.toString());
    }

    /**
     *  获取变量的长度
     *  
     *  size(H key)
     */
    public void size() {
        Long size = stringRedisTemplate.opsForHash().size("hash");
        System.out.println(size);
    }

    /**
     * 使变量中的键以long值的大小进行自增长。值必须为Integer类型,否则异常
     * 
     * increment(H key, HK hashKey, long data)
     */
    public void increment() {
        Long increment = stringRedisTemplate.opsForHash().increment("hash", "hash-key2", 1);
        System.out.println(increment);
    }

    /**
     * 以集合的方式获取变量中的值。
     * 
     * multiGet(H key, Collection<HK> hashKeys)
     */
    public void multiGet() {
        List<Object> values = stringRedisTemplate.opsForHash().multiGet("hash", Arrays.asList("hash-key", "hash-key2"));
        System.out.println(values.toString());
    }

    /**
     * 匹配获取键值对，ScanOptions.NONE为获取全部键对，ScanOptions.scanOptions().match("hash-key2").build()匹配获取键位map1的键值对,不能模糊匹配。
     * 
     * scan(H key, ScanOptions options)
     */
    public void scan() {
        Cursor<Map.Entry<Object, Object>> scan = stringRedisTemplate.opsForHash().scan("hash", ScanOptions.NONE);
        while (scan.hasNext()) {
            Map.Entry<Object, Object> next = scan.next();
            System.out.println(next.getKey() + "---->" + next.getValue());
        }
    }

    /**
     * 删除变量中的键值对，可以传入多个参数，删除多个键值对。返回删除成功数量
     * 
     * delete(H key, Object... hashKeys)
     */
    public void delete() {
        Long delete = stringRedisTemplate.opsForHash().delete("hash", "hash-key", "hash-key1");
        System.out.println(delete);
    }

}
```

#### opsForSet(操作set集合)

```java
/**
 * @author Gjing
 *
 * 以下可能有部分方法含有参数传Collection的,本案例没有描述,你们可以根据实际参数类型传参
 **/
@Component
public class RedisSet {
    @Resource
    private StringRedisTemplate stringRedisTemplate;

    /**
     * 向变量中批量添加值。返回添加的数量
     *
     * add(K key, V... values)
     */
    public void add() {
        Long add = stringRedisTemplate.opsForSet().add("set", "a", "b", "c");
        System.out.println(add);
    }

    /**
     * 获取变量的值
     *
     * members(K key)
     */
    public void members() {
        Set<String> set = stringRedisTemplate.opsForSet().members("set");
        System.out.println(set);
    }

    /**
     * 获取变量中值得长度
     *
     * size(k key)
     */
    public void size() {
        Long size = stringRedisTemplate.opsForSet().size("set");
        System.out.println(size);
    }

    /**
     * 随机获取变量中的某个元素
     *
     * randomMember(k key)
     */
    public void randomMember() {
        String member = stringRedisTemplate.opsForSet().randomMember("set");
        System.out.println(member);
    }

    /**
     * 随机获取变量中指定个数的元素
     *
     * randomMembers(k key, long count)
     */
    public void randomMembers() {
        List<String> members = stringRedisTemplate.opsForSet().randomMembers("set", 2);
        System.out.println(members);
    }

    /**
     * 检查给定的元素是否在变量中,true为存在
     *
     * isMember(k key, object value)
     */
    public void isMember() {
        Boolean member = stringRedisTemplate.opsForSet().isMember("set", "b");
        System.out.println(member);
    }

    /**
     * 转义变量的元素值到另一个变量中
     *
     * move(k key, v value, k targetKey)
     */
    public void move() {
        Boolean move = stringRedisTemplate.opsForSet().move("set", "b", "set2");
        System.out.println(move);
    }

    /**
     * 弹出变量中的元素。当元素全部弹完,变量也会删除
     *
     * pop(k key)
     */
    public void pop() {
        String pop = stringRedisTemplate.opsForSet().pop("set");
        System.out.println(pop);
    }

    /**
     * 批量删除变量中的元素,返回删除的数量
     *
     * remove(k key, v ...values)
     */
    public void remove() {
        Long remove = stringRedisTemplate.opsForSet().remove("set2", "b");
        System.out.println(remove);
    }

    /**
     * 匹配获取键值对，ScanOptions.NONE为获取全部键值对；ScanOptions.scanOptions().match("C").build()匹配获取键位map1的键值对,不能模糊匹配。
     *
     * scan(K key, ScanOptions options)
     */
    public void scan() {
        Cursor<String> set = stringRedisTemplate.opsForSet().scan("set", ScanOptions.NONE);
        while (set.hasNext()) {
            String next = set.next();
            System.out.println(next);
        }
    }

    /**
     * 通过集合求差值。
     *
     * difference(k key, k otherKey)
     */
    public void difference() {
        Set<String> difference = stringRedisTemplate.opsForSet().difference("set", "set2");
        System.out.println(difference);
    }

    /**
     * 将求出来的差值元素保存
     *
     * differenceAndStore(K key, K otherKey, K targetKey)
     */
    public void differenceAndStore() {
        Long aLong = stringRedisTemplate.opsForSet().differenceAndStore("set", "set2", "set3");
        System.out.println(aLong);
    }

    /**
     * 获取去重的随机元素
     *
     * distinctRandomMembers(K key, long count)
     */
    public void distinctRandomMembers() {
        Set<String> set = stringRedisTemplate.opsForSet().distinctRandomMembers("set", 2);
        System.out.println(set);
    }

    /**
     * 获取两个变量中的交集
     *
     * intersect(K key, K otherKey)
     */
    public void intersect() {
        Set<String> intersect = stringRedisTemplate.opsForSet().intersect("set", "set2");
        System.out.println(intersect);
    }

    /**
     * 获取2个变量交集后保存到最后一个变量上。
     *
     * intersectAndStore(K key, K otherKey, K targetKey)
     */
    public void intersectAndStore() {
        Long aLong = stringRedisTemplate.opsForSet().intersectAndStore("set", "set2", "set3");
        System.out.println(aLong);
    }

    /**
     * 获取两个变量的合集
     *
     * union(K key, K otherKey)
     */
    public void union() {
        Set<String> union = stringRedisTemplate.opsForSet().union("set", "set2");
        System.out.println(union);
    }

    /**
     * 获取两个变量合集后保存到另一个变量中
     *
     * unionAndStore(K key, K otherKey, K targetKey)
     */
    public void unionAndStore() {
        Long aLong = stringRedisTemplate.opsForSet().unionAndStore("set", "set2", "set3");
        System.out.println(aLong);
    }
}
```

#### opsForZset

```java
/**
 * @author Gjing
 *
 **/
@Component
public class RedisZSet {
    @Resource
    private StringRedisTemplate stringRedisTemplate;

    /**
     * 添加元素到变量中同时指定元素的分值。
     *
     * add(K key, V value, double score)
     */
    public void add() {
        Boolean add = stringRedisTemplate.opsForZSet().add("zset", "a", 1);
        System.out.println(add);
    }

    /**
     * 通过TypedTuple方式新增数据。
     *
     * add(K key, Set<ZSetOperations.TypedTuple<V>> tuples)
     */
    public void addByTypedTuple() {
        ZSetOperations.TypedTuple<String> typedTuple1 = new DefaultTypedTuple<>("E", 2.0);
        ZSetOperations.TypedTuple<String> typedTuple2 = new DefaultTypedTuple<>("F", 3.0);
        ZSetOperations.TypedTuple<String> typedTuple3 = new DefaultTypedTuple<>("G", 5.0);
        Set<ZSetOperations.TypedTuple<String>> typedTupleSet = new HashSet<>();
        typedTupleSet.add(typedTuple1);
        typedTupleSet.add(typedTuple2);
        typedTupleSet.add(typedTuple3);
        Long zset = stringRedisTemplate.opsForZSet().add("zset", typedTupleSet);
        System.out.println(zset);
    }

    /**
     * 获取指定区间的元素
     *
     * range(k key, long start, long end)
     */
    public void range() {
        Set<String> zset = stringRedisTemplate.opsForZSet().range("zset", 0, -1);
        System.out.println(zset);
    }

    /**
     * 用于获取满足非score的排序取值。这个排序只有在有相同分数的情况下才能使用，如果有不同的分数则返回值不确定。
     *
     * rangeByLex(K key, RedisZSetCommands.Range range)
     */
    public void rangeByLex() {
        Set<String> rangeByLex = stringRedisTemplate.opsForZSet().rangeByLex("zset", RedisZSetCommands.Range.range().lt("E"));
        System.out.println(rangeByLex);
    }

    /**
     * 用于获取满足非score的设置下标开始的长度排序取值。
     *
     * rangeByLex(k key, range range, limit limit)
     */
    public void rangeByLexAndLimit() {
        Set<String> zset = stringRedisTemplate.opsForZSet().rangeByLex("zset", RedisZSetCommands.Range.range().lt("E"),
                RedisZSetCommands.Limit.limit().offset(1).count(2));
        System.out.println(zset);
    }

    /**
     * 根据设置的score获取区间值。
     *
     * rangeByScore(K key, double min, double max)
     */
    public void rangeByScore() {
        Set<String> zset = stringRedisTemplate.opsForZSet().rangeByScore("zset", 1, 3);
        System.out.println(zset);
    }

    /**
     * 获取RedisZSetCommands.Tuples的区间值。
     *
     * rangeWithScores(K key, long start, long end)
     */
    public void rangeWithScores() {
        Set<ZSetOperations.TypedTuple<String>> zset = stringRedisTemplate.opsForZSet().rangeWithScores("zset", 1, 3);
        assert zset != null;
        for (ZSetOperations.TypedTuple<String> next : zset) {
            String value = next.getValue();
            Double score = next.getScore();
            System.out.println(value + "-->" + score);
        }
    }

    /**
     * 获取区间值的个数。
     *
     * count(k key, double min, double max)
     */
    public void count() {
        Long zset = stringRedisTemplate.opsForZSet().count("zset", 1, 3);
        System.out.println(zset);
    }

    /**
     * 获取变量中指定元素的索引,下标开始为0
     *
     * rank(k key, object o)
     */
    public void rank() {
        Long rank = stringRedisTemplate.opsForZSet().rank("zset", "a");
        System.out.println(rank);
    }

    /**
     * 匹配获取键值对，ScanOptions.NONE为获取全部键值对；ScanOptions.scanOptions().match("C").build()匹配获取键位map1的键值对,不能模糊匹配。
     *
     * scan(K key, ScanOptions options)
     */
    public void scan() {
        Cursor<ZSetOperations.TypedTuple<String>> zset = stringRedisTemplate.opsForZSet().scan("zset", ScanOptions.NONE);
        while (zset.hasNext()) {
            ZSetOperations.TypedTuple<String> next = zset.next();
            System.out.println(next.getValue() + "-->" + next.getScore());
        }
    }

    /**
     * 获取指定元素的分值
     *
     * score(k key, object o)
     */
    public void score() {
        Double score = stringRedisTemplate.opsForZSet().score("zset", "a");
        System.out.println(score);
    }

    /**
     * 获取变量中元素的个数
     *
     * zCard(k key)
     */
    public void zCard() {
        Long zset = stringRedisTemplate.opsForZSet().zCard("zset");
        System.out.println(zset);
    }

    /**
     * 修改变量中元素的分值
     *
     * incrementScore(K key, V value, double delta)
     */
    public void incrementScore() {
        Double score = stringRedisTemplate.opsForZSet().incrementScore("zset", "a", 2);
        System.out.println(score);
    }

    /**
     * 索引倒序排列指定区间的元素
     *
     * reverseRange(K key, long start, long end)
     */
    public void reverseRange() {
        Set<String> zset = stringRedisTemplate.opsForZSet().reverseRange("zset", 1, 3);
        System.out.println(zset);
    }

    /**
     * 倒序排列指定分值区间的元素
     *
     * reverseRangeByScore(K key, double min, double max)
     */
    public void reverseRangeByScore() {
        Set<String> zset = stringRedisTemplate.opsForZSet().reverseRangeByScore("zset", 1, 3);
        System.out.println(zset);
    }

    /**
     * 倒序排序获取RedisZSetCommands.Tuples的分值区间值
     *
     * reverseRangeByScore(K key, double min, double max, long offset, long count)
     */
    public void reverseRangeByScoreLength() {
        Set<String> zset = stringRedisTemplate.opsForZSet().reverseRangeByScore("zset", 1, 3, 1, 2);
        System.out.println(zset);
    }

    /**
     * 倒序排序获取RedisZSetCommands.Tuples的分值区间值。
     *
     * reverseRangeByScoreWithScores(K key, double min, double max)
     */
    public void reverseRangeByScoreWithScores() {
        Set<ZSetOperations.TypedTuple<String>> zset = stringRedisTemplate.opsForZSet().reverseRangeByScoreWithScores("zset", 1, 5);
        assert zset != null;
        zset.iterator().forEachRemaining(e-> System.out.println(e.getValue() + "--->" + e.getScore()));
    }

    /**
     * 获取倒序排列的索引值
     *
     * reverseRank(k key, object o)
     */
    public void reverseRank() {
        Long aLong = stringRedisTemplate.opsForZSet().reverseRank("zset", "a");
        System.out.println(aLong);
    }

    /**
     * 获取2个变量的交集存放到第3个变量里面。
     *
     * intersectAndStore(K key, K otherKey, K destKey)
     */
    public void intersectAndStore() {
        Long aLong = stringRedisTemplate.opsForZSet().intersectAndStore("zset", "zset2", "zset3");
        System.out.println(aLong);
    }

    /**
     * 获取2个变量的合集存放到第3个变量里面。 返回操作的数量
     *
     * unionAndStore(K key, K otherKey, K destKey)
     */
    public void unionAndStore() {
        Long aLong = stringRedisTemplate.opsForZSet().unionAndStore("zset", "zset2", "zset3");
        System.out.println(aLong);
    }


    /**
     * 批量移除元素根据元素值。返回删除的元素数量
     *
     * remove(K key, Object... values)
     */
    public void remove() {
        Long remove = stringRedisTemplate.opsForZSet().remove("zset", "a", "b");
        System.out.println(remove);
    }

    /**
     * 根据分值移除区间元素。返回删除的数量
     *
     * removeRangeByScore(k key, double min, double max)
     */
    public void removeRangeByScore() {
        Long zset = stringRedisTemplate.opsForZSet().removeRangeByScore("zset", 1, 3);
        System.out.println(zset);
    }

    /**
     * 根据索引值移除区间元素。返回移除的元素集合
     *
     * removeRange(K key, long start, long end)
     */
    public void removeRange() {
        Set<String> zset = stringRedisTemplate.opsForZSet().reverseRange("zset", 0, 4);
        System.out.println(zset);
    }
}
```

#### 序列化

+ RedisTemplate用来处理非字符串的类型，默认使用jdk序列化，但是为了可读性，会对key进行String序列化

```java
 redisTemplate.setKeySerializer(new StringRedisSerializer());//字符串序列化key
 redisTemplate.setHashKeySerializer(new StringRedisSerializer());//字符串序列化value中的key
```




### redis的集群搭建

### 集群节点的操作






