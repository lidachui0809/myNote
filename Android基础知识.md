Android基础知识

1. 布局管理器

   1. 相对布局管理器(RelativeLayout)

      1. ```xml
         <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
             xmlns:app="http://schemas.android.com/apk/res-auto"
             xmlns:tools="http://schemas.android.com/tools"
             android:layout_width="match_parent"
             android:layout_height="match_parent"   //与父容器相同
             android:gravity="center|bottom"		//设置布局位置为中间底部位置 | 可以增加控件位置的布局
             tools:context=".MainActivity">
             android:gravity="center|bottom"
         
             <TextView
                 android:id="@+id/user_2"					//设置控件单独id,不可重复
                 android:layout_width="wrap_content"			//适应内容修改大小
                 android:layout_height="wrap_content"		
                 android:text="Hello World!"
                 android:layout_centerInParent="true" />	    //layout_centerInParent 为布尔值
         
             <Button
                 android:id="@+id/user_1"				
                 android:layout_width="100dp"				//设置控件的大小
                 android:layout_height="50dp"
         	    android:layout_below="@id/user_2"	 		//使用layout_below属性，可以控制控件位于那个对象的后方
                 android:layout_alignParentLeft="true"
                 android:layout_marginTop="20dp" 	//控件得顶部与另一控件得间距
                 android:text="你好，世界！" />
         
         </RelativeLayout>
         ```

         

   2. 线性布局管理器( LinearLayout )

      1. 特有属性

         1. ```xml
             android:orientation="vertical/horizontal"  //设置控件布局为垂直线性分布
             andorid:layout_weight="1"  
             //该属性一般用在子控件中，用来设置控件占剩余空间的比例大小，即将剩余的空间平均分割，默认值为0
            ```

   3. 帧布局管理器 （FrameLayout） （多用于需要层叠时使用）

      1. 特有属性

         1. ```
            android:foreground //设置前景图像(始终位于最上层的图像)
            android:foregroundGravity //设置前景图片的位置
            ```

   4. 表格布局管理器 (TableLayout)   (每增加一个组件，该行就增加一列 ，可跨列显示)

      1. 特有属性

         1. ```
            <TableRow/> 				//增加行数
            android:stretchColumns="1"   //设置可以修改自身大小的列(最小索引为0)
            android:collapseColumns="1" //隐藏该列的内容
            ```

   5. 网格布局管理器(GridLayout)  (与表格布局管理器类似，**可跨列，跨行**)

      1. 特有属性

         1. ```
               android:columnCount="2"		//设置网格的列数的最大值为2
               android:rowCount="1"			//设置网格的行数最大为1，超过时将自动转行
               android:orientation="horizontal"  //设置网格的排列方向
               LayoutParme					//内部类。里面有许多属性
            ```

   6. padding 内边距 margin 外边距

   7. 时间类(Java)

      1. 设置时间样式

         1. ```java
            SHORT：完全为数字，如 12.5.10 或 5:30pm。
            MEDIUM：较长，如 May 10，2016。
            LONG：更长，如 May 12，2016 或 11:15:32am。
            FULL：是完全指定，如 Tuesday、May 10、2012 AD 或 11:l5:42am CST。
            
            //预览效果
            SHORT：18-10-15 上午9:30
            FULL：2018年10月15日 星期一 上午09时30分43秒 CST
            MEDIUM：2018-10-15 9:30:43
            LONG：2018年10月15日 上午09时30分43秒
            
            // 获取不同格式化风格和中国环境的日期
            DateFormat df1 = DateFormat.getDateInstance(DateFormat.SHORT, Locale.CHINA);
            DateFormat df2 = DateFormat.getDateInstance(DateFormat.FULL, Locale.CHINA);
            df1.format(mCrime.getDate());
            
            // 创建日期格式化对象,在获取格式化对象时可以指定风格  
            DateFormat df = new SimpleDateFormat("yyyy年MM月dd日");  
            DateFormat df = new SimpleDateFormat("yyyy年MM月dd日");
            String str = "2018年12月11日";
            Date date = df.parse(str);  
            
            // 将不同格式化风格的日期格式化为日期字符串
            String date1 = df1.format(new Date());
            String date2 = df2.format(new Date());
            
            // 输出日期
            System.out.println("SHORT：" + date1 + " " + time1);
            System.out.println("FULL：" + date2 + " " + time2);
            
            ```

      2. Date与Calendar

         1. ```java
            //Date 类主要封装了系统的日期和时间的信息，Calendar 类则会根据系统的日历来解释 Date 对象
            
            //Date 类表示系统特定的时间戳，可以精确到毫秒。Date 对象表示时间的默认顺序是星期、月、日、小时、分、秒、年
            
            //Calendar 类是一个抽象类，它为特定瞬间与 YEAR、MONTH、DAY_OF—MONTH、HOUR 等日历字段之间的转换提供了一些方 	法，并为操作日历字段（如获得下星期的日期） 提供了一些方法
            
            //创建 Calendar 对象不能使用 new 关键字，因为 Calendar 类是一个抽象类，但是它提供了一个 getInstance() 方法	来获得 Calendar类的对象。getInstance() 方法返回一个 Calendar 对象，其日历字段已由当前日期和时间初始化
            ```

         2. 详细介绍链接

            [http://c.biancheng.net/view/876.html#:~:text=%E5%9C%A8%20Java%20%E4%B8%AD%E8%8E%B7%E5%8F%96%E5%BD%93%E5%89%8D%E6%97%B6%E9%97%B4%EF%BC%8C%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%20java.util.Date%20%E7%B1%BB%E5%92%8C%20java.util.Calendar%20%E7%B1%BB%E5%AE%8C%E6%88%90%E3%80%82,%E5%85%B6%E4%B8%AD%EF%BC%8C%20Date%20%E7%B1%BB%E4%B8%BB%E8%A6%81%E5%B0%81%E8%A3%85%E4%BA%86%E7%B3%BB%E7%BB%9F%E7%9A%84%E6%97%A5%E6%9C%9F%E5%92%8C%E6%97%B6%E9%97%B4%E7%9A%84%E4%BF%A1%E6%81%AF%EF%BC%8CCalendar%20%E7%B1%BB%E5%88%99%E4%BC%9A%E6%A0%B9%E6%8D%AE%E7%B3%BB%E7%BB%9F%E7%9A%84%E6%97%A5%E5%8E%86%E6%9D%A5%E8%A7%A3%E9%87%8A%20Date%20%E5%AF%B9%E8%B1%A1%20%E3%80%82]: 

            

   8. android:exported属性

      1. ```java
         属性存在于四大组件中
         
         //作用
         该属性用来标示，其它应用的组件是否可以唤醒service或者和这个service进行交互：true可以，false不可以。如果为false，只有同一个应用的组件或者有着同样user ID的应用可以启动这个service或者绑定这个service。
         
         默认值根据当前service是否有intent filter来定。如果没有任何filter意味着当前service只有在被详细的描述class name后才会被唤醒。这意味这当前service只能在应用内部使用（因为其它应用不知道这个class name）.所以在这种情况下它的默认值为 false.从另一方面讲，如果至少有一个filter的话那么就意味着这个service可以被外部应用使用，这种情况下默认值为true。
         ```

   9. 两不同组件(Activity)之间传递数据

      1. ```java
         通过Intent或者Bundle对象存储数据，通过
         调用者使用
         Fragment.startActivityForResult(Intent 存储数据的Intent对象,int 请求码) 或
         Activity.startActivityForResult(Intent 存储数据的Intent对象,int 请求码) 
         
         被调用者 一般在被调用者销毁时调用onDestory()
         setResult(int resultCode,Intent 需要传回给调用者的Intent对象) 《里面一般存有调用者想要的数据》
         getActivity().setResult(int resultCode,Intent 需要传回给调用者的Intent对象)
         //fragment只能够从activity中接收返回结果，但其自身无法持有返回结果
         
         ```
         
      2. 

   10. RecyclerView类相关方法

          1. ```java
                mCrimeIndexOf=mRecyclerView.getChildAdapterPosition(view);
                mCrimeIndexOf=(RecyclerView.ViewHolder) holder.getAdapterPosition();
                
                //刷新视图列表项
                recyclerViewAdapter.notifyItemChanged(mCrimeIndexOf);//指定某个位置的view
                 recyclerViewAdapter.notifyDataSetChanged(); //指定可见范围内的所有视图	
                ```

                

   11. 知识盲点

          1. ```java
                //设备配置改变时，具有ID属性的视图可以保存运行状态,即值不会发生改变
                //时间戳：系统根据当前系统时间随机生成的一串数字，可以保证数字的唯一性
                ```

                

   12. 数据储存

       1. SharedPreferences (可以实在自动登录，将用户信息预存在文件中，随应用存在)

          1. SharedPreferences对象用来获得数据，SharedPreferences.Edit对象用来编辑数据 <Map映射存储模式>

          2. ```java
              mSharedPreferences=getSharedPreferences(FILE_NAME,MODE_PRIVATE);//SharePreference用来获得数据,可以在程序启动时，获得对象之后获取属性
              /*文件名，访问权限*/
              mEditor=mSharedPreferences.edit();//获得edit对象,用来编辑数据
              mSharedPreferences.getString(NAME,"")//存入数据
              /* 键-值 */    
              mSharedPreferences.getString(NAME,"")//获取数据    
             ```

             

       2. 内部存储（Internal Storage）

          1. FileOutputStream	(**保存文件信息**)

             1. ```java
                	FileOutputStream fileOutputStream = null;
                      try {
                          //直接创建文件
                 		   // FileOutputStream fileOutputStream=new FileOutputStream("test.txt");
                          fileOutputStream = openFileOutput(FILE_NAME, MODE_PRIVATE);
                          // MODE_PRIVATE 默认访问方式，文件仅能被创建应用程序访问。
                          //查找该文件，存在使用，不存在创建
                          fileOutputStream.write(content.getBytes());
                          //将文件保存在流中
                      } catch (Exception e) {
                          e.printStackTrace();
                      } finally {
                          try {
                              fileOutputStream.close();//文件流关闭在finally中关闭
                          } catch (IOException e) {
                              e.printStackTrace();
                          }
                      }
                ```

                

          2. FlieInputStream    (**读取文件信息**)

             1. ```java
                	FileInputStream fileInputStream=null;
                      try{
                          fileInputStream=openFileInput(FILE_NAME);
                          byte[] buff=new byte[fileInputStream.available()];
                          //fileInputStream.available() 
                          //返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取的字节数
                          StringBuffer sb=new StringBuffer("");//使用StringBuffer减少内存消耗
                          int length;
                          方法一：
                          while((length=fileInputStream.read(buff))!=0){
                              //read从流中获得传入buff.length的字节，文件末尾返回-1
                              /*
                              把文件中的字节信息复制到buff数组中，buff的数组长度用于限制每次获取字节的长度，
                              当达到buff最大长度是，会把字节长度赋值给lenth，再通过append方法将字节数组转换为
                              String
                              */
                              sb.append(new String(buff,0,length));
                          }
                          
                          方法二：
                              fileInputStream.read(buff);//读取文件中的信息
                              return new String(buff);//将byte对象转换为String对象
                          
                          return sb.toString();
                      }catch (Exception e){
                          e.printStackTrace();
                    }
                    return null;
                ```

                

       3. 外部存储（External Storage）如：sd卡

          1. ```java
             file = new File(Environment.getExternalStorageDirectory(), "Text.text");  //设置存储sd卡根目录
             FileOutputStream fos = null;              //定义文件输出流
                             String text = etext.getText().toString();        //获取文本信息
                             try {
                                 fos = new FileOutputStream(file);     //获得文件输出流,并指定文件保存的位置
                                 fos.write(text.getBytes());           //保存文本信息
                                 fos.flush();                           //清除缓存
                             } catch (FileNotFoundException e) {
                                 e.printStackTrace();
                             } catch (IOException e) {
                                 e.printStackTrace();
                             } finally {
                                 if (fos != null) {
                                     try {
                                         fos.close();                    //关闭文件输出流
                                         Toast.makeText(MainActivity.this, "保存成功", Toast.LENGTH_SHORT).show();
                                     } catch (IOException e) {
                                         e.printStackTrace();
                                     }
                                 }
                             }
                         }
             ```

             

       4. SQLite数据库存储。

          1. ```java
             public class MySqliteDateBase extends SQLiteOpenHelper {
             	//创建数据库继承sqliteOpenHelper类
             
                 private static final int DATABASE_VERSION = 2;//数据库版本
                 public static final String DICTIONARY_TABLE_NAME = "dictionary";//数据库名字
                 public static final String KEY_WORD="Name";
                 public static final String KEY_DEFINITION="Id";
                 private static final String DICTIONARY_TABLE_CREATE =
                         "CREATE TABLE " + DICTIONARY_TABLE_NAME + "(" + KEY_WORD + " TEXT, " +
                                 KEY_DEFINITION + "TEXT);";//建表SQL语句
             
             
                 public MySqliteDateBase(Context context){
                     super(context,DICTIONARY_TABLE_NAME,null,DATABASE_VERSION);
                 }
             
                 
                 @Override
                 public void onCreate(SQLiteDatabase sqLiteDatabase) {
                     sqLiteDatabase.execSQL(DICTIONARY_TABLE_CREATE);//执行Sql语句,创建数据表
                 }
             
                 @Override
                 public void onUpgrade(SQLiteDatabase sqLiteDatabase, int i, int i1) {
             
                 }
             }
             
             
             ==》
                 MySqliteDateBase mySqliteDateBasenew=new MySqliteDateBase(FileActivity.this);//创建对象
             	SQLiteDatabase sqlBase=mySqliteDateBase.getWritableDatabase();//获得SQLiteDatabase对象
             	//或者 mySqliteDateBase.getReadableDatabase();
             
             ```

       5. Room存储数据

          1. 连接：[Android JetPack架构篇，一个实战项目带你学懂JetPack_SQLite d (sohu.com)](https://www.sohu.com/a/274129728_659256)
          2. 链接2：[Android Room 使用详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/89c53c066151)
          2. 相关线程知识连接：[AsyncTask的参数介绍 - XinYiBuFang - 博客园 (cnblogs.com)](https://www.cnblogs.com/xinyibufang/p/8183990.html)

       6. 网络存储

   13. 应用权限请求

       1. 所有应用的权限需要在Manifest配置文件中声明权限

          1. ```
               <uses-permission android:name="android.permission.CALL_PHONE"/>
               //声明一条拨打电话的权限
             ```

       2. 申请权限

          1. ```java
             // ContextCompat.checkSelfPermission(Context,String)用来检测权限是否授权 String为需要判断的权限名 
             // PackageManager.PERMISSION_GRANTED和PackageManager.PERMISSION_DENIED为两个判断是否存在权限的常量值
             // ActivityCompat.requestPermissions(Context,String[]1,String2) String1：需要申请的权限数组 String2:自定   义的请求码
             // onRequestPermissionsResult(int ,String[],int[])
             if(ContextCompat.checkSelfPermission(MainActivity.this, Manifest.permission.CALL_PHONE)!=
                                PackageManager.PERMISSION_GRANTED){
                   ActivityCompat.requestPermissions(MainActivity.this,new String[]					    {Manifest.permission.CALL_PHONE,Manifest.permission.SEND_SMS},1); 
                 //弹出请求权限，并将用户选择结果传递到onRequestPermissionsResult方法中
               }else{   call();  } 
                
             //拨打电话的方法
               private void call(){
                     try {
                         Intent intent=new Intent(Intent.ACTION_CALL);
                         intent.setData(Uri.parse("tel:10086"));
                         startActivity(intent);
                     }catch (SecurityException e){
                         e.printStackTrace();
                     }
                 } 
             //requestPermissions）执行完之后，会回调onRequestPermissionsResult
                public void onRequestPermissionsResult( int requestCode, String permissions[],int[] grantResults)
             {
                 switch (requestCode) {
                     case REQUEST_PERMISSION_CAMERA_CODE: {
                         if (grantResults.length > 0
                             && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                             // permission was granted, yay! Do the
                             // contacts-related task you need to do.
                         } else {
                             // permission denied, boo! Disable the
                             // functionality that depends on this permission.
                         }
                         return;
                     }
             
                     // other 'case' lines to check for other
                     // permissions this app might request
                 }
             }       
             ```

   14. **ContentProvider内容提供器**

       1. URL与URI，Uri

          1. 链接：

          2. ```java
             URI包括URL和URN两个类别，URL是URI的子集，所以URL一定是URI，而URI不一定是URL。
             
             URI = Uniform Resource Identifier 统一资源标志符，用来标识抽象或物理资源的一个紧凑字符串。
             
             URL = Uniform Resource Locator 统一资源定位符，一种定位资源的主要访问机制的字符串，一个标准的URL必须包括：protocol、host、port、path、parameter、anchor。
             
             URN = Uniform Resource Name 统一资源名称，通过特定命名空间中的唯一名称或ID来标识资源。
                 
                 
             /////    
             Uri结构：<scheme>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]
             
             Scheme：Uri的模式，比如http、file、content。如果Uri中没有指定scheme，意味着Uri无效。
             
             Host：Uri的主机名，比如www.baidu.com。如果Uri中没有指定host，意味着Uri无效。
             
             Port：Uri的端口号，比如8080，仅在scheme和host指定的情况下才有意义。
             
             Path、pathPrefix、pathPattern表示路径信息。Path对应的是完整的路径信息；pathPattern也表示的是完整的路径信息，但是允许其中包含通配符。pathPrefix表示路径的前缀信息
             
             ```

       2. UriMatch

          1. ```java
             （1）UriMatch.addURI(String authority, String path, int code)
             
             //在ContentProvider添加一个用于匹配的Uri，当匹配成功时返回code。Uri可以是精确的字符串，Uri中带有*表示可匹配任意text，#表示只能匹配数字。
             
             （2）UriMatch.match(Uri uri)
             
             //对传递过来的uri进行验证，查看是否匹配成功。
             
             ```

   15. FileProvider (文件数据共享)

       1. 作用：封装过的ContentProvider，可实现应用间的文件传递
       2. 链接：[Android之FileProvider详解 - 掘金 (juejin.cn)](https://juejin.cn/post/7009204672225345549)
       2. 链接2:[FileProvider使用详解（拍照、安装APP、共享文件） - SegmentFault 思否](https://segmentfault.com/a/1190000021357383)

       

   16. Java部分关键字释义

       1. volatile（**对一个变量的写操作先行发生于后面对这个变量的读操作**)
          1. 当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值，即当数据发生变化，所有线程都可以立刻看到这个已经发生改变的值，如数据库中数据库对象

   17. PackageManager  [包管理器|安卓开发人员 (google.cn)](https://developer.android.google.cn/reference/android/content/pm/PackageManager)

       1. 检索与设备上当前安装的应用程序包相关的各种信息的类。Context.getPackerManager()获得

   18. 数据绑定(**DataBinding**)

       1. 可以实现不通过findById()实现对控件数据的控制
       2. 链接：[布局和绑定表达式  | Android 开发者  | Android Developers (google.cn)](https://developer.android.google.cn/topic/libraries/data-binding/expressions?hl=zh-cn)

   19. BaseObservable 与 ObservableField (**实现数据绑定，实时更新**) 

       1. 链接：[(66条消息) Andriod --- JetPack (四)：BaseObservable 与 ObservableField 双向绑定_梁同学与Android的博客-CSDN博客](https://blog.csdn.net/qq_43290288/article/details/123481749)

   20. MVVM模式，(ViewModel)

       1. 易错点：grade文件中加入

          1. ```java
             dataBinding{
                 enabled=true;
             }
             ```

       2. 视图增加事件：

          1. 链接：[(68条消息) android mvvm点击事件绑定ViewModel_Simon66991的博客-CSDN博客_android mvvm事件绑定](https://blog.csdn.net/weixin_44177244/article/details/120260368)
          2. 事件绑定错误会导致数据绑定类生成失败，且无具体提示

   21. Activity任务栈

       1. 链接：[ActivityTaskView: 直观的Activity任务栈和LaunchMode分析工具 - 简书 (jianshu.com)](https://www.jianshu.com/p/c34483bb5c0f)

   22. 反序列化获取数据模型对象

       1. Gson:  链接:[Google Gson用法详解 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1662930)

   23. Retrofit 类(实现安卓的网络连接，配合Gson对象解析数据)

       1. Retrofit类中注解：[浅谈HTTP中GET、POST用法以及它们的区别 - 割肉机 - 博客园 (cnblogs.com)](https://www.cnblogs.com/williamjie/p/9099940.html)
       2.  链接2： [(78条消息) Retrofit 注解学习 @GET @POST @Query @QueryMap @Field @FieldMap @Body ...__无问西东的博客-CSDN博客_@get](https://blog.csdn.net/weixin_36709064/article/details/82468549)

   24. Service

       1. 用处：经常用于处理无需用户前台操作的得任务，如消息通知，
       2. 实现原理：开始服务startService(...)，会在当前启用的组件得进程中创建后台线程处理任务，(未绑定时)生命周期独立于启动组件，一般不关闭stopSelf()或unbindService()太会在进程
       3. 详解：[(18条消息) 安卓Service 详解_谈情不如逗狗.的博客-CSDN博客_安卓service](https://blog.csdn.net/hdhhd/article/details/80612726)

   25. HandlerThread处理极值详解：

       1. [Android Handler机制4之Looper与Handler简介 - 简书 (jianshu.com)](https://www.jianshu.com/p/e635c3f851ea)

2. 安卓UI美化

   1. androidx.drawerlayout.widget.DrawerLayout（抽屉式布局）

      1. 实现左右滑动页面更换效果
      2. 只可以指定两个子控件，并且需要设置layout_gravity属性，以确定左右布局

   2. ToolBar

      1. 可以替换默认ActionBar（需要指定没有ActionBar得主题），setSupportActionBar()设置属性
      2. 相关方法：[(22条消息) Android Toolbar的使用详解_暗恋花香的博客-CSDN博客_android toolbar](https://blog.csdn.net/qq_42324086/article/details/117390236)
      3. [AppbarLayout的简单用法 - 简书 (jianshu.com)](https://www.jianshu.com/p/bbc703a0015e)

   3. com.google.android.material.navigation.NavigationView （标准导航菜单）

      1. 可以将一个布局视为标题布局作为上部分，在使用menu菜单布局作为下部分

      2. ```java
         app:headerLayout="@layout/nav_header" //指定布局得头布局
         app:menu="@menu/nav_item_menu" //指定布局的菜单布局
         ```

      3. 详解：[(22条消息) 【Android】Material Design 之三 NavigationView 使用_摸爬滚打的程序媛的博客-CSDN博客](https://blog.csdn.net/qq_38950819/article/details/82734208)

   4. com.google.android.material.floatingactionbutton.FloatingActionButton （悬浮按钮）

      1. 可以让一个按钮单独悬浮在布局上，不受布局影响
      2. android:elevation="5dp"   该属性可以设置布局得阴影的大小 
      3. android:layout_gravity="end|bottom" 这里的end类似于start

   5. Snackbar （另一种方式的Toast）

      1. 在用户操作时给出提示，并且可以与用户产生交互
      2. 方法：make()启动

   6. CoordinatorLayout （加强版的FragmentLayout）

      1. 可以智能对控件行为做出调整

   7. Appbar （实现更加智能的顶部栏滚动效果，需要与CoordinatorLayout 以及ToolBar搭配使用

      1. 链接：[AppbarLayout的简单用法 - 简书 (jianshu.com)](https://www.jianshu.com/p/bbc703a0015e)

3. 动画

   1. 对于getX()，getRawX()，getTranslationX()的理解
      1. 链接：[(51条消息) Android开发之getX，getRawX,getWidth,getTranslationX等的区别_奋斗之路的博客-CSDN博客_android getrawx](https://blog.csdn.net/dmk877/article/details/51550031)
      1. 通过设置视图的View.setPivotX(float pivotX) 可以实现对视图缩放位置的调整

4. View视图绘制原理

   1. 链接：[Android View框架的measure机制 - 黄金夫 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xyhuangjinfu/p/5435201.html)

5. 实现截屏功能

   1. 链接：[Android截屏方案实现原理解析 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1735861)

6. android Touch 触控事件分发原理

   1. 链接：[Android Touch事件分发超详细解析（附源码） - 简书 (jianshu.com)](https://www.jianshu.com/p/bc4c9e5f4b1c)
   1. 链接2：[带着问题重学Android事件分发 - 掘金 (juejin.cn)](https://juejin.cn/post/6961704478600855582)

7. android 打包流程

   1. 链接：[Android Apk 编译打包流程，看完这篇文章直接变懂哥 - 简书 (jianshu.com)](https://www.jianshu.com/p/ef5cdf164f51)

8. Dialog setView与setContentView区别

   1. [(106条消息) 关于AlertDialog的setView与setContentView区别_chuoe4619的博客-CSDN博客](https://blog.csdn.net/chuoe4619/article/details/100616126)
   2. setContentView 是整个界面，**在show调用后调用**，setView为dialog得自定义试图区域，**在show调用前调用**

9. 下拉框控件

   1. Spinner 下拉框控件
   2. 常用属性：spinnerMode (设置下拉框得选择样式，dialog 或 dropdown)；entities:设置下拉框数据源

10. Spannable 

    1. 实现文字局部样式

    2. 主要方法：setSpan(文字得样式，开始得位置，结束的位置，操作目标)

    3. ```java
       String str="liDaChui";
       String value="li";
       //通过正则表达式可以快速确定字符得开始位置
       Matcher match=Patten.compile(value).matchs(str);
       //设置前景色
       spn.setSpan(new ForegroundColorSpan(Color.parseColor("#FF2196F3")),matcher1.start(),matcher1.end(), Spanned.SPAN_INCLUSIVE_INCLUSIVE);
       
       ```

    4. 详解：[Android UI——SpannableString详细解析 - 简书 (jianshu.com)](https://www.jianshu.com/p/472fd3e32324)

11. 相机拍摄获取照片，相册选择照片

    1. Action常量：MediaStore.ACTION_IMAGE_CAPTURE (打开相机)；Intent.Action_PICKER (挑选行为)，设置挑选类型路劲(MediaStore.Images.Media.EXTERNAL_CONTENT_URI)和类型(image/*)

       1. ```java
          //打开相机
          intent=new Intent(MediaStore.Images.Media.EXTERNAL_CONTENT_URI)
              //获得SD文件路径
          String path= Environment.getExternalStorageDirectory().getPath()+"/文件名/.../.jpg";    
          //将拍摄得照片存储得指定路劲,这样可以保证照片清晰度
          intent.setPutExtras(Media.OutPutExtras,path)
          
          //打开相册
           intent = new Intent(Intent.ACTION_PICK);
          //选择内容的类型            intent.setDataAndType(MediaStore.Images.Media.EXTERNAL_CONTENT_URI,"image/*");
          
          
          //获取结果:相册选择后会返回一个Uri,相机若未设置照片纯路径，将以缩小Bitmap得形式存在于result.getData().getExtras().get("data")中，如果设置了，通过path路劲为该文件流，读取转换为bitmap对象
                              
          ```

       2. 连接直达：[(109条消息) Android中拍照(相册中选择)并上传图片功能（包括动态获取权限）_kaolagirl的博客-CSDN博客_android 拍照上传](https://blog.csdn.net/kaolagirl/article/details/118113530)

12. TabLayout

    1. 实现滑动导航条，常用Viewpager联用

    2. 关键属性 textApperance (通过设置style来设置文字的样式)；tabIndicatorColor :设置指示器颜色；tabIndicatorHeight：设置指示器的高度，0则不显示；tabIndicatorGravity：设置指示器位置（stretch 铺满整个tab），于layout_gravity属性类似；

    3. 注意事项

       1. ```java
            			//添加自定义的控件时需要通过tab对象setCustomView()方法
                      TextView textView=new TextView(this);
                      textView.setText(str);
                      textView.setTextAlignment(View.TEXT_ALIGNMENT_CENTER);
                      //如果自己创建new tab 其父控件将为null,需要自己指定改tab的parent
          			// new Tablayout.Tab(); 
                      taskStatus.addTab(taskStatus.newTab().setCustomView(textView));
          			//设置选择监听，可以在这里修改tab的样式
          			taskStatus.addOnTabSelectedListener()
          ```

    4. 连接直达：[(114条消息) Android控件-TabLayout使用介绍_Android开发猿的博客-CSDN博客_android tablayout](https://blog.csdn.net/csdnxia/article/details/105947804)

       

    

    

    

    

    

    

    