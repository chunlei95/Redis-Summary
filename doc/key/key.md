# redis key 相关命令
## [del](http://www.redis.cn/commands/del.html)
#### 命令格式
    del <key> [key ...]
#### 说明
    删除指定的一批key，如果某些key不存在，则直接忽略
#### 返回值
    被删除的key的数量
## [dump](http://www.redis.cn/commands/dump.html)
#### 命令格式
    dump <key>
#### 说明
    序列化给定 key ，并返回被序列化的值，使用 restore 命令可以将这个值反序列化为 Redis 键。
    序列化生成的值有以下几个特点：
        *它带有 64 位的校验和，用于检测错误，restore 在进行反序列化之前会先检查校验和。
        *值的编码格式和 RDB 文件保持一致。
        *RDB 版本会被编码在序列化值当中，如果因为 Redis 的版本不同造成 RDB 格式不兼容，那么 Redis 会拒绝对这个值进行反序列化操作。
        *序列化的值不包括任何生存时间信息
#### 返回值
    如果 key 不存在，那么返回 nil。否则，返回序列化之后的值
## [exists](http://www.redis.cn/commands/exists.html)
#### 命令格式
    exists <key> [key ...]
#### 说明
    判断key是否存在
#### 返回值
    如果key存在返回1，如果可以不存在返回0