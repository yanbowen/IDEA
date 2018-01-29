# Android 3  
<hr>  
  
## ListView优化

### BaseAdapter
  
	public class MainActivity extends AppCompatActivity {

    	private static final String TAG = "MainActivity";
    	private MyOpenHelper oh;
    	private SQLiteDatabase db;
    	private List<Person> personList;

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
    	    super.onCreate(savedInstanceState);
    	    setContentView(R.layout.activity_main);
	
    	    oh = new MyOpenHelper(this, "person.db", null, 1);
    	    db = oh.getWritableDatabase();

	//        insertApi();
	        selectApi();

	        ListView listView = findViewById(R.id.lv);
	        listView.setAdapter(new BaseAdapter() {
	            //系统调用，获取多少条元素
	            @Override
	            public int getCount() {
	                return personList.size();
	            }
	
	            @Override
	            public View getView(int i, View view, ViewGroup viewGroup) {
	                Log.d(TAG, "getView: i" + i + " ;");
	                Person person = personList.get(i);
	                View v = null;
	                if (view == null) {
	                    //把布局文件填充成一个View
	                    v = View.inflate(MainActivity.this, R.layout.item_listview, null);
	                } else {
	                    v = view;
	                }
	
	                //通过资源ID查找组件，主要是View的ID
	                TextView tv_name = v.findViewById(R.id.tv_name);
    	            tv_name.setText(person.getName());
    	            TextView tv_phone = v.findViewById(R.id.tv_phone);
    	            tv_phone.setText(person.getTel());
    	            TextView tv_age = v.findViewById(R.id.tv_age);
    	            tv_age.setText(person.getAge());
	
    	            return v;
    	        }
	
    	        @Override
    	        public Object getItem(int i) {
	
    	            return null;
    	        }
	
    	        @Override
    	        public long getItemId(int i) {
    	            return 0;
    	        }
    	    });

	//        //第二种简便写法
	//        oh = new MyOpenHelper(this);
	//        db = oh.getWritableDatabase();
	//        insertApi();
    	}
	
    	@Override
    	protected void onDestroy() {
    	    super.onDestroy();
    	    db.close();
    	}

    	//插入数据，数据封装至ContentValues
    	public void insertApi() {
    	    for (int i = 0; i < 50; i++) {
    	        ContentValues values = new ContentValues();
    	        if (i % 2 == 0) {
    	            values.put("name", "郭靖" + i);
    	            values.put("sex", "男" + i);
    	        } else {
    	            values.put("name", "黄蓉" + i);
    	            values.put("sex", "女" + i);
    	        }
    	        values.put("age", 1 + i);
    	        values.put("Tel", i + 10080);
	
    	        //返回值是改行的主键，如果出错返回-1
    	        long insert = db.insert("person", null, values);
    	        if (insert != -1)
    	            Log.d(TAG, "insertApi: " + i + " 插入成功");
    	    }
    	}

    	//删除数据
    	public void deleteApi() {
    	    int i = db.delete("person", "name = ? and _id = ?", new String[]{"孔明", "2"});
	
    	}

    	public void selectApi() {
    	    personList = new ArrayList<Person>();
    	    Cursor cursor = db.query("person", null, null, null, null, null, null, null);
    	    while (cursor.moveToNext()) {
    	        String _id = cursor.getString(cursor.getColumnIndex("_id"));
    	        String name = cursor.getString(cursor.getColumnIndex("name"));
    	        String sex = cursor.getString(cursor.getColumnIndex("sex"));
    	        String age = cursor.getString(cursor.getColumnIndex("age"));
    	        String tel = cursor.getString(cursor.getColumnIndex("Tel"));
    	        Log.d(TAG, "selectApi--- name: " + name + "sex: " + sex + "age: " + age + "Tel: " + tel);

    	        Person person = new Person(_id, name, sex, age, tel);
    	        personList.add(person);
	
    	    }
    	}

    	public void updateApi() {
    	    ContentValues values = new ContentValues();
    	    values.put("name", "赵云");
    	    int i = db.update("person", values, "Tel = ?", new String[]{"10087"});
    	}

    	public void transaction() {
    	    try {
    	        //开启事物
    	        db.beginTransaction();
    	        ContentValues values = new ContentValues();
    	        values.put("Tel", 10010);
    	        db.update("person", values, "name = ?", new String[]{"司马昭"});
    	        values.clear();
    	        values.put("Tel", 360);
    	        db.update("person", values, "name = ?", new String[]{"司马懿"});
    	        //设置事物执行成功
    	    } finally {
    	        //关闭事物， 同时提交， 如果已经设置事物执行成功，sql生效
    	    }
    	}
	}

---
  
### ArrayAdapter

只能处理一种数据

	public class MainActivity extends AppCompatActivity {

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
	        super.onCreate(savedInstanceState);
	        setContentView(R.layout.activity_main);

	        String[] objects = new String[]{"司马懿", "司马师", "司马昭"};
	        ListView listView = findViewById(R.id.lv);
	        listView.setAdapter(new ArrayAdapter<String>(this, R.layout.item_listview, R.id.tv_name, objects));
	    }
	}

#### item_listview.xml 

	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">

	    <ImageView
	        android:id="@+id/iv_photo"
	        android:layout_width="60dp"
	        android:layout_height="60dp"
	        android:layout_gravity="center_vertical"
	        android:src="@mipmap/simayi"
	        />

	    <TextView
	        android:id="@+id/tv_name"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_gravity="center_vertical"
	        android:textSize="23sp"
	        android:text="名字"/>

	</LinearLayout>
  
![](https://i.imgur.com/zjvKCcB.png) 
  
---

### SimpleAdapter

能处理多种数据

	public class MainActivity extends AppCompatActivity {

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
    	    super.onCreate(savedInstanceState);
    	    setContentView(R.layout.activity_main);

    	    String[] objects = new String[]{"司马懿", "司马师", "司马昭"};
    	    ListView listView = findViewById(R.id.lv);

    	    //集合中每个元素都包含ListView条目需要的所有数据
    	    List<Map<String, Object>> data = new ArrayList<Map<String, Object>>();

    	    Map<String, Object> map1 = new HashMap<String, Object>();
    	    map1.put("photo", R.mipmap.simayi);
    	    map1.put("name", "司马懿");
    	    data.add(map1);

    	    Map<String, Object> map2 = new HashMap<String, Object>();
    	    map2.put("photo", R.mipmap.simashi);
    	    map2.put("name", "司马师");
    	    data.add(map2);

    	    Map<String, Object> map3 = new HashMap<String, Object>();
    	    map3.put("photo", R.mipmap.simazhao);
    	    map3.put("name", "司马昭");
    	    data.add(map3);

    	    listView.setAdapter(new SimpleAdapter(this, data, R.layout.item_listview, new String[]{"photo", "name"}, new int[]{R.id.iv_photo, R.id.tv_name}));
    	}
	}

![](https://i.imgur.com/Lh1MdE6.png)  

---

## 确定取消对话框  

    public void bt_confirm_cancel(View view) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setIcon(android.R.drawable.btn_dialog);
        builder.setTitle("退出");
        builder.setMessage("确定退出应用？");

        builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {

                onStop();
            }
        });
        builder.setNegativeButton("取消", new DialogInterface.OnClickListener() {
            @SuppressLint("WrongConstant")
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                Toast.makeText(MainActivity.this, "已取消！", 0).show();
            }
        });

        //使用创建器，生成一个对话框对象
        AlertDialog ad = builder.create();
        ad.show();
    }

![](https://i.imgur.com/I1f0n7V.jpg)

---

## 单选对话框

    public void bt_dx(View view) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setIcon(android.R.drawable.btn_radio);
        builder.setTitle("选择性别");
        final String[] items = new String[]{
                "男",
                "女"
        };
        builder.setSingleChoiceItems(items, -1, new DialogInterface.OnClickListener() {
            @SuppressLint("WrongConstant")
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                Toast.makeText(MainActivity.this, "您选择的是" + items[i], 0).show();
                //关闭对话框
                dialogInterface.dismiss();
            }
        });

        //使用创建器，生成一个对话框对象
        AlertDialog ad = builder.create();
        ad.show();
    }

![](https://i.imgur.com/JR09AoG.jpg)  
  
---

## 多选对话框

    public void bt_duoxuan(View view) {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setIcon(android.R.drawable.btn_radio);
        builder.setTitle("请选出亚洲国家");
        final String[] items = new String[]{
                "中国",
                "韩国",
                "美国",
                "新加坡",
                "日本"
        };
        final boolean[] checkedItems = new boolean[]{
                true,
                true,
                false,
                true,
                true
        };
        builder.setMultiChoiceItems(items, checkedItems, new DialogInterface.OnMultiChoiceClickListener() {
            @SuppressLint("WrongConstant")
            @Override
            public void onClick(DialogInterface dialogInterface, int i, boolean b) {
                checkedItems[i] = b;

            }
        });

        //设置确定取消按钮
        builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
            @SuppressLint("WrongConstant")
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                String text = " ";
                for (int n = 0; n < items.length; n++) {
                    text += checkedItems[n] ? items[n]+" " : "";
                }
                Toast.makeText(MainActivity.this, "您选择的是" + text, 0).show();
                dialogInterface.dismiss();
            }
        });

        //使用创建器，生成一个对话框对象
        AlertDialog ad = builder.create();
        ad.show();
    }