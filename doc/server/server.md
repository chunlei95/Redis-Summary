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
## [client getname](http://www.redis.cn/commands/client-getname.html)
#### 说明
  获取当前连接由 client setname 设置的名字，如果没有设置，将返回一个空的回复
#### 返回值
  返回链接名字或者空(没有设置名字的时候)
## [client setname](http://www.redis.cn/commands/client-setname.html)
#### 命令格式
  client setname <connection-name>
#### 说明
  为当前链接设置一个名称，标示当前连接，一个新创建的连接默认是没有名字的
#### 返回值
  如果设置成功返回OK
## [client list](http://www.redis.cn/commands/client-list.html)
#### 说明
  获取所有连接到服务器的客户端信息和统计数据
## [client kill](http://www.redis.cn/commands/client-kill.html)
#### 命令格式
    CLIENT KILL [ip:port] [ID client-id] [normal|slave|pubsub] [ADDR ip:port] [SKIPME yes/no]
#### 说明
  关闭一个指定的连接
## [client pause](http://www.redis.cn/commands/client-pause.html)
#### 命令格式
  client pause < timeout >
#### 说明
  client pause是一个连接控制命令，能够在指定的时间内（以毫秒为单位）挂起所有Redis客户端
#### 返回值
  返回OK或者错误(如果timeout是无效的)
## [command](http://www.redis.cn/commands/command.html)
  返回redis所有的命令数组
## [command count](http://www.redis.cn/commands/command-count.html)
  返回redis命令的数量
## [command getkeys](http://www.redis.cn/commands/command-getkeys.html)
#### 命令格式
  command getkeys <一条命令>
#### 说明
  从命令中获取命令中存在的所有的key
## [command info](http://www.redis.cn/commands/command-info.html)
#### 命令格式
  command info <command-name> [command-name ...]
#### 说明
  获取命令的详情
  