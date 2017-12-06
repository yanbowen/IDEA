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

### 连接查询
	#交叉查询
	select * from stu s cross join score c on s.id = c.id;  
	#内连接查询
	select name,chinese,english,history,chinese+english+history 总分 from stu s inner join score c on s.id=c.sid;
	#查询所有人的成绩
	#外连接
	#左外链查询
	select name,chinese,english,history,chinese+english+history 总分 from stu s left join score c on s.id=c.sid;
	#右外连接查询
![](https://i.imgur.com/Aqx0QiS.png)  

###子查询
	#没有参加考试的人
	select * from stu where id not in(select sid from score);
	
###联合查询
	select * from score where china >80 union select * from score where id =4;  
 
	#分组查询
	select sex from stu group by sex ;  

	#聚合函数
	#sum max min avg count
	
	#表内有多少条记录
	select count(*) from stu;
	#单列综合
	select sum(china) from score;
	#单列平均值
	select avg(china) from score;
	#单列最大
	select max(china) from score;
	
## 数据的备份与恢复
	#在cmd里执行 
	#导出数据库
	mysqldump -u root -proot mydb1>d:\mydb1.sql
	#导入数据库
	mysql -u root -proot mydb1<d:\mydb1.sql
	#导出一个表，包括表结构和数据  
	mysqldump -u用户名 -p 密码  数据库名 表名> 导出的文件名 
	C:\Users\jack> mysqldump -uroot -pmysql sva_rec date_rec_drv> e:\date_rec_drv.sql 
	#导出一个数据库结构 
	C:\Users\jack> mysqldump -uroot -pmysql -d sva_rec > e:\sva_rec.sql 
	#导出一个表，只有表结构 
	mysqldump -u用户名 -p 密码 -d数据库名  表名> 导出的文件名 
	C:\Users\jack> mysqldump -uroot -pmysql -d sva_rec date_rec_drv> e:\date_rec_drv.sql 
  
## JDBC
 JAVA连接MySQL稍微繁琐，所以先写一个类用来打开或关闭数据库 ： DBHelper.java
	package com.jdbc.demo;  
  
	import java.sql.Connection;  
	import java.sql.DriverManager;  
	import java.sql.PreparedStatement;  
	import java.sql.SQLException;  
  
	public class DBHelper {  
    	public static final String url = "jdbc:mysql://127.0.0.1:3306/mydb";  
    	public static final String name = "com.mysql.jdbc.Driver";  
    	public static final String user = "root";  
    	public static final String password = "root";  
  
    	public Connection conn = null;  
    	public PreparedStatement pst = null;  
  	
    	public DBHelper(String sql) {  
    	    try {  
    	        Class.forName(name);//指定连接类型  
    	        conn = DriverManager.getConnection(url, user, password);//获取连接  
    	        pst = conn.prepareStatement(sql);//准备执行语句  
    	    } catch (Exception e) {  
    	        e.printStackTrace();  
    	    }  
    	}  
  
    	public void close() {  
    	    try {  
    	        this.conn.close();  
    	        this.pst.close();  
    		    } catch (SQLException e) {  
    	        e.printStackTrace();  
    	    }  
    	}  
	}  
  
  
再写一个Demo.java来执行相关查询操作  

	package com.jdbc.demo;  
  
	import java.sql.ResultSet;  
	import java.sql.SQLException;  
  
	public class Demo {  
  
	    static String sql = null;  
	    static DBHelper db1 = null;  
	    static ResultSet ret = null;  
  
	    public static void main(String[] args) {  
	        sql = "select * from stuinfo";//SQL语句  
	        db1 = new DBHelper(sql);//创建DBHelper对象  
  
	        try {  
	            ret = db1.pst.executeQuery();//执行语句，得到结果集  
	            while (ret.next()) {  
	                String uid = ret.getInt("id");  
	                String ufname = ret.getString("name");  
	                String ulname = ret.getString("address");  
	                String udate = ret.getString(4);  
	                System.out.println(uid + "\t" + ufname + "\t" + ulname + "\t" + udate );  
	            }//显示数据  
	            ret.close();  
	            db1.close();//关闭连接  
	        } catch (SQLException e) {  
	            e.printStackTrace();  
	        }  
	    }  
  
	}  