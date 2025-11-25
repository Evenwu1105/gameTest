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









