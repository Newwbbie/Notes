### mysql主从配置用到的sql：
```
-- 主
CREATE USER 'repl'@'192.168.247.129' IDENTIFIED WITH mysql_native_password BY 'Ron_master_2';
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'192.168.247.129';
flush privileges;
SHOW MASTER STATUS;
-- 从
CHANGE MASTER TO
MASTER_HOST='192.168.247.130',
MASTER_USER='repl',
MASTER_PASSWORD='Ron_master_2',
MASTER_LOG_FILE='mysql-bin.000007',
MASTER_LOG_POS=2390;
start slave
show slave status
show variables like 'server_id'
```
---
### mysql 出现2059错误解决方法：
```
-- 进mysql库
ALTER USER 'root'@'%' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
flush privileges;
```
---
### ```auto_increment_offset``` 和 ```auto_increment_increment``` 区别
```
auto_increment_offset表示自增长字段从哪个数开始，指字段一次递增多少，他的取值范围是1 .. 65535
auto_increment_increment表示自增长字段每次递增的量，指自增字段的起始值，其默认值是1，取值范围是1 .. 65535
为了避免两台服务器同时做更新时自增长字段的值之间发生冲突。一般在主主同步配置时，需要将两台服务器的auto_increment_increment增长量都配置为2，
auto_increment_offset分别配置为1和2。
```
---
### MySQL互为主从配置：（Linux在/etc/my.cnf；Windows在安装根目录）
```
# 日志
log-bin=mysql-bin
# 控制logbin的刷新
sync_binlog = 1
# 混合复制
binlog_format=mixed
server-id = 2
# 要同步的库
binlog-do-db=qwer
# 忽视的库
binlog-ignore-db=mysql
# 不做校验，节省空间
binlog_checksum = none
# master=1, slave=2
auto-increment-offset = 1
# 每次自增的量
auto-increment-increment = 2
# 跳过错误
slave-skip-errors = all
```