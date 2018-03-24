# Android 6  
<hr>  
  
### 启动远程服务    

Android studio 快捷键   

	提取局部变量：Ctrl+Alt+V
	提取全局变量：Ctrl+Alt+F
	提取方法：Shit+Alt+M
  

####远程服务项目下    
在远程服务app的AndroidManifest.xml中定义service   
  
	<service android:name="com.yanbowen.remoteservice.RemoteService">
		<intent-filter >
			<action android:name="com.yanbowen.remote"/>
		</intent-filter>
	</service>

RemoteService.java类：  

	public class RemoteService extends Service {
		@Override
		public IBinder onBind(Intent intent) {
			// TODO Auto-generated method stub
			System.out.println("bind方法");
			return new furong();
		}

		class furong extends Stub{
			@Override
			public void qianXian() {
				// TODO Auto-generated method stub
				banzheng();
			}
		}
		public void banzheng(){
			System.out.println("李局帮你来办证");
		}
	}   
   
将抽取出来的中间人接口的后缀名改为aidl,随后将aidl文件复制到启动服务项目下即可。（注意：aidl的报名不可以改变）
  
####启动服务项目下    
  
	public class MainActivity extends AppCompatActivity {

    	private MyConnect myConnect;
    	IMyAidlInterface iMyAidlInterface;

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
    	    super.onCreate(savedInstanceState);
    	    setContentView(R.layout.activity_main);
    	    myConnect = new MyConnect();
    	}

    	public void qd(View v) {
    	    Intent intent = new Intent();
    	    intent.setAction("edu.android.myservice");
    	    intent.setPackage("edu.android.myaidl");
    	    startService(intent);
    	}

    	public void tz(View v) {
    	    Intent intent = new Intent();
    	    intent.setPackage("edu.android.myaidl");
    	    intent.setAction("edu.android.myservice");
    	    stopService(intent);
    	}

    	public void bd(View v) {
    	    Intent intent = new Intent();
    	    intent.setPackage("edu.android.myaidl");
    	    intent.setAction("edu.android.myservice");
    	    bindService(intent, myConnect, BIND_AUTO_CREATE);
    	}

    	public void jb(View v) {
    	    unbindService(myConnect);
    	}

    	public void ycbz(View view) {
    	    try {
    	        iMyAidlInterface.Qianxian();
    	    } catch (RemoteException e) {
    	        e.printStackTrace();
    	    }
    	}

    	class MyConnect implements ServiceConnection {

    	    @Override
    	    public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
    	        iMyAidlInterface = IMyAidlInterface.Stub.asInterface(iBinder);
    	    }

    	    @Override
    	    public void onServiceDisconnected(ComponentName componentName) {
	
    	    }
    	}
	}
   
---
  

  

	