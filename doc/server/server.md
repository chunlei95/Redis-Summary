# redis server 相关命令
## [dbsize](http://www.redis.cn/commands/dbsize.html)
  获取当前数据库里面key的数量
## [info](http://www.redis.cn/commands/info.html)
#### 命令格式
  info [section]
#### 说明
  返回关于Redis服务器的各种信息和统计数值。
  通过给定可选的参数 section ，可以让命令只返回某一部分的信息:
  server: Redis服务器的一般信息
  clients: 客户端的连接部分
  memory: 内存消耗相关信息
  persistence: RDB和AOF相关信息
  stats: 一般统计
  replication: 主/从复制信息
  cpu: 统计CPU的消耗
  commandstats: Redis命令统计
  cluster: Redis集群信息
  keyspace: 数据库的相关统计
  它也可以采取以下值:
  all: 返回所有信息
  default: 值返回默认设置的信息
  如果没有使用任何参数时，默认为default, default相当于all
## [time](http://www.redis.cn/commands/time.html)
  返回当前Unix时间戳和这一秒已经过去的微秒数。基本上，该接口非常相似gettimeofday.返回内容包含两个元素:UNIX时间戳（单位：秒）、微秒
## [role](http://www.redis.cn/commands/role.html)
  获取当前redis实例的角色，如果角色为master或者slave, 还会返回复制状态的额外信息, 如果角色为sentinel, 则会返回监控主名称列表
#### 返回值
  返回以下三个字符串中的一个：
    “master”
    “slave”
    “sentinel”
## [flushdb](http://www.redis.cn/commands/flushdb.html)
  删除当前数据库里面的所有数据。这个命令永远不会出现失败。这个操作的时间复杂度是O(N),N是当前数据库的keys数量
## [flushall](http://www.redis.cn/commands/flushall.html)
  删除所有数据库里面的所有数据，注意不是当前数据库，而是所有数据库。这个命令永远不会出现失败。这个操作的时间复杂度是O(N),N是数据库的数量
