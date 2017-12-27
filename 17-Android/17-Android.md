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
  
### 线性布局

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

