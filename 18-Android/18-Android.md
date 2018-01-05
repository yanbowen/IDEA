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

### 创建数据库

	//创建OpenHelper对象
	MyOpenHelper oh = new MyOpenHelper(getContext(), "person.db", null, 1);
	//获得数据库对象,如果数据库不存在，先创建数据库，后获得，如果存在，则直接获得
	SQLiteDatabase db = oh.getWritableDatabase();

* getWritableDatabase()：打开可读写的数据库
* getReadableDatabase()：在磁盘空间不足时打开只读数据库，否则打开可读写数据库
* 在创建数据库时创建表

		public void onCreate(SQLiteDatabase db) {
			// TODO Auto-generated method stub
			db.execSQL("create table person (_id integer primary key autoincrement, name char(10), phone char(20), money integer(20))");
			db.close();
		}

---

### 数据库的增删改查SQL语句

* insert into person (name, phone, money) values ('张三', '159874611', 2000);
* delete from person where name = '李四' and _id = 4;
* update person set money = 6000 where name = '李四';
* select name, phone from person where name = '张三';

### 执行SQL语句实现增删改查

	//插入
	db.execSQL("insert into person (name, phone, money) values (?, ?, ?);", new Object[]{"张三", 15987461, 75000});
	//查找
	Cursor cs = db.rawQuery("select _id, name, money from person where name = ?;", new String[]{"张三"});

测试方法执行前会调用此方法


	protected void setUp() throws Exception {
		super.setUp();
		//获取虚拟上下文对象
		oh = new MyOpenHelper(getContext(), "people.db", null, 1);
	}

### 使用api实现增删改查
* 插入

		//以键值对的形式保存要存入数据库的数据
		ContentValues cv = new ContentValues();
		cv.put("name", "刘能");
		cv.put("phone", 1651646);
		cv.put("money", 3500);
		//返回值是改行的主键，如果出错返回-1
		long i = db.insert("person", null, cv);
* 删除

		//返回值是删除的行数
		int i = db.delete("person", "_id = ? and name = ?", new String[]{"1", "张三"});
* 修改
	
		ContentValues cv = new ContentValues();
		cv.put("money", 25000);
		int i = db.update("person", cv, "name = ?", new String[]{"赵四"});
* 查询

		//arg1:要查询的字段
		//arg2：查询条件
		//arg3:填充查询条件的占位符
		Cursor cs = db.query("person", new String[]{"name", "money"}, "name = ?", new String[]{"张三"}, null, null, null);
		while(cs.moveToNext()){
			//							获取指定列的索引值
			String name = cs.getString(cs.getColumnIndex("name"));
			String money = cs.getString(cs.getColumnIndex("money"));
			System.out.println(name + ";" + money);
		}

---

### 事务
* 保证多条SQL语句要么同时成功，要么同时失败
* 最常见案例：银行转账
* 事务api

		try {
			//开启事务
			db.beginTransaction();
			ContentValues values = new ContentValues();
			values.put("salary", 13000);
			db.update("person", values, "name = ?", new String[]{"小志"});

			values.clear();
			values.put("salary", 15000);
			db.update("person", values, "name = ?", new String[]{"小志的儿子"});
			
			//设置事务执行成功
			db.setTransactionSuccessful();
		} finally{
			//关闭事务
			//如果此时已经设置事务执行成功，则sql语句生效，否则不生效
			db.endTransaction();
		}

---

### 分页查询

		//从第0页开始查询10页
		Cursor cs = db.query("person", null, null, null, null, null, null, "0, 10");

---

### ListView
* 就是用来显示一行一行的条目的
* MVC结构
	* M：model模型层，要显示的数据           ———————people集合  ------ javaBean
	* V：view视图层，用户看到的界面          ———————ListView    ---------- jsp 
	* C：control控制层，操作数据如何显示     —————adapter对象  ---- servlet
