+++
date = '2026-05-13T00:00:00+08:00'
draft = false
title = 'MySQL'
tags = ['database', 'mysql']
+++
# MySQL

# MySQL

MySQL 默认端口号 3306

初始 sql 语句

客户端连接服务端命令

```sql
mysal -h 127.0.0.1 -P 3306 uroot -p
```

基本 sql 语句

```py
"""
1 sql语句是以分号为结束标识

2、show databases:查看所有库名

3、连接服务端命令简写
	mysql -uroot -p

4、错误输入不想返回错误信息，加\c取消

5、客户端退出
	exit
	quit
	
6、连接服务端时，只输入mysql也能连接，只是游客模式
"""
```

环境变量配置和系统服务制作

小知识点

```python
"""
1,查看当前进程
	tasklist
	tasklist |findstr mysql
	
2、杀死具体进程（管理员窗口）
	taskkill /F /PID PID号
"""
```

配置环境变量

优化起两个窗口

将 MySQL 服务端制作成系统服务，开机自启动

mysqld --install

mysqld --remove(移除系统服务)

## 设置密码

```python
"""
mysqladmin -uroot -p原密码 password 新密码
该命令直接在终端输入，无需进服务端

忘记密码可以移除登录认证装饰器
1 先关闭服务端
命令行方式启动（跳过认证功能）
	mysqld --skip-grant-tables
2 直接以无密码的方式连接
	mysql -uroot -p
3 修改当前用户密码
	update mysql.user set password= password(1234) where user='root' and host='localhost'

真正存储用户表的密码字段存的都是密文
只有用户自己知道明文是什么，
密码比对只比对密文
4 立刻将数据刷写到硬盘
	flush privileges;
5 关闭当前的服务端，重新以校验方式启动
"""
```

将管理员身份密码输入到配置文件中

```python
[mysql]
user="root"
password=1234
```

## 基本 sql 语句

大部分业务逻辑都是增删改查

### 针对库（文件夹）

```python
# 增
create database db1;
# 查
show databases;
show create database db1;
# 改
alter database db1 charset='utf8';
# 删
drop database db1;
```

### 针对表（文件）

```python
# 操作表的时候需要指定所在的库
# 查当前所在的库
select database();
# 切换库
use db1;
# 增
create table t1(id int,name char(4));
# 查
show tables;
show create table t1;
describe t1; # 支持简写desc t1
# 改
alter table t1 modify name char(16);
# 删
drop table t1;
# 以绝对路径形式操作不同的库
create table db2.t1(id int);
```

### 针对数据（记录）

```python
# 有库，有表在操作数据
# 增
insert into t1 values(1,'jason');
insert into t1 values(2,'today'),(3,'tank');
# 可以省略（into）
# 查
select * from t1; # 数据量特别大不建议使用，查所有数据
select id,name from t1;
# 改
update t1 set name='DSB' where id > 1;
# 删
delete from t1 where id > 1;
delete from t1 where name='jason';
# 将所有的数据清空
delete from t1;
```

## 存储引擎

针对不同的数据类型的不同处理机制

### 主要处理引擎

- Innodb  -v5.5 之后的默认引擎（表结构文件，表数据文件）

  支持事务，行锁，外键，存数据更加安全
- myisam -v5.5 之前的默认引擎,速度更快（表结构文件，表数据文件，表索引文件）
- memory -内存引擎，数据存放在内存中，临时数据存储，断电数据消失（表结构文件）
- blackhole -无论存什么，都立刻消失（表结构文件）

```python
"""
# 查看所有的存储引擎
show engines;

# 不同的存储引擎在存储表的时候的不同点
create table t1(id int) engine=innodb;
create table t2(id int) engine=myisam;
create table t3(id int) engine=memory;
create table t4(id int) engine=blackhole;
(表结构，表数据，索引)
"""
```

## 创建表的完整语法

```python
# 语法
create table 表名(
	字段名1 类型（宽度） 约束条件，
    字段名1 类型（宽度） 约束条件，
    字段名1 类型（宽度） 约束条件
)

# 注意
1、在同一张表中，字段名不能重复
2、宽度和约束条件是可写可不写的，字段名是必须写的
	约束条件支持写多个
    字段名1 类型（宽度） 约束条件1 约束条件2...
    create table t5(id); 报错
3、最后一行不能有逗号（*****）

"""补充"""
# 宽度
	一般情况下是对存储数据的限制
    默认宽度是1，超过之后要么截断，要么报错（data too long）
    insert into t1 values(null); # 关键字null不受宽度限制
数据库使用准则：
    mysql5.7之后默认是开启严格模式
    尽量少的让数据库干活，不给数据库增加压力

# 约束条件 null   not null(不能插入null)
create table t2(id int,name char not null);

"""
宽度和约束条件的关系
	宽度是限制数据的存储
	约束条件是宽度基础之上额外的约束
"""
    
```

## 严格模式

```python
# 查看严格模式
show variables like "%mode"

## 模糊匹配
	关键字 :like
    	%:匹配任意多个字符
        _:匹配任意单个字符

# 修改严格模式
	set session 只在当前窗口有效
    set global  全局有效
    
    set global sql_mode = 'STRICT_TRANS_TABLES';
    
    修改之后重新进入客户端
```

## 基本数据类型

### 整形

- 分类

			TINYINT（1） SAMLLINT（2） MEDUIMINT（3） INT（4） BINGINT（8）

- 作用

  	存储年龄、等级、id、号码等

```python
"""
TINYINT：默认情况是带符号的
			create table t3(id tinyint unsigned);设置成无符号的
		超出会只存最大可接受值
# 整形默认情况下都是带有符号的

# 针对整形，括号内的参数的作用
create table t4(id int(8));
insert into t4 values(123456789);
# 只有整形括号内的数字不是标识限制位数，有几位存几位，不足位数用空格填充，但是要遵守最大存储限制。
"""
# 约束条件，零填充
create table t5 (id int(8) unsigned zerofill);

# 总结
针对整形字段，括号内无需指定宽度

```

### 浮点型

- 分类

  FLOAT   DOUBLE    DECIMAL
- 作用

  身高、体重、薪资

```python
# 存储限制
float(255,30)  # 总共255位，小数部分占30位
double(255,30) # 总共255位，小数部分占30位
decimal(65,30) # 总共65位，小数部分占30位

# 精确度不同
float < double < decimal
# 结合实际应用场景，选择使用三者
```

### 字符类型

- 分类

  char   varcahr

  char   定长，

  	char（4） 数据超过四个字符报错，不够空格补全

  varchar 变长，

  	varchar（4） 超过四个字符直接报错，不够的有几个存几个

```python
#方法
char_length 统计字段长度
select char_length(name) from t4;
存储的时候是带空格的，但是mysql在显示的时候会自动剔除空格
# 显示空格
set global sql_mode =
'STRICT_TRANS_TABLES,PAD_CHAR_TO_FULL_LENGTH';
```

对比

|类型|缺点|优点|
| -------| --------| --------------------------------------------------------------------------------|
|char|浪费空间|存储简单，直接按照固定的字符存数据即可|
|varchar|节省空间|存取较为麻烦，不知道数据占几位，因此存储时会加上一个报头，标识数据位数，存取更慢|

### 时间类型

- 分类

  data:年月日

  datetime：年月日时分秒

  time:时分秒

  year:年份

```python
create table student(
	id int,
	name varchar(16),
    born_year year,
    birth date,
    study_time time,
    reg_time datetime
)
```

### 枚举与集合类型

- 分类

  枚举（enum）  多选一

  集合（set）       多选多
- 使用

  ```python
  create table user(
  	id int,
      name char(16),
      gender enum('male','female','others')
  );
  # 枚举字段在存数据的时候只能从枚举中选择

  create table teacher(
  	id int,
      name char(16),
      gender enum('male','female','other'),
      hobby set('read','DBJ','hecha')
  );
  # 集合可以写多个或一个，但是不能写没有的
  ```

## 约束条件

### default 默认值

```python
# 补充知识点：插入数据是可以指定字段
create table t1(
	id int,
    name char(16)
);
insert into t1 (name,id) values('jason',1);

create bable t2(
	id int,
    name char(16),
    gender enum('male','female','other') default 'male'
);
isnert into t2(id,name) values (1,'egon');
isnert into t2 values (2,'egon','female');
```

### unique 唯一

```python
# 单列唯一
create table t3(
	id int unique,
    name char(16)
)
insert into t3(1,'egon'),(2,'jason'); 
# 联合唯一
"""
ip和port
单个都可以重复，但是加在一起必须是唯一的
"""
create table t4(
	id int,
    ip char(16),
    port int,
    unique(ip,port)
);
innsert into t4 values (1,'127.0.0.1',8080);
```

### primary key 主键

```python
"""
1、单从约束效果上看，primary key等价于not null + unique
非空且唯一！！！！
"""
create table t5(id int primary key);
insert into t5 values(null); # can't be null
insert into t5 values(1),(1); # 不能重复

"""
2、他除了有约束效果之外，他还是Innodb存储引擎组织数据的依据
Innodb存储引擎在创建表的时候必须要有primary key
因为他类似输得目录，能够提升查询效率，并且也是创建表的依据
"""
# 1 一张表中有且只有一个主键，如果没有设置主键，那么会从上往下搜索直到遇到一个非空且唯一的字段将它升级为主键
create rable t6(
	id int,
    name char(16),
    age int not null unique,
    addr char(32) not null unique
);
# 2 如果表中没有主键也没有其他任何非空且唯一字段，那么Innodb会采用内部提供的一个隐藏字段作为主键，隐藏意味着无法使用到它，无法提升查询速度

# 3 一张表中通常都有一个主键字段，并且通常将id字段作为主键
create table t5(
	id int primary key,
    name char(16)
);
# 联合主键（将多个字段联合起来作为表的主键，本质还是一个主键）
create table t4(
	id int,
    ip char(16),
    port int,
    primary key(ip,port)
);
"""
在创建表的时候要加上primary key
"""
```

### auto_increment 自增

```python
# 当编号特别多的时候，自增序号
create table t8(
	id int primary key auto_increment,
    name char(16)
);
insert into t8(name) values('jason'),('egon'),('kevin');
```

#### 结论

```python
"""
以后在创建表的id（数据的唯一标识id，uid，sid）字段的时候写：
id int primary key auto_increment
"""

# 补充
delete from删掉数据后，主键的自增不会停止
truncate t1 清空数据并且重置主键
```

## 表与表之间的键关系

### 外键

```python
"""
外键就是用来建立表与表之间关系的
foreign key
"""
```

### 表关系

```python
"""
表关系有四种
	一对一关系
	多对多关系
	一对多关系
	没有关系
"""
```

#### 一对多关系

```python
"""
判断表与表关系要换位考虑
一个员工只能对应一个部门
一个部门可以对应多个员工
表关系是一对多
"""

foreign key
	1 一对多表关系  外键字段建在多的一方
    2 在创建表的时候要先建被关联表
    3 录入数据的时候先录入被关联表
# sql语句建立表关系
create table dep(
	id int primary key auto_increment,
    dep_name char(16),
    dep_desc char(32)
);

create table emp(
	id int primary key auto_increment,
    name char(16),
    gender enum('male','female','others') default 'male',
    dep_id int,
    foriegn key(dep_id) references dep(id)
);

# 修改emp里面的dep_id字段 或 dep中的id字段
update dep set id=200 where id=2; # error
delete from dep;# error

# 1 先删除教学部对应的员工数据，再修改id
# 2 同步更新删除
"""
级联更新
级联删除
"""
create table dep(
	id int primary key auto_increment,
    dep_name char(16),
    dep_desc char(32)
);

create table emp(
	id int primary key auto_increment,
    name char(16),
    gender enum('male','female','others') default 'male',
    dep_id int,
    foriegn key(dep_id) references dep(id) 
    on uodate cascade # 同步更新
    on delete cascade # 同步删除
);

```

#### 多对多

```python
"""图书表和作者表"""

# 针对多对多关系需要重新再创建一张单独表
记录两者的关系(如下表所示)
此表对于原来两张表是一对多的关系

create table book(
	id int rimary key auto_increment,
    title varchar(32),
    price int
);
create table author(
	id int primary key auto_incerment,
    name varchar(32),
    age int
);
create table book2author(
	id int primary key auto_increment,
    author_id int,
    book_id int,
    foreign key(book_id) referencs book(id)
    on update cascade
    on delete cascade,
    foriegn key(author_id) references author(id)
    on update cascade
    on delete cascade
)

```

|Id|book_id|author_id|
| -: | ------: | --------: |
|1|1|1|
|2|1|2|
|3|2|1|
|4|3|2|
|5|4|1|

#### 一对一

```python
"""
一个人多用用个字段，但是有的字段查询频率较低，可以将这些字段炒成了两个表
Id name age
id addr hobby phone ...
这个时候两张表是一对一对的关系
"""

一对一关系，外键建在任意一方都可以，一般建在访问频率较高的那一方
reate tbale authoerdetail(
	id int primary key auto_increment,
    phone int,
    addr varchar(32)
;
create table author(
	id int primary key auto_increment,
    name varchar(16),
    age int,
    authordetail_id int unique,
    foriegn key(authordetail_id) references authoerdetail(id)
    on update cascade
    on delete cascade
)
```

## 操作表

### 修改表

```python
# MySQL对大小写是不敏感的

"""
1、修改表名
	alter table 表名 rename 新表名；
	
2、增加字段
	alter table 表名 add 字段名 字段类型（宽度） 约束条件；
	alter table 表名 add 字段名 字段类型（宽度） 约束条件 first；
	alter table 表名 add 字段名 字段类型（宽度） 约束条件 after 字段名
	
3、删除字段
	alter table 表名 drop 字段名；
	
4、修改字段
	alter table 表名 modify 字段名 字段类型（宽度） 约束条件；
	
	alter table 表名 change 旧字段名 新字段名 字段类型（宽度） 约束条件；
"""
```

### 复制表

```python
"""
sql语句的查询结果是一张虚拟表
"""
create table 新表 select * from 旧表; # 不能复制主键，外键，索引等
create table 新表 select * from 旧表 where id>3;
```

## 查询表

```python
# 表准备
create table emp(
	id int not null unique auto_increment,
    name varchar(20) not null,
	sex enum('male','female') not null default 'male',#大部分是男的
    age int(3) unsigned not null default 28,
	hire_date date not null,
    post varchar(50),
    post_comment varchar(100),
    salary double(15,2),
    office int,#一个部门一个屋子
    depart_id int
);

# 插入数据
insert into emp(name,sex,age,hire_date,post,salary,office,depart_id) values
('jason','male',18,'20170301','张江第一帅形象代言',7300.33,401,1), # 以下是教学部
('tom','male',78,'20150302','teacher',1000000.31,401,1),
('kevin','male',81,'20130305','teacher',8300,401,1),
('tony','male',73,'20140701','teacher',3500,401,1),
('owen','male',28,'20121101','teacher',2100,401,1),
('jack','female',18,'20110211','teacher',9000,401,1),
('jenny','male',18,'19000301','teacher',30000,401,1),
('sank','male',48,'20101111','teacher',10000,401,1),
('哈哈','female',48,'20150311','sale',3000.13,402,2), # 以下是销售部门
('呵呵','female',38,'20101101','sale',2000.35,402,2),
('西西','female',18,'20110312','sale',1000.37,402,2),
('乐乐','female',18,'20160513','sale',3000.29,402,2),
('拉拉','female',28,'20170127','sale',4000.33,402,2),
('僧龙','male',28,'20160311','operation',10000.13,403,3), # 以下是运营部门
('程咬金','male',18,'19970312','operation',200000,403,3),
('程咬银','female',18,'20130311','operation',190000,403,3),
('程咬铜','male',18,'20150411','operation',180000,403,3),
('程咬铁','female',18,'20140512','operation',170000,403,3);

# 当表的数据特别多，显示错乱可以用\G分行展示
select * from emp\G;

```

### 几个重要关键字的执行顺序

```python
#书写顺序
select id,name from emp where id > 3;
# 执行顺序
from 
where
select

"""
虽然执行顺序和书写顺序不一致
可以按照书写顺序的方式写sql
	select * 先用*号占位
	之后再把*替换成具体想要的字段
"""
```

### where 筛选条件

```python
# 作用：对整体数据的一个筛选操作
# 1、查询id大于等于3 小于等于6的所有数据
select id,name,age from emp where id>=3 and id <=6;
select id,name,age from emp where id between 3 and 6;

# 2、查询薪资是20000或18000或17000的数据
select * from emp where salary=20000 or salary=18000 or salary=17000;
select * from emp where salary in (20000,18000,17000);

# 3、查询员工姓名中包含字母o的姓名和薪资
"""
模糊查询
	like 
		% 匹配任意多个字符
		_ 匹配任意单个字符
"""
select name,salary from emp where name like '%o%';

# 4、查询员工姓名是由四个字符组成的姓名和薪资
select name salary from emp where name like '____'; # 模糊匹配
select name salary from emp where char_length(name) = 4;

# 5、查询id小于3或者id大于6的数据
select * from emp where id not between 3 and 6;

# 6、查询薪资不在20000,18000的数据
select * from emp where salary not in (20000,18000,17000);

# 7、查询岗位描述为空Dee员工姓名和岗位名  
# 针对null要用is
select name,post from emp where post_commet is null;
```

### group by 分组

```python
# 分组应用场景
	男女比例
    部门平均薪资
    国家之间数据统计
# 1、按照部门分组
select * from emp group by post;
"""
分组时候可操作的最小单位是组，不再是单个数据
	上述命令在没有设置严格模式的情况下是可以正常执行的，返回的是分组之后每个组的第一条数据，但是这并不符合分组规范：分组之后应以组为操作单位
	如果设置了严格模式，那么上述命令会直接报错
"""
set global sql_mode = 'strict_trans_tables,only_full_group_by';
# 设置严格模式后，分组默认只能拿到分组的依据
select post from emp group by post; 
# 按照什么分组就只能拿到分组，其他的字段不能 直接获取，需要借助于一些方法

"""
什么时候需要分组
key word ： 每个，平均，最高，最低
聚合函数：max,min,avg,count，sum
"""
# 1、获取每个部门的最高薪资
select post,max(salary) from emp group by post;
select post as '部门',max(salary) as '最高薪资' from emp group by post; # 可以在显示的时候显示别名
# 2、获取每个部门的最低薪资
select post,min(salary) from emp group by post;
# 3、获取每个部门的平均薪资
select post,avg(salary) from emp group by post;
# 4、获取每个部门的薪资总和
select post,sum(salary) from emp group by post;
# 5、获取每个部门的人数
select post,count(id) from emp group by post; # 常用，符合逻辑
select post,count(salary) from emp group by post;
# count后不能放null

# 查询分组后的部门名称以及每个部门下所有的员工姓名
# group_concat 不单单支持获取其他字段，还支持拼接操作
select post,group_concat(name) from emp group by post;
select post,group_concat(name,‘_DSB’) from emp group by post;
select post,group_concat(name,‘:’,salary) from emp group by post;
# concat_ws:如果多个字段之间的链接付相同，可以使用此命令
select concat(':',name,age,sex) from emp;
输出： jason:18:male
# concat不分组的时候用concat
select concat_ws('NAME:',name),concat('SAL:',salary) from emp;

# 补充：as不仅可以给字段起别名，还可以给表取别名
select emp.ip,emp.name from emp;
select t1.ip,t1.name from emp as t1;

# 查询每个人年薪 12薪
select name,salary*12 from emp;

```

#### 分组注意事项

```python
# 关键字where和group by同时出现的时候，group by 必须在where的后面
where先对整体数据进行过滤之后再分组
where的筛选条件不能使用聚合函数
select id,name,age from emp where max(salary) > 3000;# error
select max(salary) from emp; # 不分组默认就是一组

# 统计各部门年龄在30岁以上的员工平均薪资
	1 先求所有年龄大于30的员工
    	select * from emp where age > 30;
    2 在对结果进行分组
    	select * from emp where age>30 group by post;
    select post,avg(salary) from emp where age>30 group by post;

```

### having 分组之后的筛选条件

```python
"""
having的语法和where是一致的
having是在分组之后进行的过滤操作
having是可以直接使用聚合函数的
"""
# 统计各部门年龄在30岁以上的员工工资并且保留平均薪资大于10000的部门
select post,avg(salary) from emp
		where age>30 # 分组前
    	group by post
        having avg(salary)>1000 # 分组后
        ;
```

### distinct 去重

```python
"""
一定要注意，必须是完全一样的数据才能去重！！！！
注意： 完全一样！！！！
不要忽视主键，有主键存在的情况下无法去重
"""
select distinct id,age from emp; # empty
select distinct age from emp; # 把主键去掉

# 查询主要关键字
select distinct 字段一，字段二，，， from 表名；
```

### order by 排序

```python
select * from emp order by salary;
select * from emp order by 2; # 按照第二列排序
select * from emp order by salary desc;
"""
order by默认是升序， asc 默认可以不写
desc降序
"""
select * from emp order by age desc,salary asc;
# 先按照age降序排，age相同再按照salary升序排
# 统计各部门年龄在10岁以上的员工工资并且保留平均薪资大于1000的部门，然后对平均工资降序排序
select post,avg(salary) from emp
		where age>30 # 分组前
    	group by post
        having avg(salary)>1000 # 分组后
        order by avg(salary) desc
        ;
```

### limit 限制展示条数

````python
select * from emp;
# 针对过多数据通常进行分页处理
select * from emp limit 3; # 只展示三条数据
select * from emp limit 0,5;
select * from emp limit 6,5;
# 第一个参数是起始位置，第二个参数是条数
````

### regexp 正则

```python
select * from emp where name regexp '^j.*(n|y)$'
需要什么表达式上网搜
python中借助re模块
    面试
    1、re模块中常用的方法
        findall：分组优先展示
            不会展示所有正则表达式匹配到的内容
            而仅仅展示括号内正则表达式匹配到的内容
        match：从头匹配
        search：从整体匹配
    2、贪婪匹配和非贪婪匹配
        正则表达式默认是贪婪匹配
        变成非贪婪需要在表达式后面加‘？’
```

### 多表操作

```python
# 建表
# -- 部门表 dep
create table dep(
    id int,
    name varchar(20)
);

# -- 员工表 emp
create table emp(
    id int primary key auto_increment,
    name varchar(20),
    sex enum('male','female') not null default 'male',
    age int,
    dep_id int
);

# 插入数据
# -- 向部门表 dep 插入数据
insert into dep values
(200,'技术'),
(201,'人力资源'),
(202,'销售'),
(203,'运营');

# -- 向员工表 emp 插入数据
insert into emp(name,sex,age,dep_id) values
('jason','male',18,200),
('egon','female',48,201),
('kevin','male',18,201),
('nick','male',28,202),
('owen','male',18,203),
('jerry','female',18,204);
```

#### 联表查询

```python
select * from dep,emp;# 结果 笛卡尔积

select * from emp,dep where emp.dep_id = dep.id;
"""
mysql直到在查询过程中经常用到拼表操作
有四种方法
	inner join 内连接
	left join 左链接
	right join 右连接
	union 全连接
"""
# inner join 内连接
select from emp inner join dep on emp.dep_id = dep.id;
# 只拼接两张表中共有的数据部分

# left join 左链接
select from emp left join dep on emp.dep_id = dep.id;
# 左表所有的数据都展示出来，没有的用null填充

# right join 右连接
select from emp right join dep on emp.dep_id = dep.id;
# 右表所有的数据都展示出来，没有的用null填充

# union 全连接
select from emp left join dep on emp.dep_id = dep.id 
union 
select from emp right join dep on emp.dep_id = dep.id;
# 左右两表大的内容都展示出来，没有的用null填充
```

#### 子查询

```python
"""
子查询就是平时解决问题的思路
	分步骤解决问题
		第一步
		第二步
将一个查询语句的结果当做另一个查询语句的条件去使用，用括号括起来
"""
# 查询部门是技术或者人力资源的员工信息
	1 先获取部门的id号
    2 再去员工表中筛选出对应的员工
	select id from dep where name='技术' or name ='人力资源';
    select name from emp where dep_id in (200,201);
    
	select * from emp where dep_id in (select id from dep where name='技术' or name = '人力资源');
```

#### 总结

表的查询结果可以当做其他表的查询条件

也可以通过起别名的方式把它作为一张虚拟表跟其他表关联

**多表查询就两种方式**：1，拼表 2，子查询

#### 知识点补充

```python
# 查询平均年龄在25以上的部门名称
# 多表查询两个思路： 1、联表，2、子查询
# 连表操作
	1 先拿到拼接结果
    2 分析语义需要按照部门分组
    select * from emp inner join dep
    	on emp.dep_id = dep.od
        group by dep.name
        having avg(age) > 25;
    """射击多表操作的时候一定要加上表的前缀"""
# 子查询
	select name from dep where id in
    	(select dep_id from emp group by dep_id 
			having avg(age) > 25);
# 关键字exist（了解）
	只返回	True False
    返回True时，外层查询语句执行
    返回False时，外层查询语句不执行
    select * from emp where exists 
    	(select id from dep where id > 8);

```

## pymysql 模块

```python
import pymysql

conn = pymysql.connect(
    host = '127.0.0.1',
    port = 3306,
    user = 'root',
    password = '', 
    database = 'day48', # 指定对象
    charset = 'utf8' # 不加-
)

cursor = conn.cursor(cursor=pymysql.cursors.DictCursor) # 产生一个游标对象
# 不加参数默认是元组形式返回
# 字典形式返回内容
sql = 'select * from teacher;'
res = cursor.execute(sql) # execute返回的是当前sql语句影响的行数
# 获取执行命令的结果
print(cursor.fetchone()) # 直接拿到数据
print(cursor.fetchall()) # 拿到列表套数据
print(cursor.fetchmany(5)) # 指定拿几条
# 控几指针移动的方法
cursor.scroll(1, 'relative')# 相对于光标位置向后移动一位
cursor.scroll(1, 'absolute')# 相对于起始位置向后移动一位
```

#### pymysql 补充

```python
import pymysql

conn = pymysql.connect(
    host = '127.0.0.1',
    port = 3306,
    user = 'root',
    passwd = '',
    database = 'day49',
    charset = 'utf8',
    autocommit = True # 加上这个不用commit二次确认
)

cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
sql = 'insert into user(name,password) values(%s,%s)'
# rows = cursor.execute(sql,('john',123))
rows = cursor.executemany(sql,[('xxx',123),('ooo',123),('aaa',123)]) # 插入多条数据，列表套元组
print(rows)
# conn.commit() # 修改数据库加上commit操作，进行确认
```

## sql 注入

```python
sql注入是一种高危 Web 安全漏洞，核心是用户可控输入被当作 SQL 代码执行，从而篡改数据库逻辑、窃取数据甚至控制服务器。
利用sql语法特性
mysql中利用的就是其注释语法‘--’，‘#’

语句 1：注释掉密码条件的注入
select * from user where name='jason' --asfgghh and password=''
语句 2：恒成立条件的注入
select * from user where name='xxx' or 1=1 -- sakjdk1jak1djas1' and password=''

# 日用软件常限制特殊字符的输入
# 敏感的数据不要自己做拼接，交给execute方法
sql = "select * from users where name=%s and password=%s;"
# 用%s占位，execute方法拼接
rows = cursor.execute(sql,(username,password))
```

## 了解内容

### 视图

视图就是通过查询得到一张虚拟表，然后保存下来，下次可以直接使用。

如果要频繁的操作一张虚拟表，你就可以制作成视图后续直接操作。

```python
create view 表名 as 虚拟表的查询sql语句
具体使用
CREATE VIEW teacher2course AS
SELECT * 
FROM teacher 
INNER JOIN course
ON teacher.tid = course.teacher_id;
```

**注意**：

- 创建视图在硬盘上只会有表结构没有表数据（数据还是来自于之前的表）
- 视图一般只用来查询 里面的数据不要继续修改 可能会影响真正的表

使用频率不高：当你创建了很多视图之后 会造成表的不好维护

### 触发器

在满足对表数据进行增、删、改的情况下，自动触发的功能

使用触发器可以帮助我们实现监控、日志...

触发器可以在六种情况下自动触发 增前 增后 删前 删后 改前 改后

**基本语法**

```python
-- 触发器通用语法模板
CREATE TRIGGER 触发器的名字 
BEFORE/AFTER INSERT/UPDATE/DELETE 
ON 表名
FOR EACH ROW
BEGIN
    -- 要执行的SQL语句
    SQL语句
END;

-- 命名规范说明
-- 触发器的名字通常建议见名知意，格式一般为：tri_触发时机_触发操作_表名
-- 比如 tri_before_insert_t1 就表示：t1表 插入前 触发的触发器

-- 插入前触发器示例
CREATE TRIGGER tri_before_insert_t1 
BEFORE INSERT ON t1
FOR EACH ROW
BEGIN
    -- 这里写具体的SQL逻辑
    SQL语句
END;

# 修改MySQL默认语句结束符（仅作用于当前会话/窗口）
DELIMITER $$
# 含义：将MySQL默认的语句结束符号由 ; 改为 $$,只在当前窗口有效。

-- 临时修改语句结束符，避免与触发器内的 ; 冲突
DELIMITER $$

-- 创建触发器：在cmd表插入数据后触发
CREATE TRIGGER tri_after_insert_cmd 
AFTER INSERT ON cmd
FOR EACH ROW
BEGIN
    -- 条件判断：如果新插入记录的success字段为'no'
    IF NEW.success = 'no' THEN
        -- 向errlog表插入错误日志
        INSERT INTO errlog(err_cmd, err_time)
        VALUES (NEW.cmd, NEW.sub_time);
    END IF;
END$$ -- 用自定义结束符标记触发器定义结束

-- 恢复默认语句结束符
DELIMITER ;

# 删除触发器
drop trigger tri_after_insert_cmd;
```

### 事务（掌握）

开启一个事务可以包含多条 sq1 语句这些 sq1 语句要么同时成功要么一个都别想成功，称之为事务的原子性

保证了对数据操作的安全性

eg:还钱的例子
egon 用银行卡给我的支付宝转账 1000
1 将 egon 银行卡账户的数据减 1000 块 ；2 将 jason 支付宝账户的数据加 1000 块

**事务的四大特性**（ACID）

- A：原子性

  	一个事务是一个不可分割的单位，事务中包含的诸多操作要么同时成功要么同时失败
- C：一致性

  	事务必须是使数据库从一个一致性的状态变到另外一个一致性的状态

  	一致性跟原子性是密切相关的
- I：隔离性

  	一个事务的执行不能被其他事务干扰
  	（即一个事务内部的操作及使用到的数据对并发的其他事务是隔离的，并发执行的事务之间也是互相不干扰的）
- D：持久性

  	也叫"永久性"
  	一个事务一旦提交成功执行成功那么它对数据库中数据的修改应该是永久的接下来的其他操作或者故障不应该对其有任何的影响

**如何使用**

```python
# 1、开启事务
start transaction;
# 2、回滚（回到事务执行之前的状态）
rollback;
# 3、确认（确认后无法回滚）
commit;

"""模拟转账功能"""
create table user (
    id int primary key auto_increment,
    name char(16),
    balance int
);

insert into user(name, balance)
values
    ('jason', 1000),
    ('egon', 1000),
    ('tank', 1000);
    
-- 1 先开启事务
start transaction;

-- 2 多条sql语句
update user set balance=900 where name='jason';
update user set balance=1010 where name='egon';
update user set balance=1090 where name='tank';

-- 3 提交事务（如果都没问题）
commit;

-- 或者 回滚事务（如果中间出错）
-- rollback;
```

### 存储过程

存储过程就类似于 python 中的自定义函数
它的内部包含了一系列可以执行的 sql 语句，存储过程存放于 MySQL 服务端中，你可以直接通过调用存储过程触发内部 sql 语句的执行

**使用**

```python
create procedure 存储过程的名字（形参1，形参2，...）
begin
	sql代码
end
# 调用
call 存储过程的名字（）;
```

**三种开发模式**

1. 第一种

   ```python
   """
   应用程序: 程序员写代码开发
   MySQL: 提前编写好存储过程，供应用程序调用

   好处: 
   - 开发效率提升了
   - 执行效率也上去了

   缺点: 
   - 考虑到人为因素、跨部门沟通的问题
   - 后续的存储过程的扩展性差
   """
   ```
2. 第二种

   ```python
   """
   应用程序：程序员写代码开发之外，涉及到数据库操作也自己动手写

   优点：
   - 扩展性很高

   缺点：
   - 开发效率降低
   - 编写SQL语句太过繁琐，而且后续还需要考虑SQL优化的问题
   """
   ```
3. 第三种

   ```python
   """
   应用程序：只写程序代码，不写SQL语句，基于别人写好的操作MySQL的Python框架直接调用操作即可
   → ORM框架

   优点：
   - 开发效率比上面两种情况都要高

   缺点：
   - 语句的扩展性差
   - 可能会出现效率低下的问题
   """
   ```

具体演示

```python
delimiter $$
create procedure p1(
    in m int,   -- 只进不出，m不能返回出去
    in n int,
    out res int -- 该形参可以返回出去
)
begin
    select tname from teacher where tid>m and tid<n;
    set res=666; -- 将res变量修改，用来标识当前的存储过程代码确实执行了
end $$
delimiter ;

# 针对形参res 不能直接传数据 应该传一个变量名
# 定义变量
set @ret = 10;

# 查看变量对应的值
select @ret;
```

pymysql 调用存储过程

```python
# 调用存储过程 p1，传入参数
cursor.callproc('p1', (1, 5, 10))

# 这三个变量是callproc自动生成的会话变量，用来对应传入的参数
# @_p1_0=1  对应第一个参数 m=1
# @_p1_1=5  对应第二个参数 n=5
# @_p1_2=10 对应第三个参数 res=10

# 获取存储过程中select语句返回的结果集
print(cursor.fetchall())
```

### 函数

```python
('jason', '0755', 'ls -l /etc', NOW(), 'yes')

create table blog (
    id int primary key auto_increment,
    name char(32),
    sub_time datetime
);

insert into blog (name, sub_time)
values
    ('第1篇', '2015-03-01 11:31:21'),
    ('第2篇', '2015-03-11 16:31:21'),
    ('第3篇', '2016-07-01 10:21:31'),
    ('第4篇', '2016-07-22 09:23:21'),
    ('第5篇', '2016-07-23 10:11:11'),
    ('第6篇', '2016-07-25 11:21:31'),
    ('第7篇', '2017-03-01 15:33:21'),
    ('第8篇', '2017-03-01 17:32:21'),
    ('第9篇', '2017-03-01 18:31:21');

select date_format(sub_time, '%y-%m'), count(id)
from blog
group by date_format(sub_time, '%y-%m');
```

### 流程控制

```python
# if判断
delimiter //
create procedure proc_if ()
begin
    declare i int default 0;
    if i = 1 then
        select 1;
    elseif i = 2 then
        select 2;
    else
        select 7;
    end if;
end //
delimiter ;

# while循环
delimiter //
create procedure proc_while ()
begin
    declare num int;
    set num = 0;
    while num < 10 do
        select num;
        set num = num + 1;
    end while;
end //
delimiter ;
```

### 索引

ps: 数据都是存在硬盘上的，查询数据不可避免地需要进行 IO 操作

索引：就是一种数据结构，类似于书的目录。 意味着以后在查询数据时，应该先找目录再找数据，而不是一页一页翻书，从而提升查询速度、降低 IO 操作。

索引在 MySQL 中也叫“键”，是存储引擎用于快速查找记录的一种数据结构：

- primary key（主键索引）
- unique key（唯一索引）
- index key（普通索引）

注意：foreign key（外键）不是用来加速查询的，不在索引优化的研究范围内。

上面三种 key 的区别：

	primary key 和 unique key：除了可以增加查询速度外，还各自带有约束条件（主键非空且唯一、唯一键唯一）

	index key：没有任何约束条件，仅用于帮助快速查询数据

**本质**： 通过不断缩小想要的数据范围筛选出最终的结果， 同时将随机事件（一页一页地翻）变成顺序事件（先找目录、再找数据）。

也就是说，有了索引机制，我们可以总是用一种固定的方式查找数据。

一张表中可以有多个索引（多个目录）

索引虽然能够帮助你加快查询速度，但是也有缺点

```python
"""
1 当表中有大量数据存在的前提下，创建索引速度会很慢
2 在索引创建完毕之后，对表的查询性能会大幅度的提升，但是写的性能也会大幅度的降低
"""
索引不要随意的创建！！！
```

#### b+ 树

```python
"""
只有叶子节点存放的是真实的数据，其他节点存放的是虚拟数据，仅仅是用来指路的。
树的层级越高，查询数据所需要经历的步骤就越多（树有几层，查询数据就需要几步）。

一个磁盘块存储是有限制的。
为什么建议你将id字段作为索引：
    占得空间少，一个磁盘块能够存储的数据多，
    那么就降低了树的高度，从而减少查询次数。
"""
```

#### 聚集索引（primary key）

```python
"""
聚集索引指的就是主键

InnoDB 只有两个文件，直接将主键存放在了ibd表中
MyISAM 三个文件，单独将索引存在一个文件
"""
```

#### 辅助索引（unique,index）

查询数据的时候不可能一直使用到主键，也有可能会用到 name,password 等其他字段

那么这个时候你是没有办法利用聚集索引。这个时候你就可以根据情况给其他字段设置辅助索引(也是一个 b+ 树)

```python
"""
叶子节点存放的是数据对应的主键值
先按照辅助索引拿到数据的主键值，
之后还是需要去主键的聚集索引里面查询数据
"""
```

#### 覆盖索引

在辅助索引的叶子节点就已经拿到了需要的数据

```python
# 给name设置辅助索引
-- 覆盖索引：直接从name索引里拿到所需字段，无需回表
select name from user where name='jason';

# 非覆盖索引：需要先从name索引拿到主键，再回表查age字段
select age from user where name='jason';
```
