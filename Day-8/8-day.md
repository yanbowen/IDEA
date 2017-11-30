# Java Web之servlet  
<hr>

## Servlet   
* 处理从客户端发送的请求及服务端的响应。  
![](https://i.imgur.com/AntGypW.png)  

### Servlet生命周期    
* public void init(ServletConfig) ; 初始化方法  
* public service(ServletRequest,ServletResponse) ; 服务方法  
* public destroy() ;  销毁方法  

	默认情况下,servlet对象在第一次请求的时候调用构造函数创建， 创建之后自动调用带参的init方法，然后调用service方法.destroy方法在停止服务器或者停止应用的时候调用。整个过程中，init方法和destroy方法只会调用一次，而service方法会反复调用。  
	可以通过配置web.xml文件来改变创建servlet的时机.配置如下（就是可以不用客户访问的时候直接就创建，也就是控制servlet里面的创建时间）  
![](https://i.imgur.com/4Orrng8.png)  
  	此时在服务器启动的时候就创建对象并进行初始化了.此Servlet对象在服务器停止或者应用停止时才死亡.   
  
#### url配置(掌握)  
![](https://i.imgur.com/ffbqFSL.png)  
![](https://i.imgur.com/v59QlbZ.png)  

*  配置优先级：  精确匹配  > 以/开头的匹配 > 以 * 开头的匹配  
*  如果配置成/ 那么就是一个缺省的servlet，此Servlet处理所有找不到匹配路径的url  

#### servlet的创建问题(掌握)  
创建一个servlet有3中方式:  

* 配采用实现servlet接口, （不推荐）  
* 采用继承GenericServlet类( 不推荐)  
* 采用继承HttpServlet(推荐)   
  
 
#### serlvet的线程安全(明白)  
* 明确： Servlet的设计是一个单实例多线程。  
* 线程安全要求将变量创建成一个局部变量，而不要创建成实例变量.   
  

#### ServletContext (非常重要)  
  
1.	生命周期很长
2.	每个web应用都有一个唯一的servletContext对象.
3.	在每个应用加载的时候，服务器就会创建servletContext对象。
4.	ServletContext对象是一个域对象(领域)
5.	获得servletContext的方式  
![](https://i.imgur.com/sTIf9Qn.png)  
6.	应用
	1.	url的写法注意：  
		* 客户端跳转:(由浏览器发出的请求)  一定需要在地址前加应用的名称  
		* 服务端跳转: (由服务端发出的请求)  不需要在地址前加应用的名称
	2.	应用1
		* 作为域对象，里面存取的是键值对，可以拿
		* 可以修改，所以一般保存的是公用数据
		* Cookie就是用来保存私有数据
		* 生命周期长，所以里面保存东西少点，
	3.	应用
		* 实现数据共享
		* 获取全局配置参数
		* 请求转发：拿取请求转发器，然后转发
		* 获取资源文件
  
三种方式优缺点:   

* 采用servletContext对象获得.  
	* 优点： 任意文件，任意路径都可获得
	* 缺点： 必须在web环境下
* 采用resourceBundle获得
	* 优点： 非web环境下
	* 缺点： 只能获取properties文件
* 采用类加载器获得
	* 优点： 任意路径,任意文件
     
#### ResourceBundle对象  
专门获取properties文件信息  

	ResourceBundle rb = ResourceBundle.getBundle("p1");//src下开始    
  
#### 类加载器获取资源  
  
	//获取类加载器。
	//3种方式
	//1.通过类名  			ServletContext7.class.getClassLoader()
	//2.通过对象  			this.getClass().getClassLoader()
	//3.Class.forName()		获取Class.forName("ServletContext7").getClassLoader()  
  
