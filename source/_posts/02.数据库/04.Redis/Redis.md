---
title: Redis笔记
comments: true
tags: Redis
categories:
  - 02.数据库
  - 04.Redis
date: 2017-09-05 16:57:27
---
## 1 键值对

- SET TESTKEY "TESTVALUE",设置键值对TESTKEY-"TESTVALUE"，返回OK；
- GET TESTKEY,获取键TESTKEY的值（获取不存在的键的值返回nil，即空）；
- DEL TESTKEY,删除键为TESTKEY的键值对，成功返回1；
- EXISTS TESTKEY,键是否存在，0否1是
- TYPE TESTKEY,返回键的类型，如string、list等，若键不存在返回None;
- INCR TESTKEY,自动加一，成功返回结果（若TESTKEY不是int值，则报错）
    `注意：INCR命令是原子操作（即不会被线程调度机制打断的操作）`;
- SETNX TEST1 'TESTVALUE'，若键不存在则设置，若键存在则不设置，成功返回1，失败返回0；
- EXPIRE TESTKEY 120,设置键TESTKEY有效期120秒（等同于 SET TESTKEY 'TESTVALUE' EX 120）；
- PERSIST TESTKEY,取消TESTKEY的有效期，1成功0失败
- TTL TESTKEY,查看键TESTKEY剩余有效期,-2表示键已过期不存在，-1表示永不过期，若重下SET TESTKEY，则状态重置为-1;

<!--more-->

## 2 数据结构

### 2.1 列表（list）有序、可重复

- RPUSH TESTLIST "ITEM1" "ITEM2" "ITEM3" ... "ITEMN",插入多项到列表尾部，返回列表子项个数；
- LPUSH TESTLIST "ITEM2",插入一项到列表头部，返回列表子项个数；
- LRANGE TESTLIST 0 -1,列出列表子项，参数1表示从第0个开始，参数2表示到第N个（-1表示最后）；
- LLEN TESTLIST,获取列表子项个数；
- LPOP TESTLIST,移除列表头部项，返回项的值；
- RPOP TESTLIST,移除列表尾部项，返回项的值；
- 工具命令BRPOP TESTLIST 0、BLPOP，阻塞版本的取元素，若LIST为空，仅在规定时间（0代表永久）内有新元素加入时候取出，而不是返回NULL；
    - 客户端按顺序执行，第一个取得先等其他客户端加入元素，以此类推；
    - 与RPOP相比，返回值是不同的：它是一个两元素数组，因为它也包括键的名称，因为BRPOP和BLPOP能够阻止等待来自多个列表的元素。
    - 如果超时，则返回NULL。
    - RPOPLPUSH更适合命令创建安全的队列，BRPOPLPUSH阻塞版本
- LTRIM TESTLIST 0 2，只保留前3项，丢弃之后的元素；

### 2.2 集合（set）无序、不可重复

- SADD TESTSET "ITEM1" "ITEM2" "ITEM3" ... "ITEMN",插入一项到集合中，返回1表示成功，若已有该项则返回0；
- SREM TESTSET "ITEM1",从集合中移除指定项，返回1表示成功，若无该项则返回0；
- SISMEMBER TESTSET "ITEM1"，验证指定项是否在集合中，0否1是；
- SMEMBERS TESTSET，列出集合项
- SUNION TESTSET1 TEST2 ... TESTN,取多个集合并集（无序无重复项）；
- SINTER TESTSET1 TEST2 ... TESTN,取多个集合交集
- SUNIONSTORE TESTSETALL TESTSET1 TESTSET2 ...TESTSETN,将多个集合并集保存至TESTSETALL
- SCARD TESETSET1，获取集合元素个数
- SPOP TESTSET1，随机取一个集合元素，移除集合
- SRANDMEMBER TESTSET1，随机取一个集合元素，不移除集合

### 2.3 有序集合（sorted set）有序、不可重复

- ZADD TESTSORTSET 3 "C",3为关联值，用于排序，float；
- ZRANGE TESTSORTLIST 0 -1 [withscores],列出有序集合子项，参数1表示从第0个开始，参数2表示到第N个（-1表示最后）,[withscores]可选，是否列出score项；
- ZREVRANGE TESTSORTLIST 0，-1,反向列出有序集合元素；
- ZRANK TESTSORTLIST 'C',查找指定元素的位置；
- ZREVRANK TESTSORTLIST 'C',反向查找指定元素的位置；

### 2.4 哈希（Hashes）用于保存对象

- HSET obj name 'venux';HSET obj age '27';HSET obj email '337225164@qq.com',保存一个obj对象，单个属性存放用户名、年龄、email。
- HMSET obj name 'venux' age '27' email '337225164@qq.com',保存一个obj对象，多个属性存放用户名、年龄、email。
- HGETALL obj,获取obj对象
- HGET obj name,获取obj对象的name属性
- HINCRBY obj age 10,给obj对象的age属性加10，Hash字段中数值类型使用同等的字符串表示，并能通过`HINCRBY`（原子操作）累加

## 3 Redis支持的数据结构

1. Binary-safe strings；
2. Lists:按插入顺序排序的列表，基于链表；
3. Sets:无序、唯一的集合；
4. Sorted sets:有序、唯一的有序集合，用一个称为scroe的float字段存放排序值；
5. Hashes:一系列属性合集，即对象，字段名和值都为strings；
6. Bit arrays (or simply bitmaps):二进制数组；
7. HyperLogLogs:this is a probabilistic data structure which is used in order to estimate the cardinality of a set（概率性数据结构，用于评估集合的基数）.

## 4 Redis keys

- 空字符串也是有效的key值；
- 太长的key不好，若key代表的对象本身过长，使用hash（如SHA1）后的值作为key值；
- 太短的key值也不好，如使用user:1000:followers替代u1000flw，这样可读性更良好；
- 尽量（坚持）使用模式，一个良好的模式`object-type:id`，通常使用`:`、`-`、`.`分割。例如`user:1000`、`comment:1234:reply.to`、`comment:1234:reply-to`；
- 键最大容量为512MB。

## 5 Redis Strings

- 键值都为string类型，和`Memcached`一样，string作为唯一的数据类型；
- 值也可用于保存图片资源，只要格式本质是string（如二进制），且大小不能超出512M；
- SET命令选项：SET TESTKEY "TESTVALUE" nx/xx,nx代表如果键已存在，则SET失败；反之xx表示，如果键已存在则成功；
- INCR TESTKEY：将string作为int值累加一并保存新值，DECR减； INCRBY TESTKEY 10：加10，DECRBY减； （其实是同一个底层命令不同表示方式）；
- GETSET：先获取旧值后设置新值（有点儿像`i++`）；
- MSET A 10 B 20 C 30;MGET A B C;MSET或MGET（返回一个Array）同时操作多个键值对ABC；

## 6 Redis expires（有效期）

1. 精度可以说秒或毫秒；
2. 本质上精度都是毫秒；
3. 当Redis server停止时，过期的数据也会保存到磁盘中，Redis只是给key加了个有效期的属性；

## 7 Redis Lists

### 7.1 注意区分链表（Linked Lists）和数组（Array）。

- Redis Lists本质是链表，在存储上不连续，优点插入时间复杂度为常量即O(1)，缺点索引查找O(n)。
- 数组指一系列元素的集合，在存储上是连续的，优点索引查找时间复杂度为常量即O(1)，缺点插入O(n)。

### 7.2 适用场景

1. 记录社交网络最后一个提交更新；
2. 消息队列等；

## 8 Bitmaps（位图不是一个确切的数据类型）

1. SETBIT BITKEY 10 1，设置BITKEY键的值的第10位为1；
2. GETBIT BITKEY 10，获取BITKEY键的值的第10位；

### 8.1 适用场景

1. 任何实时分析情况；
2. 高效高性能存储boolean信息，通过各位0或1直接判断各种状态；

## 9 HyperLogLogs(估算各类分布概率)

1. PFADD HLLTEST a b c d；插入元素；
2. PFCOUNT HLLTEST；查询个数

### 9.1 适用场景

1. 例如统计每天用户查询不同关键词的数目

## 参考
1 [redis入门](http://try.redis.io/)
2 [介绍Redis数据结构和抽象](https://redis.io/topics/data-types-intro)