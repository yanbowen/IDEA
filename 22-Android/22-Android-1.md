# Android 6  
<hr>  
  
## 广播
* 广播的概念
	* 现实：电台通过发送广播发布消息，买个收音机，就能收听
	* Android：系统在产生某个事件时发送广播，应用程序使用广播接收者接收这个广播，就知道系统产生了什么事件。
Android系统在运行的过程中，会产生很多事件，比如开机、电量改变、收发短信、拨打电话、屏幕解锁  
  
### 广播的两种类型
* 无序广播：所有跟广播的intent匹配的广播接收者都可以收到该广播，并且是没有先后顺序（同时收到）
* 有序广播：所有跟广播的intent匹配的广播接收者都可以收到该广播，但是会按照广播接收者的优先级来决定接收的先后顺序
	* 优先级的定义：-1000~1000
	* 最终接收者：所有广播接收者都接收到广播之后，它才接收，并且一定会接收
	* abortBroadCast：阻止其他接收者接收这条广播，类似拦截，只有有序广播可以被拦截  
  
  
## 服务  
### 开启方式
* startService
	* 该方法启动的服务所在的进程属于服务进程
	* Activity一旦启动服务，服务就跟Activity一毛钱关系也没有了
* bindService
	* 该方法启动的服务所在进程不属于服务进程
	* Activity与服务建立连接，Activity一旦死亡，服务也会死亡

* 服务的混合调用
	* 先开始、再绑定，先解绑、再停止
* 就是默默运行在后台的组件，可以理解为是没有前台的activity，适合用来运行不需要前台界面的代码
* 服务可以被手动关闭，不会重启，但是如果被自动关闭，内存充足就会重启
* startService启动服务的生命周期
	* onCreate-onStartCommand-onDestroy
* 重复的调用startService会导致onStartCommand被重复调用   
  
### 服务两种启动方式
* startService：服务被启动之后，跟启动它的组件没有一毛钱关系
* bindService：跟启动它的组件同生共死
* 绑定服务和解绑服务的生命周期方法：onCreate->onBind->onUnbind->onDestroy  

* 绑定服务时，会触发服务的onBind方法，此方法会返回一个Ibinder的对象给MainActivity，通过这个对象访问服务中的方法
* 绑定服务

		Intent intent = new Intent(this, BanZhengService.class);
    	bindService(intent, conn, BIND_AUTO_CREATE);
* 绑定服务时要求传入一个ServiceConnection实现类的对象
* 定义这个实现类

		class MyServiceconn implements ServiceConnection{
		@Override
		public void onServiceConnected(ComponentName name, IBinder service) {
			zjr = (PublicBusiness) service;
		}
		@Override
		public void onServiceDisconnected(ComponentName name) {	
		}
    	
    }
* 创建实现类对象

		 conn = new MyServiceconn();
* 在服务中定义一个类实现Ibinder接口，以在onBind方法中返回

		class ZhongJianRen extends Binder implements PublicBusiness{
			public void QianXian(){
				//访问服务中的banZheng方法
				BanZheng();
			}	
			public void daMaJiang(){
			
			}
		}  

* 把QianXian方法抽取到接口PublicBusiness中定义    

---  
  
### 两种启动方法混合使用
* 用服务实现音乐播放时，因为音乐播放必须运行在服务进程中，可是音乐服务中的方法，需要被前台Activity所调用，所以需要混合启动音乐服务
* 先start，再bind，销毁时先unbind，在stop  

---  

#找领导办证
* 把服务看成一个领导，服务中有一个banZheng方法，如何才能访问？
* 绑定服务时，会触发服务的onBind方法，此方法会返回一个Ibinder的对象给MainActivity，通过这个对象访问服务中的方法
* 绑定服务

		Intent intent = new Intent(this, BanZhengService.class);
    	bindService(intent, conn, BIND_AUTO_CREATE);
* 绑定服务时要求传入一个ServiceConnection实现类的对象
* 定义这个实现类

		class MyServiceconn implements ServiceConnection{
		//连接服务成功，此方法调用
		@Override
		public void onServiceConnected(ComponentName name, IBinder service) {
			zjr = (PublicBusiness) service;
		}
		@Override
		public void onServiceDisconnected(ComponentName name) {	
		}
    	
    }
* 创建实现类对象

		 conn = new MyServiceconn();
* 在服务中定义一个类实现Ibinder接口，以在onBind方法中返回

		class ZhongJianRen extends Binder implements PublicBusiness{
		public void QianXian(){
			//访问服务中的banZheng方法
			BanZheng();
		}	
		public void daMaJiang(){
			
		}
	}
* 把QianXian方法抽取到接口PublicBusiness中定义  
  
---  
  
### MainActivity.java类
  
	public class MainActivity extends Activity {

    private Intent intent;
	private MyServiceConn conn;
	PublicBusiness pb;
	
	@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        intent = new Intent(this, LeaderService.class);
        conn = new MyServiceConn();
        //绑定领导服务
        bindService(intent, conn, BIND_AUTO_CREATE);
    }
    
    public void click(View v){
    	//调用服务的办证方法
    	pb.QianXian();
    }

    class MyServiceConn implements ServiceConnection{

    	//连接服务成功，此方法调用
		@Override
		public void onServiceConnected(ComponentName name, IBinder service) {
			// TODO Auto-generated method stub
			pb = (PublicBusiness) service;
		}

		@Override
		public void onServiceDisconnected(ComponentName name) {
			// TODO Auto-generated method stub
			
		}
    	
    }
    
	}  
  
### LeaderService.java类  
  
	public class LeaderService extends Service {

		@Override
		public IBinder onBind(Intent intent) {
			// 返回一个Binder对象，这个对象就是中间人对象
			return new ZhouMi();
		}

		class ZhouMi extends Binder implements PublicBusiness{
			public void QianXian(){
				banZheng();
			}
		
			public  void daMaJiang(){
				System.out.println("陪李处打麻将");
			}
		}
	
		public void banZheng(){
			System.out.println("李处帮你来办证");
		}
	}  
  
### PublicBusiness.java类   
  
	public interface PublicBusiness {

		void QianXian();
	}  
  
### 服务的分类
* 本地服务：指的是服务和启动服务的activity在同一个进程中
* 远程服务：指的是服务和启动服务的activity不在同一个进程中  

### AIDL
* Android interface definition language
* 安卓接口定义语言
* 作用：跨进程通信
* 应用场景：远程服务中的中间人对象，其他应用是拿不到的，那么在通过绑定服务获取中间人对象时，就无法强制转换，使用aidl，就可以在其他应用中拿到中间人类所实现的接口  

### 支付宝远程服务
1. 定义支付宝的服务，在服务中定义pay方法
2. 定义中间人对象，把pay方法抽取成接口
3. 把抽取出来的接口后缀名改成aidl
4. 中间人对象直接继承Stub对象
5. 注册这个支付宝服务，定义它的intent-Filter

### 需要支付的应用
1. 把刚才定义好的aidl文件拷贝过来，注意aidl文件所在的包名必须跟原包名一致
2. 远程绑定支付宝的服务，通过onServiceConnected方法我们可以拿到中间人对象
3. 把中间人对象通过Stub.asInterface方法强转成定义了pay方法的接口
4. 调用中间人的pay方法