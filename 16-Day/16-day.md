# JDBC  
<hr>  
  
## 多表设计
	#自动增长 
	create table t5
	(
		id int primary key auto_increment,
		name varchar(10);
	);	

## 多表连接查询
	#交叉查询
	select * from stu s cross join score c on s.id = c.id;  
 
	#内连接查询
	select name,chinese,english,history,chinese+english+history 总分 from stu s inner join score c on s.id=c.sid;
	
	#查询所有人的成绩
	#左外链查询
	select name,chinese,english,history,chinese+english+history 总分 from stu s left join score c on s.id=c.sid;
	
	#没有参加考试的人
	#子查询
	select * from stu where id not in(select sid from score);
	
	#联合查询
	select * from score where china >80 union select * from score where id =4;