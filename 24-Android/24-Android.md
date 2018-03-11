# Android 8  
<hr>  
  
## 内容提供者 ContentProvider

* 应用的数据库是不允许其他应用访问的
* 内容提供者的作用就是让别的应用访问到你的数据库
* 自定义内容提供者，继承ContentProvider类，重写增删改查方法，在方法中写增删改查数据库的代码，举例增方法

		@Override
		public Uri insert(Uri uri, ContentValues values) {
			db.insert("person", null, values);
			return uri;
		}
* 在清单文件中定义内容提供者的标签，注意必须要有authorities属性，这是内容提供者的主机名，功能类似地址

		<provider android:name="com.itheima.contentprovider.PersonProvider"
            android:authorities="com.itheima.person"
            android:exported="true"
         ></provider>

* 创建一个其他应用，访问自定义的内容提供者，实现对数据库的插入操作

		public void click(View v){
			//得到内容分解器对象
			ContentResolver cr = getContentResolver();
			ContentValues cv = new ContentValues();
			cv.put("name", "小方");
			cv.put("phone", 138856);
			cv.put("money", 3000);
			//url:内容提供者的主机名
			cr.insert(Uri.parse("content://com.itheima.person"), cv);
		}

###UriMatcher  
	UriMatcher um = new UriMatcher(UriMatcher.NO_MATCH);

* 用于判断一条uri跟指定的多条uri中的哪条匹配
* 添加匹配规则

		//指定多条uri
		um.addURI("com.itheima.person", "person", PERSON_CODE);  // content://com.itheima.person/person
		um.addURI("com.itheima.person", "company", COMPANY_CODE);// content://com.itheima.person/company
		//#号可以代表任意数字
		um.addURI("com.itheima.person", "person/#", QUERY_ONE_PERSON_CODE);
* 通过Uri匹配器可以实现操作不同的表

		@Override
		public Uri insert(Uri uri, ContentValues values) {
			if(um.match(uri) == PERSON_CODE){
				db.insert("person", null, values);
			}
			else if(um.match(uri) == COMPANY_CODE){
				db.insert("company", null, values);
			}
			else{
				throw new IllegalArgumentException();
			}
			return uri;
		}
* 如果路径中带有数字，把数字提取出来的api

		int id = (int) ContentUris.parseId(uri);  
  
---  
  
