# redis事务处理
## [multi](http://www.redis.cn/commands/multi.html)
#### 命令格式
    multi
#### 说明
    标记一个事务块的开始。 随后的指令将在执行EXEC时作为一个原子执行
#### 返回值
    总是返回OK
## [exec](http://www.redis.cn/commands/exec.html)
#### 命令格式
    exec
#### 说明
    执行事务中所有在排队等待的指令并将链接状态恢复到正常 当使用watch时，只有当被监视的键没有被修改，且
    允许检查设定机制时，exec会被执行
## [discard](http://www.redis.cn/commands/discard.html)
#### 命令格式
    discard
#### 说明
    刷新一个事务中所有在排队等待的指令，并且将连接状态恢复到正常。如果已使用watch，discard将释放所有被
    watch的key
#### 返回值
    总是返回OK
## [watch](http://www.redis.cn/commands/watch.html)
#### 命令格式
    watch <key> [key ...]
#### 说明
    标记所有指定的key 被监视起来，在事务中有条件的执行(乐观锁)
#### 返回值
    总是返回OK
## [unwatch](http://www.redis.cn/commands/unwatch.html)
#### 命令格式
    unwatch
#### 说明
    刷新一个事务中已被监视的所有key。如果执行exec 或者discard， 则不需要手动执行unwatch
#### 返回值
    总是返回OK
## [redis事务处理](http://www.redis.cn/topics/transactions.html)
