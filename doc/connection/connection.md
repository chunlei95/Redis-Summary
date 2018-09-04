# redis connection 命令
## [ping](http://www.redis.cn/commands/ping.html)
#### 命令格式
    ping [message]
#### 说明
    如果后面没有message参数时返回pong，否则会返回后面带的message参数。这个命令经常用来测试一个连接是否还是可用的，
    或者用来测试一个连接的延时
## [echo](http://www.redis.cn/commands/echo.html)
#### 命令格式
    echo <message>
#### 说明
    返回消息，消息内容为message
## [select](http://www.redis.cn/commands/select.html)
#### 命令格式
    select <index>
#### 说明
    选择数据库，默认连接的数据库为db0
## [auth](http://www.redis.cn/commands/auth.html)
#### 命令格式
    auth <password>
#### 说明
    为redis服务请求设置一个密码。redis可以设置在客户端执行commands请求前需要通过密码验证。通过修改配置文件的requirepass
    就可以设置密码。 如果密码与配置文件里面设置的密码一致，服务端就会发会一个OK的状态码，接受客户端发送其他的请求命令，否则服
    务端会返回一个错误码，客户端需要尝试使用新的密码来进行连接
#### 补充
    config get requirepass  获取当前密码
    config set requirepass <password> 设置当前服务密码
    该方式在服务重启后又会设置为默认，即无密码
    另一个设置密码的方式就是修改配置文件redis.conf里面的requirepass一项，永久修改
## [quit](http://www.redis.cn/commands/quit.html)
#### 命令格式
    quit
#### 说明
    请求服务器关闭连接。连接将会尽可能快的将未完成的客户端请求完成处理
#### 返回值
    始终返回OK