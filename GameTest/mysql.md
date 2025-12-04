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









