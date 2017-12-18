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
  
