# Android 2  
<hr>  
  
## 测试
* 黑盒测试
	* 测试逻辑业务
* 白盒测试
	* 测试逻辑方法

* 根据测试粒度
	* 方法测试：function test
	* 单元测试：unit test
	* 集成测试：integration test
	* 系统测试：system test

* 根据测试暴力程度
	* 冒烟测试：smoke test
	* 压力测试：pressure test

### 单元测试junit
* 定义一个类继承AndroidTestCase，在类中定义方法，即可测试该方法


* 在指定指令集时，targetPackage指定你要测试的应用的包名

		<instrumentation 
	    android:name="android.test.InstrumentationTestRunner"
		//指定该测试框架要测试哪一个项目
	    android:targetPackage="com.itheima.junit"
	    ></instrumentation>

* 定义使用的类库

		<uses-library android:name="android.test.runner"></uses-library>

* 断言的作用，检测运行结果和预期是否一致  
 
		assertEquals(8, result);//期望值，实际值
* 如果应用出现异常，会抛给测试框架

---

### SQLite数据库
* 轻量级关系型数据库
* 创建数据库需要使用的api：SQLiteOpenHelper
	* 必须定义一个构造方法：

			//arg1:数据库文件的名字
			//arg2:游标工厂 null
			//arg3:数据库版本
			public MyOpenHelper(Context context, String name, CursorFactory factory, int version){}
	* 数据库被创建时会调用：onCreate方法
	* 数据库升级时会调用：onUpgrade方法
