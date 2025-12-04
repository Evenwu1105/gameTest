```mysql
delimiter $$ 修改sql结束符号，使得遇到之后结束

drop procedure if exits 存储过程名;
delimiter $$
create procedure 存储过程名(参数名 数据类型(长度),参数名 数据类型)
begin
	sql语句;
end $$
delimiter ;
#变量定义
declare i int;
#赋值
set i = 10;
declare x int default 0;

#select语句只能返回一条记录
```
>[!NOTE] if条件语句用法
```mysql
if 条件1 then 
	条件1为真时执行的sql语句;
elseif 条件2 then
	1为假,条件2为真时执行的sql语句
Else
	以上条件都为假执行的sql语句;
end if;
```
>[!note] while循环语句用法

```mysql
while 关于变量的条件判断 do
	条件为真则执行循环，为假则跳出循环
end while;
```

例:
```mysql
delimiter $$
create procedure add_user(yhm char(20),startNo int,stopNo int,mm char(20))
begin
	declare i int default startNo;
	while i<=stopNo do
		insert into ecs_users(email,user_name,password,alias,msn,qq,office_phone,home_phone,mobile_phone,credit_line)
			values(concat(yhm,'_',i,'@ec.com'), concat(yhm,'_',i), 
      md5(mm),'','','','','','',0);
		set i = i+1;
	END while	
end $$

call add_user('test_312',100,300,'123456')
```

性能从优到劣大致为：`eq_ref` > `ref` > `range`（均远优于全表扫描 `ALL`）
### eq_ref：主键 / 唯一索引的「精准匹配」（性能最优）

#### 定义
	使用 **主键索引（PRIMARY KEY）** 或 **唯一非空索引（UNIQUE NOT NULL）**，对索引列进行「等值匹配」（`=`），且**每次匹配仅返回 1 条记录**（索引的唯一性保证）。


### ref：非唯一索引的「等值匹配」（性能优秀）

#### 定义

使用 **非唯一索引**（普通 B+ 树索引，无 UNIQUE 约束），对索引列进行「等值匹配」（`=`），可能返回「多条符合条件的记录」（索引不保证唯一性）。

在 MySQL 性能调优场景中，**配置参数调整** 指的是根据服务器硬件规格、业务访问特点（如读写比例、并发量）、数据量大小等实际场景，修改 MySQL 配置文件（如 `my.cnf`/`my.ini`）中的核心参数，以此优化 MySQL 的运行效率、资源利用率、稳定性，解决慢查询、连接超时、内存溢出、磁盘 IO 过高等性能问题。

简单来说，MySQL 启动时会加载一套默认的参数配置，但这套配置是通用的，无法适配所有业务场景（比如低配服务器用默认高内存参数会浪费资源，高并发业务用默认低连接数参数会导致请求排队），**配置参数调整就是 “按需定制” 这些规则**。

### 举几个核心配置参数调整的例子（易懂且高频）

1. **内存相关参数**（最核心）
    
    - `innodb_buffer_pool_size`：InnoDB 引擎的核心缓存区，用来缓存表数据和索引，是影响性能的第一关键参数。
        - 默认值可能只有几十 M，若服务器是 8G 内存、业务以读为主，可调整为 4-5G（让热点数据直接在内存中读取，避免频繁读磁盘）；
        - 若服务器只有 2G 内存，调太大反而会导致系统内存不足，需下调至 1G 左右。
    - `join_buffer_size`：关联查询（join）的缓存大小，若业务多表关联查询多且慢，可适当调大（但不宜全局设太高，避免内存浪费）。
2. **连接与并发参数**
    
    - `max_connections`：MySQL 允许的最大并发连接数，默认可能是 151。若业务高峰期并发请求多，会出现 “Too many connections” 错误，需调大（比如 500-1000，同时结合服务器资源）；
    - `wait_timeout`：空闲连接的超时时间，默认 8 小时，若业务短连接多，可调小（比如 300 秒），释放闲置连接资源。
3. **IO 与写入参数**
    
    - `innodb_flush_log_at_trx_commit`：控制事务日志（redo log）的刷盘策略，默认值 1（每次事务提交都刷盘，最安全但写入性能低）；若业务对数据一致性要求稍低、追求写入速度，可调整为 2（每秒刷盘一次）；
    - `sync_binlog`：二进制日志（binlog）的刷盘策略，默认 1（每次事务同步刷盘），高写入场景可调为 100（累计 100 次事务刷一次盘），降低磁盘 IO 压力。
4. **查询优化参数**
    
    - `query_cache_size`：查询缓存大小（注意：MySQL 8.0 已移除该参数），若业务有大量重复只读查询（比如首页数据查询），可调大缓存，避免重复解析执行 SQL；
    - `slow_query_log`：慢查询日志开关，默认关闭，调为 ON 后可记录执行时间超过 `long_query_time`（默认 10 秒）的 SQL，是调优的 “排查工具”。







