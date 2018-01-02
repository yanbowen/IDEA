# Android  
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

