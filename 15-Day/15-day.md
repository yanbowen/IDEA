# JDBC  
<hr>  
  
## JDBC概述  
* Java Data Base Connectivity(Java数据库连接)  
* 组成包： java.sql.\*; javax.sql.*;
  
## SQL简介
* SQL ： Structured Query Language
* 结构化查询语言
* 作用 ： 是一种定义、操作、管理关系数据库的句法。   

## SQL语句分为三种类型
* DML ： 数据操作语言 ( Data Manipulation Language )
* DDL ： 数据定义语言 ( Data Definition Language )
* DCL ： 数据控制语言 ( Data Control Language )
* DQL ： 数据查询语言
* TPL ： 事务处理语言
  
## MySQL 5.5
	#进入数据库
	mysql -u root -proot  
![](https://i.imgur.com/H0oxPZv.png)
### 数据库的操作
注释 ## （oracle 注释 --）   
CREATE		//创建  
ALTER		//更改表信息  
DROP		//删除  
TRUNCATE	//删除表信息  

#### 针对数据库的操作
	#查看所有的数据库
	show databases;  
	
	#c创建数据库
	CREATE DATABASE mydb;
  
	#查看创建数据库的语句
	SHOW CREATE DATABASE mydb;
  
	#改变当前的数据库
	use mydb; 

	#删除数据库
	drop database mydb;

	#创建数据库并设置字符集用gbk
	create database mydb1 character set gbk;

	#修改数据库字符集为gbk
	alter database mydb character set gbk;  
  
	#展示正在使用的数据库
	show database();
  
#### 针对表的操作
	#创建表t
	create table t
	(id int ,
	 name varchar(30)
	);

	#查看创建表源码
	show create table t;

	#创建表t1，使用字符集gbk
	create table t1
	(
		id int,
		name varchar(30),
		optime timestamp 
	)character set gbk;
	
	#插入数据
	#设置客户端字符集为gbk
	set character_set_client=gbk;
	#设置结果集字节集为gbk
	set character_set_results=gbk;
	insert into t1(id,name) values(1,'张无忌')；
	
	#查询表
	select * from t; 

	#更新
	update t set name='杨康' where id = 3;
	#更新多个字段
	update t set id=6,name='萧峰' where id=1；

	#删除 //delete 只能删除行
	delete from t where id=4;
	#删除所有数据
	delete from t;
	#删除所有记录
	truncate table t;
	
	#增加一个字段address
	alter table t add address varchar(100);
	#删除字段
	alter table t drop column address;
	
	#查看表的结构
	desc t;  
  
#### DQL数据查询语言 

	#创建一个学生表
	create table stu
	(
		id int primary key,					#主键约束
		name varchar(30) unique,			#唯一约束		
		sex char(2) not null,				#非空约束
		age int check(age>0 and age<120),	#检查约束(mysql不支持)
		address varchar(50) default '地球'	#默认约束
	);
	insert into stu values(1,'张无忌','男',20,'武当山');
	insert into stu values(2,'小龙女','女',18,'古墓');
	insert into stu values(3,'黄蓉','女',16,'桃花岛');
	insert into stu values(4,'康熙皇帝','男',56,'紫禁城');
	insert into stu values(5,'刘备','男',46,'白帝城');  
  
	#查看带条件信息
	select * from stu where id = 2;
	#查看年龄在20-50之间
	select * from stu where age>=20 and age <=50;
	#查看姓名
	#select name from stu;
	select name,age,sex from stu;
	
	#模糊查询
	select * from 表名 where 字段名 like 字段表达式
	%  表示任意字符数
	_  表示任意一个字符
	[] 表示在某个区间

	#查询所有以张开头的人
	select * from stu where name like '张%';
	#查询姓名中有张字的人
	select * from stu where name like '%张%';
	
	#查找表中有几种不同数据
	select distinct sex from stu;
	
	create table score
	(
		id int,
		sid int,
		china int,
		english int,
		history int,
		#创建引用约束
		constraint stu_score_FK foreign key (sid) references stu(id)
	)

	insert into score values(1,1,68,54,81);
	insert into score values(2,3,89,98,90);
	insert into score values(3,4,25,54,74);
	insert into score values(4,6,48,34,29);
	
	#字段可以有表达式
	select id,china+10.english,history from score;
	#给字段起别名
	select id 编号,china 语文,english 英语,history 历史 from score；

	#查询
	select * from stu where address ='桃花岛' or address = '武当山';
	select * from stu where address in('桃花岛','武当山');
	
	#查询没有考试的人
	select id,name from stu where id not in (select sid from score);
	
	#查询NULL
	select * from stu where address is null;
	
	#排序(order by)
	#对Chinese升序排列
	select * from score order by china asc;
	#对history降序排列
	select * from score order by history desc;
	#根据多个字段进行排列
	select * from score order by china asc,history desc;  
![](https://i.imgur.com/j0zflsE.png)  
  
* 主键 ： 唯一区分每一条记录的一列或者多列的值  

--	
	#创建引用约束
	alter table score add constraint stu_score_FK foreign key(sid) references stu(id);
	
	#引用约束
	1.添加记录时必须先添加主表中的记录，再添加子表中的记录
	2.不能更改主表中具有外键约束的记录的主键
	3.删除记录时，不允许删除具有外键关系的主表中的记录（也就是先删除子表的记录，然后再删除主表中的记录）

	#删除约束
	alter table score drop foreign key stu_XXX_FK ;
		
	