#Redis

Redis一个键值储存系统，也就是我们说得NOSQL数据库。

##优点
数据保存在硬盘上，读取快；占用更小的内存；当然还有和其他数据库一样的特性，像集群，数据库复制等。

##安装
```shell
$ wGET http://download.redis.io/releases/redis-3.0.4.tar.gz
$ tar xzf redis-3.0.4.tar.gz
$ cd redis-3.0.4
$ make
```
##启动服务
```shell
$ src/redis-server
```

##运行
```shell
$ src/redis-cli
redis> SET foo bar
OK
redis> GET foo
"bar"
```

##使用
###基本操作
`SET Key Value #设置键和值`

`SET floor 10`

`GET Key #获得键的值`

`GET floor => 10`

`INCR Value #值自动加一`

`INCR floor => 11`

`DEL Value #删除键`

`DEL floor`

`EXPIRE Key Seconds #设置键在多少秒后自动销毁`

```
SET resource "Demo"
EXPIRE resource 120
```

`TTL Key #显示键在多少秒后销毁`

```
TTL resource => 120
TTL resource => -2 #-2代表键已销毁
```

`TTL Key=> -1 # -1代表这个键没有设置自动销毁`

###List操作

```
RPUSH friends "Lily" #在list尾增加值
RPUSH friends "Lucy"
LPUSH friends "Alan" #在list首增加值

LRANGE friends 0 -1 => 1) "Alan", 2) "Lily", 3) "Lucy" #显示所有值
LRANGE friends 0 1 => 1) "Alan", 2) "Lily"
LRANGE friends 1 2 => 1) "Lily", 2) "Lucy"

LLEN friends => 3 #显示值个数
LPOP friends => "Alan" #移除第一个值
RPOP friends => "Lucy" #移除最后一个值
```
###Set操作
>于List的不同之处在于他没有固定的顺序和他的值可能只出现一次

```
SADD friends "Alan"
SADD friends "Lucy"
SADD friends "Lily"

SMEMBERS friends => 1) "Lily" 2) "Lucy"` 3) "Alan" #显示所有的值

SREM friends "Alan" #在set中删除这个值

SISMEMBER friends "Lucy" => 1 #1代表set中存在该值
SISMEMBER friends "Alan" => 0 #0代表set中不存在该值

SADD enemy "Jack"
SADD enemy "Zed"
SUNION friends enemy => 1) "Jack" 2) "Lucy" 3) "Lily" 4) "Zed"

SADD runner 1009 "Alan"
SADD runner 1000 "Jack"
SADD runner 1003 "Hoan"

ZRANGE runner 1 2 => 1) "Hoan" 2) "Alan" #在Redit1.2中增加了set得排序功能
```
###Hash操作
```
HSET user:1000 name "Jack"
HSET user:1000 address "Beijing chaoyang"

HMSET user:1000 name "Jack" address "Beijing chaoyang" #以上这两种键值设置方法都可以

HGET user:1000 name => "Jack" #得到键的值
HGETALL user:1000 => 1) "name" 2) "Jack" 3) "address" 4) "Beijing chaoyang"

HSET user:1000 visits 100
HINCRBY user:1000 visits 1 => 101 #HASH值的增加
HINCRBY user:1000 visits 100 => 201
HDEL user:1000
```
