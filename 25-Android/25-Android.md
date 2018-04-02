# Android 9  
<hr>  
  
## JNI(Java Native Interface,JAVA原生接口)   
问：为什么要进行交互？    

* 首先，Java语言提供的类库无法满足要求,且在数学运算,实时渲染的游戏上,音视频处理等方面上与C/C++相比效率稍低。 
* 然后，Java语言无法直接操作硬件，C/C++代码不仅能操作硬件而且还能发挥硬件最佳性能。
* 接着，使用Java调用本地的C/C++代码所写的库，省去了重复开发的麻烦，并且可以利用很多开源的库提高程序效率。

![](https://i.imgur.com/VNSx3SC.jpg)   
   
![](https://i.imgur.com/p4IXc2U.jpg)   

## 交叉编译
* 在一个平台下，编译出另一个平台能够执行的二进制的代码
* 平台：windows，mac os，linux
* 处理器：x86，arm，mips   

## 交叉编译的原理
* 源代码->编译->链接->可执行程序
* 模拟其他平台的特性  

## 交叉编译的工具链
* 多个工具的集合，一个工具使用完后接着调用下一个工具   

## 常见工具
* NDK：native developement kit：开发jni必备，就是模拟其他平台特性来编译代码的工具
* CDT：C/C++ developement tools：高亮显示c语言关键字
* cygwin：一个模拟器，可以再windows下运行linux指令   

## NDK目录结构
* docs:帮助文档
* build/tools：linux的批处理文件
* platforms：编译c代码需要使用的头文件和类库
* prebuilt：预编译使用的二进制可执行文件
* sample：jni的使用例子
* source：ndk的源码
* toolchains：工具链
* ndk-build.cmd:编译打包c代码的一个指令   

## 使用jni
1. 在项目根目录下创建jni文件夹
2. 在jni文件中创建一个c文件
3. 在java代码中，创建一个本地方法helloFromC

		public native String helloFromC();
4. 在jni中定义函数实现这个方法，函数名必须为

		jstring Java_com_itheima_helloworld1_MainActivity_helloFromC(JNIEnv* env, jobject obj)
5. 返回一个字符串，用c定义一个字符串

		char* cstr = "hello from c";
6. 把c的字符串转换成java的字符串

		jstring jstr = (*env)->NewStringUTF(env, cstr);
		return jstr；
7. 在jni中创建Android.mk文件
8. 在c文件中添加<jni.h>头文件
9. 在jni文件夹下执行ndk-build.cmd指令
10. java代码中加载so类库，调用本地方法