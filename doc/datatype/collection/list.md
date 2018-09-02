# redis操作List(其实就是一个队列)
## rpush
#### 命令格式
    rpush <key> <value> [value value ...]
#### 说明
    向列表尾部插入所有指定的值，如果key对应的列表不存在，那么会创建一个空的列表再进行push操作，当key对应的不是一个列表，那么会返回一个错误，
#### 返回值
    push操作后列表的长度
## rpushx
#### 命令格式
    rpushx <key> <value>
#### 说明
    将value插入到key对应的列表的尾部(前提是key对应的列表存在)，当key对应的列表不存在时，什么事情也不做    
#### 返回值
    *rpushx*命令执行之后列表的长度
## lpush
#### 命令格式
    lpush <key> <value> [value value ...]
#### 说明
    将所有指定的值插入到key对应的列表的头部，如果key对一个的列表不存在，则会创建一个新的列表再进行push操作，如果key对应的不是一个列表，
    则会返回一个错误
#### 返回值
    lpush命令执行后列表的长度
## lpushx
#### 命令格式
    lpushx <key> <value>
#### 说明
    将value插入到key对应的列表的头部，如果key对应的列表不存在，则什么事情也不做
#### 返回值
    执行lpushx命令后列表的长度, 如果key对应的列表不存在，返回值为0
## llen
#### 命令格式
    llen <key>
#### 说明
    获取key对应的列表的长度，如果key对应的列表不存在，则视为一个空列表，返回0，如果key对应的不是一个列表，则返回一个错误
#### 返回值
    key对应的列表中元素的个数，key不存在则返回0    
## lindex
#### 命令格式
    lindex <key> <index>
#### 说明
    获取key对应的列表中索引为index处的值，如果key对应的不是一个列表，则返回一个错误，索引是从0开始的，负数索引表示从列表尾部开始索引
#### 返回值
    key对应的列表中索引为index处的值，如果index超出key对应的列表的长度，则返回nil
## linsert
#### 命令格式
    linsert <key> <before|after> <pivot> <value>
#### 说明
    将value插入到key对应的列表中基准值为pivot的元素的前面或者后面，当key不存在时会被看做一个空列表，任何操作都不会发生，
    当key对应的不是一个列表的时候，会返回一个错误, 当基准值pivot不存在是，什么都不做
#### 返回值
    执行插入操作后的列表的长度，当 pivot 值不存在的时候返回 -1
## lrange
#### 命令格式
    lrange <key> <start> <stop>
#### 说明
    获取key对应的列表中指定范围内的元素，start和stop都是从0开始的，也可以是负数，负数表示从列表尾部开始，start和stop对应
    的元素都会包含在返回值当中当下标超过list范围的时候不会产生error。 如果start比list的尾部下标大的时候，会返回一个空列表。 
    如果stop比list的实际尾部大的时候，Redis会当它是最后一个元素的下标
#### 返回值
    指定范围里的列表元素
## lpop
#### 命令格式
    lpop <key>
#### 说明
    移除并返回key对应列表的第一个元素
#### 返回值
    返回列表中第一个元素的值，当key对应的列表不存在时返回nil
## rpop
#### 命令格式
    rpop <key>
#### 说明
    移除并返回key对应列表的最后一个元素
#### 返回值
    返回列表中最后一个元素的值，当key对应的列表不存在时返回nil
## rpoplpush
#### 命令格式
    rpoplpush <source> <destination>
#### 说明
    原子性地返回并移除存储在 source 的列表的最后一个元素（列表尾部元素）， 并把该元素放入存储在 destination 的列表的
    第一个元素位置（列表头部）,如果 source 不存在，那么会返回 nil 值，并且不会执行任何操作。 如果 source 和 destination 
    是同样的，那么这个操作等同于移除列表最后一个元素并且把该元素放在列表头部， 所以这个命令也可以当作是一个旋转列表的命令
#### 返回值
    被移除和放入的元素
## lset
#### 命令格式
    lset <key> <index> <value>
#### 说明
    设置key对应的列表中index处的值为value，当index超出范围时会返回错误
#### 返回值
    字符串 OK，index超出范围时会返回错误
## ltrim
#### 命令格式
    ltrim <key> <start> <stop>
#### 说明
    裁剪一个列表，start和stop都是从0开始，可以为负数，负数表示从列表尾部开始，超过范围的下标并不会产生错误：如果 start 
    超过列表尾部，或者 start > end，结果会是列表变成空表（即该 key 会被移除）。 如果 end 超过列表尾部，Redis 会将其
    当作列表的最后一个元素(该命令相当于删除操作)
#### 返回值
    字符串 OK
## lrem
#### 命令格式
    lrem <key> <count> <value>
#### 说明
    从存于 key 的列表里移除前 count 次出现的值为 value 的元素。 这个 count 参数通过下面几种方式影响这个操作：
    
    count > 0: 从头往尾移除值为 value 的元素。
    count < 0: 从尾往头移除值为 value 的元素。
    count = 0: 移除所有值为 value 的元素。
    比如， LREM list -2 “hello” 会从存于 list 的列表里移除最后两个出现的 “hello”。
    
    需要注意的是，如果list里没有存在key就会被当作空list处理，所以当 key 不存在的时候，这个命令会返回 0
#### 返回值
    被移除的元素个数
## [blpop](http://www.redis.cn/commands/blpop.html)
 
## [brpop](http://www.redis.cn/commands/brpop.html)
 
## [brpoplpush](http://www.redis.cn/commands/brpoplpush.html)
 
    

    
    
