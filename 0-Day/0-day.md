<center>  

# www.yanbowen.cn  

<hr width = "50%">  

## 网站建设-部署与发布  

</center>    

---  

### 建站的基本步骤  
#### 用户访问网站的过程  
* 在浏览器上输入域名，如：http://www.yanbowen.cn  
* 浏览器自动调用DNS（域名服务）将域名解析为IP地址
* 浏览器通过IP地址找到网站的服务器
* 服务器返回网页至浏览器  
  
![](https://i.imgur.com/UPyU2pH.jpg)  
  
![](https://i.imgur.com/Pdo4tT9.jpg)  
  
### 获取web项目的绝对路径的方法总结  
  
	一、用Jsp获取

	 1、获取文件的绝对路径
	String file="文件";（例如：data.mdb）
	String path=application.getRealPath(file);

	结果：
	E:\java_web\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\myWebsite\文件

	2、获取文件的绝对路径
	String p2=request.getRequestURI();

	结果：
	E:\java_web\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\myWebsite\文件
	
	3、获取当前jsp页面的路径
	String p3=request.getContextPath(); 

	结果：
	/myWebsite/index.jsp

	4、获取当前项目的路径
	String p4=request.getServletPath(); 

	结果：
	/myWebsite

	二、用Java类获取

	1、获取Eclipse路径
	String a1=System.getProperty("user.dir");

	结果：
	D:\StudySystem\JavaWeb\3-eclipse-jee-indigo-win32\eclipse

	2、获取当前的classpath路径
	String a2=类名.class.getResource("").toString();
	String a3=DBConnection.class.getResource("/").toString();
	String a4=DBConnection.class.getClassLoader().getResource("").toString();
	String t=Thread.currentThread().getContextClassLoader().getResource("").getPath();

	打印出来分别是：

	file:/E:/java_web/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/myWebsite/WEB-INF/classes/com/site/db/

	file:/E:/java_web/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/myWebsite/WEB-INF/classes/

	file:/E:/java_web/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/myWebsite/WEB-INF/classes/

	/E:/java_web/workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps/myWebsite/WEB-INF/classes/

 

	3、获取文件的绝对路径
	如果要获取WebContent目录下的文件绝对路径怎么办？可以用下面的方法
	String t=Thread.currentThread().getContextClassLoader().getResource("").getPath(); 
	int num=t.indexOf(".metadata");
	String path=t.substring(1,num).replace('/', '\\')+"项目名\\WebContent\\文件";

	结果是：
	E:\java_web\workspace\项目名\WebContent\文件

	三、用servlet获取

	1、获取项目的绝对路径
	request.getSession().getServletContext().getRealPath("")
	
	结果：
	E:\java_web\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\myWebsite

	2、获取浏览器地址
	request.getRequestURL()

	结果：
	http://localhost:8080/myWebsite/QuestionServlet

	3、获取当前文件的绝对路径
	request.getSession().getServletContext().getRealPath(request.getRequestURI())

	结果：
	E:\java_web\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\myWebsite\myWebsite\QuestionServlet  
  
