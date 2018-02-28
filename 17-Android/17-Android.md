# Android 1  
<hr>  
  
## Android简单史
* 安卓之父 ： 安迪-鲁宾

## Android体系结构
![](https://i.imgur.com/Y3YPVaB.jpg)  

* Linux Kernel：我们知道Android其实就是一个操作系统，其底层是基于Linux Kernel的，这一层主要完成的是操作系统所具有的功能，比如这一层有许多的驱动程序，正是通过这些驱动程序来驱动我们设备上的硬件设备的。

* Android Runtime：Android的运行环境，我们学过java的都知道，java程序的运行需要java的核心包的支持，然后通过JVM虚拟机来运行我们的应用程序，这里Android Runtime里的Core Libraries就相当于java的JDK，是运行android应用程序所需要的核心库，Dalvik Virtual Machine就相当于JVM，这时Google专为Android开发的运行android应用程序所需的虚拟机。

* Liberaries：这里面都是Android的库文件，例如我们访问SQLite数据库的库文件等等。

* Application Framework：应用程序的框架，这个是非常的重要的，相信Framework这个词大家都应该非常的熟悉了，我们学习Android也主要学的就是这一层，我们通过这些各种各样的框架来实现我们的Application。

* Application：这个就是我们开发的Application了。  
  
Dalvik Virtual Machine : DVM  

![](https://i.imgur.com/FwmfnXV.png)  
  
![](https://i.imgur.com/z53sKgi.png)  
 
---  
  
### 清单文件
* package：应用在系统中的唯一识别 

### DDMS
* Dalvik debug monitor service

### 常用的adb指令：Android debug bridge：安卓调试桥
* adb start-server:启动adb进程
* adb kill-server：杀死adb进程
* adb devices：查看当前与开发环境连接的设备，此命令也可以启动adb进程
* adb install XXX.apk：往模拟器安装apk
* adb uninstall 包名：删除模拟器中的应用
* adb shell:进入linux命令行	
* ps：查看运行进程
* ls：查看当前目录下的文件结构
* netstat -ano：查看占用端口的进程  
  
--- 
  
## 布局介绍

* LinearLayout		(线性布局)
* RelativeLayout	(相对布局)
* AbsoluteLayout	(绝对布局)
* FrameLayout		(帧布局)
* TableLayout		(表格布局)

---
  
### 线性布局 LinearLayout

* 推荐dp
* 字体sp
* 像素px(不推荐) 

---

* 指定各个节点的排列方向

		android:orientation="horizontal"
* 设置右对齐

		android:layout_gravity="right"
* 当竖直布局时，只能左右对齐和水平居中，顶部底部对齐竖直居中无效

* 当水平布局时，只能顶部底部对齐和竖直居中

* 线性布局非常重要的一个属性：权重 --- __权重设置的是按比例分配剩余的空间__

		android:layout_weight="1"
通过设置控件的layout\_weight属性以控制各个控件在布局中的相对大小。
线性布局会根据该控件layout_weight值与其所处布局中所有控件weight值之和的比值为该控件分配占用的区域。  

### 相对布局 RelativeLayout
* 组件默认左对齐、顶部对齐
* 设置组件在指定组件的右边

		android:layout_toRightOf="@id/tv1"
* 设置在指定组件的下边

		android:layout_below="@id/tv1"
* 设置右对齐父元素

		android:layout_alignParentRight="true"
* 设置与指定组件右对齐

		android:layout_alignRight="@id/tv1"

* 组件竖直居中 

		android:layout_centerVertical="true"

### 帧布局
* 有特定的api要求必须使用帧布局
* 组件默认位置都是左上角，组件之间可以重叠
* 可以设置上下左右对齐，水平竖直居中，设置方式与线性布局一样  

		android:layout_gravity="bottom"  

### 表格布局 TableLayout
* 每个<TableRow/>节点是一行，它的每个子节点是一列
* 表格布局中的节点可以不设置宽高，因为设置了也无效
	* 根节点<TableLayout/>的子节点宽为匹配父元素，高为包裹内容
	* <TableRow/>节点的子节点宽为包裹内容，高为包裹内容
	* 以上默认属性无法修改
	* android:layout_column="1" //强制修改列索引
	* android:layout_span="2"   //设置当前列占用2列

* 根节点中可以设置以下属性，表示让第1列拉伸填满屏幕宽度的剩余空间

		android:stretchColumns="1"

### 绝对布局 AbsoluteLayout
* 直接指定组件的x、y坐标

		android:layout_x="144dp"
        android:layout_y="154dp"

---
## logcat
* 日志信息总共分为5个等级
	* verbose ：冗余，最低等级
	* debug ：调试
	* info ：正常等级的信息
	* warn ：警告
	* error ：错误
* 定义过滤器方便查看
* System.out.print输出的日志级别是info，tag是System.out
* Android提供的日志输出api
	
		Log.v(TAG, "加油吧，童鞋们");
		Log.d(TAG, "加油吧，童鞋们");
		Log.i(TAG, "加油吧，童鞋们");
		Log.w(TAG, "加油吧，童鞋们");
		Log.e(TAG, "加油吧，童鞋们");

---
## 在Android中读写程序

### 内部存储空间
* RAM内存：运行内存，相当于电脑的内存
* ROM内存：存储内存，相当于电脑的硬盘

### 外部存储空间
* SD卡：相当于电脑的移动硬盘
	* 2.2之前，sd卡路径：sdcard
	* 4.3之前，sd卡路径：mnt/sdcard
	* 4.3开始，sd卡路径：storage/sdcard
* SD卡：相当于电脑的移动硬盘
* 弹土司提示用户登录成功

		Toast.makeText(this, "登录成功", Toast.LENGTH_SHORT).show();

* 写sd卡需要权限

		<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
* 读sd卡，在4.0之前不需要权限，4.0之后可以设置为需要

		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>

* 使用api获得sd卡的真实路径，部分手机品牌会更改sd卡的路径

		Environment.getExternalStorageDirectory()
* 判断sd卡是否准备就绪

		if(Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED))

### 使用路径api读写文件
* getFilesDir()得到的file对象的路径是data/data/com.itheima.rwinrom2/files
	* 存放在这个路径下的文件，只要你不删，它就一直在
		File file = new File(getFilesDir(), "info.txt");
* getCacheDir()得到的file对象的路径是data/data/com.itheima.rwinrom2/cache
	* 存放在这个路径下的文件，当内存不足时，有可能被删除

* 系统管理应用界面的清除缓存，会清除cache文件夹下的东西，清除数据，会清除整个包名目录下的东西

---
### Linux文件的访问权限
* 在Android中，每一个应用是一个独立的用户
* drwxrwxrwx
* 第1位：d表示文件夹，-表示文件
* 第2-4位：rwx，表示这个文件的拥有者用户（owner）对该文件的权限
	* r：读
	* w：写
	* x：执行
* 第5-7位：rwx，表示跟文件拥有者用户同组的用户（grouper）对该文件的权限
* 第8-10位：rwx，表示其他用户组的用户（other）对该文件的权限  
  
----
### openFileOutput的四种模式
* MODE_PRIVATE：-rw-rw----
* MODE_APPEND:-rw-rw----
* MODE_WORLD_WRITEABLE:-rw-rw--w-
* MODE_WORLD_READABLE:-rw-rw-r--

---

### SharedPreference
>用SharedPreference存储账号密码

* 往SharedPreference里写数据

		//拿到一个SharedPreference对象
		SharedPreferences sp = getSharedPreferences("config", MODE_PRIVATE);
		//拿到编辑器
		Editor ed = sp.edit();
		//写数据
		ed.putString("name", name);
		ed.putString("password", password);
		ed.commit();

* 从SharedPreference里取数据

		SharedPreferences sp = getSharedPreferences("config", MODE_PRIVATE);
		//从SharedPreference里取数据
		String name = sp.getBoolean("name", "");

### 使用XMl序列化器生成xml文件
* 得到xml序列化器对象

		XmlSerializer xs = Xml.newSerializer();
* 给序列化器设置输出流

		File file = new File(Environment.getExternalStorageDirectory(), "backupsms.xml");
		FileOutputStream fos = new FileOutputStream(file);
		//指定用什么编码生成xml文件
		xs.setOutput(fos, "utf-8");
* 开始生成xml文件

		//指定头结点中enconding属性值
		xs.startDocument("utf-8", true);

		xs.startTag(null, "message");

		xs.text(sms.getData()...);

		xs.endTag(null, "message");

		//告诉序列化器生成完毕
		xs.endDocument();

--- 

### 拿到xml文件
		
		InputStream is = getClassLoader().getResourceAsStream("weather.xml");
### 拿到pull解析器

		XmlPullParser xp = Xml.newPullParser();

### 开始解析
* 拿到指针所在当前节点的事件类型

		int type = xp.getEventType();
* 事件类型主要有五种
	* START_DOCUMENT：xml头的事件类型
	* END_DOCUMENT：xml尾的事件类型
	* START_TAG：开始节点的事件类型
	* END_TAG：结束节点的事件类型
	* TEXT：文本节点的事件类型

如果获取到的事件类型不是END_DOCUMENT，就说明解析还没有完成，如果是，解析完成，while循环结束

	while(type != XmlPullParser.END_DOCUMENT) 

---

		public void click(View v){
			//获取到src文件夹下的资源文件
			InputStream is = getClassLoader().getResourceAsStream("weather.xml");
			
			//拿到pull解析器对象
			XmlPullParser xp = Xml.newPullParser();
			//初始化
			try {
				xp.setInput(is, "gbk");
				
				//获取当前节点的事件类型，通过事件类型的判断，我们可以知道当前节点是什么节点，从而确定我们应该做什么操作
				int type = xp.getEventType();
				City city = null;
				while(type != XmlPullParser.END_DOCUMENT){
					//根据节点的类型，要做不同的操作
					switch (type) {
					case XmlPullParser.START_TAG:
						//					获取当前节点的名字
						if("weather".equals(xp.getName())){
							//创建city集合对象，用于存放city的javabean
							cityList = new ArrayList<City>();
						}
						else if("city".equals(xp.getName())){
							//创建city的javabean对象
							city = new City();
						}
						else if("name".equals(xp.getName())){
							//				获取当前节点的下一个节点的文本
							String name = xp.nextText();
							city.setName(name);
						}
						else if("temp".equals(xp.getName())){
							//				获取当前节点的下一个节点的文本
							String temp = xp.nextText();
							city.setTemp(temp);
						}
						else if("pm".equals(xp.getName())){
							//				获取当前节点的下一个节点的文本
							String pm = xp.nextText();
							city.setPm(pm);
						}
						break;
					case XmlPullParser.END_TAG:
						if("city".equals(xp.getName())){
							//把city的javabean放入集合中
							cityList.add(city);
						}
						break;
	
					}
				
					//把指针移动到下一个节点，并返回该节点的事件类型
					type = xp.next();
				}
				
				for (City c : cityList) {
					System.out.println(c.toString());
				}
			} catch (Exception e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}

---


## 系统的层级架构  
  
整体架构组件，主要分为五层：  

* 应用层（Applications）
* 应用程序框架（Application Framework）
* 核心库与运行环境层（Libraries and Runtime）
* Linux Kernel 层（Linux 内核层）  
  
![](https://i.imgur.com/rAbXjF4.png)  
  
1.1.1 应用层
Android 的应用程序主要是用户界面（User Interface），通常以 JAVA 程序编写，其中还可以包含各种资源文件（放置在 res 目录中）。JAVA 程序及相关资源经过编译后，将生成一个 APK 包（Android Package的缩写，Android应用程序安装包的意思）。Android 本身提供了主屏幕（Home），联系人（Contact），电话（Phone），浏览器（Browsers）等众多的核心应用。同时应用程序的开发者还可以使用应用程序框架层的 API 实现自己的程序。

 

1.1.2 框架层
Android 的应用程序框架为应用程序层的开发者提供 APIs，它实际上是一个应用程序的框架。由于上层的应用程序是以 JAVA 构建的，因此本层次提供的首先包含了 UI 程序中所需要的各种控件： 例如： Views ( 视图组件 ) 包括 lists( 列表 ), grids( 栅格 ), text boxes( 文本框 ), buttons( 按钮 ) 等，甚至一个嵌入式的 Web 浏览器。一个 Android 的应用程序可以利用应用程序框架中的以下几个部分： Activity （活动）、Broadcast Intent Receiver （广播意图接收者）、Service （服务）、Content Provider （内容提供者）。

 

1.1.3 核心库与运行环境层
本层次对应一般嵌入式系统，相当于中间件层次。Android 的本层次分成两个部分一个是各种库，另一个是 Android 运行环境。本层的内容大多是使用 C++ 实现的。 在其中，各种库包括：

 

l C 库

C 语言的标准库，这也是系统中一个最为底层的库，C 库是通过 Linux 的系统调用来实现。

 

l 多媒体框架（Media Framework）

这部分内容是 Android 多媒体的核心部分，基于 PacketVideo（即 PV）的 OpenCORE，从功能上本库一共分为两大部分，一个部分是音频、视频的回放（Play Back），另一部分是则是音视频的纪录（Recorder）。

 

l SGL

2D 图像引擎。

 

l SSL

即 Secure Socket Layer 位于 TCP/IP 协议与各种应用层协议之间 , 为数据通讯提供安全支持。

 

l OpenGL ES 1.0 

本部分提供了对 3D 的支持。

 

l 界面管理工具（Surface Management）

本部分提供了对管理显示子系统等功能。

 

l SQLite

一个通用的嵌入式数据库

 

l WebKit

网络浏览器的核心

 

l FreeType

位图和矢量字体的功能。

 

Android 的各种库一般是以系统中间件的形式提供的，它们均有的一个显著特点就是与移动设备的平台的应用密切相关。 Android 运行环境主要指的虚拟机技术—— Dalvik。Dalvik 虚拟机和一般 JAVA 虚拟机（Java VM）不同，它执行的不是 JAVA 标准的字节码（bytecode ）而是 Dalvik 可执行格式（.dex）中执行文件。在执行的过程中，每一个应用程序即一个进程（Linux 的一个 Process）。 二者最大的区别在于 Java VM 是以基于栈的虚拟机（Stack-based），而 Dalvik 是基于寄存器的虚拟机（Register-based）。显然，后者最大的好处在于可以根据硬件实现更大的优化，这更适合移动设备的特点。

 

1.1.4 Linux内核层
Android 使用 Linux2.6 作为操作系统，Linux2.6 是一种标准的技术，Linux 也是一个开放的操作系统。Android 对操作系统的使用包括核心和驱动程序两部分，Android 的 Linux 核心为标准的 Linux2.6 内核，Android 更多的是需要一些与移动设备相关的驱动程序。主要的驱动如下所示：

 

l 显示驱动（Display Driver）

常用基于 Linux 的帧缓冲（Frame Buffer）驱动

 

l Flash 内存驱动（Flash Memory Driver）

 

l 照相机驱动（Camera Driver）

常用基于 Linux 的 v4l（Video for ）驱动。

 

l 音频驱动（Audio Driver）

常用基于 ALSA（Advanced Linux Sound Architecture，高级 Linux 声音体系）驱动

 

l WiFi 驱动（Camera Driver）

基于 IEEE 802.11 标准的驱动程序

 

l 键盘驱动（KeyBoard Driver）

 

l 蓝牙驱动（Bluetooth Driver）

Binder IPC 驱动：Andoid 一个特殊的驱动程序，具有单独的设备节点，提供进程间通讯的功能。

 

l Power Management（能源管理）  
  
1.1.4 Linux内核层
Android 使用 Linux2.6 作为操作系统，Linux2.6 是一种标准的技术，Linux 也是一个开放的操作系统。Android 对操作系统的使用包括核心和驱动程序两部分，Android 的 Linux 核心为标准的 Linux2.6 内核，Android 更多的是需要一些与移动设备相关的驱动程序。主要的驱动如下所示：

 

l 显示驱动（Display Driver）

常用基于 Linux 的帧缓冲（Frame Buffer）驱动

 

l Flash 内存驱动（Flash Memory Driver）

 

l 照相机驱动（Camera Driver）

常用基于 Linux 的 v4l（Video for ）驱动。

 

l 音频驱动（Audio Driver）

常用基于 ALSA（Advanced Linux Sound Architecture，高级 Linux 声音体系）驱动

 

l WiFi 驱动（Camera Driver）

基于 IEEE 802.11 标准的驱动程序

 

l 键盘驱动（KeyBoard Driver）

 

l 蓝牙驱动（Bluetooth Driver）

Binder IPC 驱动：Andoid 一个特殊的驱动程序，具有单独的设备节点，提供进程间通讯的功能。

 

l Power Management（能源管理）