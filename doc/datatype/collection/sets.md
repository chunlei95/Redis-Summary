# redis操作Set
## [sadd](http://www.redis.cn/commands/sadd.html)
#### 命令格式
    sadd <key> <member> [member ...]
#### 说明
    添加一个或多个指定的member元素到集合的 key中.指定的一个或者多个元素member 如果已经在集合key中存在则忽略.
    如果集合key 不存在，则新建集合key,并添加member元素到集合key中.如果key 的类型不是集合则返回错误
#### 返回值
    返回新成功添加到集合里元素的数量，不包括已经存在于集合中的元素.
## [scard](http://www.redis.cn/commands/scard.html)
#### 命令格式
    scard <key>
#### 说明
    获取key对应的集合中元素的数量, 如果key对应的不是一个set集合，则返回错误
#### 返回值
    集合的基数(元素的数量),如果key不存在,则返回 0
## [sdiff](http://www.redis.cn/commands/sdiff.html)
#### 命令格式
    sdiff <key1> <key2> [key3 ...]
#### 说明
    获取一个集合与给定集合之间的差集
#### 返回值
    差集的元素
## [sdiffstore](http://www.redis.cn/commands/sdiffstore.html)
#### 命令格式
    sdiffstore <destination> <key1> [key2 ...]
#### 说明
    该命令类似于 sdiff, 不同之处在于该命令不返回结果集，而是将结果存放在destination集合中.
    如果destination已经存在, 则将其覆盖
#### 返回值
    结果集元素的个数
## [sinter](http://www.redis.cn/commands/sinter.html)
#### 命令格式
    sinter <key1> [key2 ...]
#### 说明
    获取所有指定集合的交集，如果key对应的集合不存在则被认为是一个空的集合
#### 返回值
    结果集成员列表
## [sinterstore](http://www.redis.cn/commands/sinterstore.html)
#### 命令格式
    sinterstore <destination> <key1> [key2 ...]
#### 说明
    这个命令与sinter命令类似, 但是它并不是直接返回结果集,而是将结果保存在 destination集合中.
    如果destination 集合存在, 则会被覆盖
#### 返回值
    结果集中成员的个数
## [sismember](http://www.redis.cn/commands/sismember.html)
#### 命令格式
    sismember <key> <member>
#### 说明
    判断member是否是key对应的集合中的元素
#### 返回值
    如果是，返回值为1，如果不是或者key对应的集合不存在，返回值为0
## [smembers](http://www.redis.cn/commands/smembers.html)
#### 命令格式
    smembers <key>
#### 说明
    获取key对应的集合中的所有元素
#### 返回值
    集合中的所有元素
## [smove](http://www.redis.cn/commands/smove.html)
#### 命令格式
    smove <source> <destination> <member>
#### 说明
    将member从source集合移动到destination集合中. 如果source 集合不存在或者不包含指定的元素,smove命令不执行
    任何操作并且返回0.否则对象将会从source集合中移除，并添加到destination集合中去，如果destination集合已经
    存在该元素，则smove命令仅将该元素从source集合中移除. 如果source 和destination不是集合类型,则返回错误
#### 返回值
    如果该元素成功移除,返回1，如果该元素不是 source集合成员,无任何操作,则返回0
##  [spop](http://www.redis.cn/commands/spop.html)
#### 命令格式
    spop <key> [count]
#### 说明
    随机移除key对应的集合中count个数量的元素, 如果没有指定count，则默认随机移除key对应的集合中的其中一个元素,
    如果count大于key对应的集合中的元素的数量，则表示全部移除, 入宫count小于0，则返回错误, count为0不执行任何
    操作
#### 返回值
    被移除的元素, 如果key对应的集合不存在，则返回nil
## [srandmember](http://www.redis.cn/commands/srandmember.html)
#### 命令格式
    srandmember <key> [count]
#### 说明
    如果count是整数且小于元素的个数，返回含有 count 个不同的元素的数组,如果count是整数且大于集合中元素的个数时,
    返回集合的所有元素,当count是负数,则会返回一个包含count的绝对值的个数元素的数组，如果count的绝对值大于元素的
    个数,则返回的结果集里会出现一个元素出现多次的情况, 如果不指定count，则随机返回一个key对应的集合中的元素
#### 返回值
    不指定count 参数的情况下返回随机的一个元素,如果key不存在则返回nil，指定count参数时,返回一个随机的元素数组,
    如果key不存在则返回一个空的数组
## [srem](http://www.redis.cn/commands/srem.html)
#### 命令格式
    srem <key> <member> [member ...]
#### 说明
    移除key对应的集合中指定的元素. 如果指定的元素不是key集合中的元素则忽略，如果key集合不存在则被视为一个空的集
    合，该命令返回0.如果key对应的不是一个集合,则返回错误
#### 返回值
    从集合中移除元素的个数，不包括不存在的成员
## [sscan](http://www.redis.cn/commands/sscan.html)
## [sunion](http://www.redis.cn/commands/sunion.html)
#### 命令格式
    sunion <key> [key ...]
#### 说明
    获取指定集合的并集，如果key对应的集合不存在则被认为是空的集合
#### 返回值
    并集的成员列表
## [sunionstore](http://www.redis.cn/commands/sunionstore.html)
#### 命令格式
    sunionstore <destination> <key> [key ...]
#### 说明
    该命令作用类似于sunion命令,不同的是它并不返回结果集,而是将结果存储在destination集合中.如果destination 
    已经存在,则将其覆盖
#### 返回值
    结果集中元素的个数
    