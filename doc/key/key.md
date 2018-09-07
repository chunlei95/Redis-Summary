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
## [keys](http://www.redis.cn/commands/keys.html)
#### 命令格式
    keys <pattern>
#### 说明
    查询所有符合正则表达式pattern的key。(可能会出现阻塞服务器的问题)
#### 返回值
    所有符合条件的key
## [type](http://www.redis.cn/commands/type.html)
#### 命令格式
    type <key>
#### 说明
    获取key存储的value的数据结构类型
#### 返回值
    返回key存储的value的数据结构类型，如果key不存在，则返回none
## [rename](http://www.redis.cn/commands/rename.html)
#### 命令格式
    rename <key> <newkey>
#### 说明
    将key重命名为newkey，如果key与newkey相同，将返回一个错误。如果newkey已经存在，则值将被覆盖
## [renamenx](http://www.redis.cn/commands/renamenx.html)
#### 命令格式
    renamenx <key> <newkey>
#### 说明
    当且仅当 newkey 不存在时，将 key 改名为 newkey 。当 key 不存在时，返回一个错误
#### 返回值
    修改成功返回1，如果newkey已经存在则返回0
## [randomkey](http://www.redis.cn/commands/randomkey.html)
#### 说明
    从当前数据库返回一个随机的key，如果数据库没有任何key，返回nil，否则返回一个随机的key
## [scan](http://www.redis.cn/commands/scan.html)
## [move](http://www.redis.cn/commands/move.html)
#### 命令格式
    move <key> <db>
#### 说明
    将当前数据库的 key 移动到给定的数据库 db 当中。如果当前数据库(源数据库)和给定数据库(目标数据库)
    有相同名字的给定 key ，或者 key 不存在于当前数据库，那么 MOVE 没有任何效果
#### 返回值
    移动成功返回1，失败则返回0
