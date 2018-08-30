# Redis操作String类型数据
## append
### 命令格式
    append <key> <value>
### 说明
    如果 key 已经存在，并且值为字符串，那么这个命令会把 value 追加到原来值（value）的结尾。 如果 key 不存在，那么它将首先创建key，再执行追加
    操作
### 返回值
    返回append后字符串的长度(追加前和追加后的长度和)
## set
### 命令格式
    set <key> <value> [EX seconds] [PX milliseconds] [NX|XX]
    选项：
        EX seconds: 设置键key的过期时间, 单位是秒
        PX milliseconds: 设置键key的过期时间, 单位是毫秒
        NX: 只有键key不存在的时候才设置key的值
        XX: 只有键key存在的时候才设置key的值
### 说明
    将键key设定为指定的“字符串”值。如果 key 已经保存了一个值，那么这个操作会直接覆盖原来的值，并且忽略原始类型。当set命令执行成功之后，之前设置
    的过期时间都将失效
### 返回值
    如果SET命令正常执行会返回`OK`，否则如果加了`NX` 或者 `XX`选项，但是没有设置条件。那么会返回`nil`
## mset
### 命令格式
    mset <key1> <value1> [key2 value2 ...]
### 说明
    对应给定的keys到他们相应的values上。MSET会用新的value替换已经存在的value，就像普通的SET命令一样。如果你不想覆盖已经存在的values，可以使
    用`MSETNX`, `mset`是原子的，所以所有给定的keys是一次性set的。客户端不可能看到这种一部分keys被更新而另外的没有改变的情况
### 返回值
    总是OK，因为`mset`不会失败
## setbit
### 命令格式
    setbit <key> <offset> <value>
### 说明
        设置或者清空key的value(字符串)在offset处的bit值。对应位置的bit要么被设置，要么被清空，这个由value（只能是0或者1）来决定。当key不存在的
    时候，就创建一个新的字符串value, 要确保这个字符串在offset处有bit值。参数offset需要大于等于0，并且小于232(限制bitmap大小为512)。当key
    对应的字符串增大的时候，新增的部分bit值都是设置为0
### 返回值
    在offset处原来的bit值
## setex
### 命令格式
    setex <key> <seconds> <value>
### 说明
    设置key对应字符串value，并且设置key在给定的seconds时间之后超时过期。这个命令等效于执行下面的命令：
    ```
    set <key> <value>
    expire <key> <seconds>
    ```
    `setex`是原子的，也可以通过把上面两个命令放到MULTI/EXEC块中执行的方式重现。相比连续执行上面两个命令，它更快，因为当Redis当做缓存使用时，
    这个操作更加常用
### 返回值
    返回字符串`OK`
## setnx
### 命令格式
    setnx <key> <value>
### 说明
    将key设置值为value，如果key不存在，这种情况下等同`set`命令。 当key存在时，什么也不做。`setnx`是”set if not exist”的简写
### 返回值
    特定值：
        × 1 如果key对应的值被设置了
        × 0 如果key对应的值没有被设置
## msetnx
### 命令格式
    msetnx <key> <value> [key value ...]
### 说明
    对应给定的keys到他们相应的values上。只要有一个key已经存在，`msetnx`一个操作都不会执行。 由于这种特性，`msetnx`可以实现要么所有的操作都
    成功，要么一个都不执行，这样可以用来设置不同的key，来表示一个唯一的对象的不同字段。`msetnx`是原子的，所以所有给定的keys是一次性set的。客
    户端不可能看到这种一部分keys被更新而另外的没有改变的情况
### 返回值
    只有以下两种值
        × 1 如果所有的key对应的值都被set
        × 0 如果没有key对应的值被set(说明至少其中有一个key是存在的)
## psetex
### 命令格式
    psetex <key> <milliseconds> <value>
### 说明
    `psetex`和`setex`命令格式与作用一样, 只不过`psetex`设置的过期时间以毫秒为单位
## setrange
### 命令格式
    setrange <key> <offset> <offsetvalue>
### 说明
        这个命令的作用是覆盖key对应的string的一部分，从指定的offset处开始，覆盖长度为offsetvalue的长度。如果offset比当前key对应string还
    要长，那这个string后面就补0以达到offset。不存在的keys被认为是空字符串，所以这个命令可以确保key有一个足够大的字符串，能在offset处设置value
    
    注意，offset最大可以是229-1(536870911),因为redis字符串限制在512M大小。如果你需要超过这个大小，你可以用多个keys
### 返回值
    该命令修改后的字符串长度
## get
### 命令格式
    get <key>
### 说明
    返回key的value。如果key不存在，返回特殊值nil。如果key的value不是string，就返回错误，因为GET只处理string类型的values
### 返回值
    key对应的value，或者nil(key不存在时)
## mget
### 命令格式
    mget <key> [key ...]
### 说明
    返回所有指定的key的value。对于每个不对应string或者不存在的key，都返回特殊值nil。正因为此，这个操作从来不会失败
### 返回值
    指定的key对应的values的list
## getbit
### 命令格式
    getbit <key> <offset>
### 说明
    返回key对应的string在offset处的bit值 当offset超出了字符串长度的时候，这个字符串就被假定为由0比特填充的连续空间。当key不存在的时候，它就
    认为是一个空字符串，所以offset总是超出范围，然后value也被认为是由0比特填充的连续空间
### 返回值
    在offset处的bit值(要么是1, 要么是0)
## getrange
### 命令格式
    getrange <key> <start> <end>
### 说明
    这个命令是被改成`getrange`的，在小于2.0的Redis版本中叫`substr`。 返回key对应的字符串value的子串，这个子串是由start和end位移决定的
    （两者都在string内）。可以用负的位移来表示从string尾部开始数的下标。所以-1就是最后一个字符，-2就是倒数第二个，以此类推。
    
    这个函数处理超出范围的请求时，都把结果限制在string内
    
### 返回值
    start到end之间的字符串
## getset
### 命令格式
    getset <key> <value>
### 说明
    自动将key对应到value并且返回原来key对应的value。如果key存在但是对应的value不是字符串，就返回错误
    `getset`可以和`incr`一起使用实现支持重置的计数功能
### 返回值
    返回之前的旧值，如果之前Key不存在将返回`nil`
## incr
### 命令格式
    incr key
### 说明
    对存储在指定key的数值执行原子的加1操作。
    
    如果指定的key不存在，那么在执行incr操作之前，会先将它的值设定为0。
    
    如果指定的key中存储的值不是字符串类型或者存储的字符串类型不能表示为一个整数，那么执行这个命令时服务器会返回一个错误(eq:(error) ERR value 
    is not an integer or out of range)。
    
    这个操作仅限于64位的有符号整型数据。
    
    注意: 
        * 由于redis并没有一个明确的类型来表示整型数据，所以这个操作是一个字符串操作。
        × 执行这个操作的时候，key对应存储的字符串被解析为10进制的64位有符号整型数据。
        × 事实上，Redis 内部采用整数形式来存储对应的整数值，所以对该类字符串值实际上是用整数保存，也就不存在存储整数的字符串表示所带来的额外消耗
### 返回值
    执行递增操作后key对应的值
## incrby
### 命令格式
    incrby <key> <increment>
### 说明
        将key对应的数字加decrement。如果key不存在，操作之前，key就会被置为0。如果key的value类型错误或者是个不能表示成数字的字符串，就返回错
    误。这个操作最多支持64位有符号的正型数字
### 返回值
     增加之后的value值
## incrbyfloat
### 命令格式
    incrbyfloat <key> <increment>
### 说明
    通过指定浮点数key来增长浮点数(存放于string中)的值. 当键不存在时,先将其值设为0再操作.下面任一情况都会返回错误:
    
        key 包含非法值(不是一个string).
        当前的key或者相加后的值不能解析为一个双精度的浮点值.(超出精度范围了)
    
    如果操作命令成功, 相加后的值将替换原值存储在对应的键值上, 并以string的类型返回.
### 返回值
    当前key增加increment后的值
## decr
### 命令格式
    decr <key>
### 说明
        对key对应的数字做减1操作。如果key不存在，那么在操作之前，这个key对应的值会被置为0。如果key有一个错误类型的value或者是一个不能表示成数
    字的字符串，就返回错误。这个操作最大支持在64位有符号的整型数字
### 返回值
    减小之后的value
## decrby
### 命令格式
    decrby <key> <decrement>
### 说明
        将key对应的数字减decrement。如果key不存在，操作之前，key就会被置为0。如果key的value类型错误或者是个不能表示成数字的字符串，就返回错
    误。这个操作最多支持64位有符号的正型数字
### 返回值
    减少之后的value值
## bitcount
### 命令格式
    bitcount key [start end]
### 说明
    统计字符串被设置为1的bit数.
    
    一般情况下，给定的整个字符串都会被进行计数，通过指定额外的 start 或 end 参数，可以让计数只在特定的位上进行。
    
    start 和 end 参数的设置都可以使用负数值：比如 -1 表示最后一个位，而 -2 表示倒数第二个位，以此类推。
    
    不存在的 key 被当成是空字符串来处理，因此对一个不存在的 key 进行`bitcount`操作，结果为 0
### 返回值
    被设置为 1 的位的数量
## bitfield
## bitop
## bitpos