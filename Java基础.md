Java基础

1. # JavaIO流

   1. 分类：
      按**流向方向**可分为（以内存为基准）：流向内存为**输入流**(Input)，也成为读(Read)；流出内存为**输出流**(Output)，也称为写(Write)。
      按**存取方式**可分为：**字符流**，以字符为单位，只能读取纯文本文件；**字节流**，一个一个字节读取，可以读取任意文件，包括图像视频。

   2. Java流四大家族

      1. 字节流：java.io.InputStream；java.io.OutputStream；

      2. 字符流：java.io.Read；java.io.Write；

      3. 特别说明：

         四大家族均为抽象类，且都实现了Closable接口；

         所有输出流都实现了Flushable接口，可以使用flush()方法刷新管道，如果使用后未调用，有可能会导致数据丢失；【flush()本质就是让系统知晓，该数据已经输出完毕】；

         **类名带有Stream的表示为字节流，带有Writer/Read的为字符流**

   3. 需要掌握的十六流

      1. 参考文章：[Java IO流（超详细！）_java io流(超详细!)_io流 csdn 野指针_一个快乐的野指针~的博客-csdn博客_一个快乐的野指针~的博客-CSDN博客](https://blog.csdn.net/qq_44715943/article/details/116501936?ops_request_misc=%7B%22request%5Fid%22%3A%22169494141416800211591589%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=169494141416800211591589&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-116501936-null-null.142^v94^insert_down1&utm_term=javaIO流&spm=1018.2226.3001.4187)
      2. 两个比较特别的转换流（将字节流转为字符流）
         InputStreamReader；
         OutputStreamWriter；

   4. 具体使用

      1. FileInputStream（文件输入字节流）

         ```java
         @Test
             public void testFileInputS() throws IOException {
                 FileInputStream fileInputStream=new FileInputStream("src/main.xml");
                 byte[] bytes=new byte[1024];
                 int readCount;
                 StringBuilder sb=new StringBuilder();
                 //read(每次读取字节的个数) 该方法会依次按以每次bytes读取文件,加载到内存中
                 //并返回读取到的字节个数,到末尾时会返回-1
                 //或者也可以用fileInput.available()方法，它可以直接判断该输入流里可读的长度;这样可以避免使用循环,不过该方法不适用于较大的文件
                 while((readCount=fileInputStream.read(bytes))!=-1){
                     sb.append(new String(bytes,0,readCount));
                 }
                 System.out.println(sb);
             }
         
         ```

      2. FileOutputStream

         ```java
         public void testFileOutputS() throws IOException {
                 FileOutputStream fileOutputStream=null;
                 try {
                     // main文件不存在的时候会自动新建！
                     // 这种方式谨慎使用，这种方式会先将原文件清空，然后重新写入。
                     //fos = new FileOutputStream("main");
                     //如果append为true则说明将内存中写出的直接拼接到源文件末尾
                     fileOutputStream=new FileOutputStream("src/main.xml",true);
                     String str="\\n FileOutputStream数据成功从内存中写出！";
                     byte[] bytes=str.getBytes("UTF-8");
                     //将内存中的数据写入文件中
                     fileOutputStream.write(bytes);
                     //写入完毕后，刷新一下
                     fileOutputStream.flush();
                 } catch (IOException e) {
                     e.printStackTrace();
                 }finally {
                     if(fileOutputStream!=null){
                         fileOutputStream.close();
                     }
                 }
             }
         ```

      3. FileReader（文本输入字符流）和FileWrite (文本输出字符流)
         这两个类适用于读取纯文本文件，基本上与上面类似，只是写入的格式必须以字符为单位写入；

      4. BufferedReader 【自带缓冲区的字符流，它不需要自定义字符char或者自定义字节byte】；InputStreamReader 【将字节流转为字符流】；

         ```java
         public class BufferedReaderTest01 {
             public static void main(String[] args) throws Exception{
         
                 FileReader reader = new FileReader("Copy02.java");
                 // 当一个流的构造方法中需要一个流的时候，这个被传进来的流叫做：节点流。
                 // 外部负责包装的这个流，叫做：包装流，还有一个名字叫做：处理流。
                 // 像当前这个程序来说：FileReader就是一个节点流。BufferedReader就是包装流/处理流。
                 BufferedReader br = new BufferedReader(reader);
         
                 // br.readLine()方法读取一个文本行，但不带换行符。
                 String s = null;
                 while((s = br.readLine()) != null){
                     System.out.print(s);
                 }
         
                 // 关闭流
                 // 对于包装流来说，只需要关闭最外层流就行，里面的节点流会自动关闭。（可以看源代码。）
                 br.close();
             }
         }
         
         ```

      5. InputStreamReader 转换流

         ```java
         public class BufferedReaderTest02 {
             public static void main(String[] args) throws Exception{
         
                 /*// 字节流
                 FileInputStream in = new FileInputStream("Copy02.java");
         
                 // 通过转换流转换（InputStreamReader将字节流转换成字符流。）
                 // in是节点流。reader是包装流。
                 InputStreamReader reader = new InputStreamReader(in);
         
                 // 这个构造方法只能传一个字符流。不能传字节流。
                 // reader是节点流。br是包装流。
                 BufferedReader br = new BufferedReader(reader);*/
         
                 // 合并
                 BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream("Copy02.java")));
         
                 String line = null;
                 while((line = br.readLine()) != null){
                     System.out.println(line);
                 }
         
                 // 关闭最外层
                 br.close();
             }
         }
         
         ```

2. ## Java注解

   1. 参考文档：[java注解-最通俗易懂的讲解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/37701743)

   2. 个人理解：
      java注解的出现只是为了辅助编译器去执行相关功能，它的存在对被注解的类型数据并无影响。

      java注解中有五个元注解，元注解就是给注解提供注解的注解，也就是用来修饰注解的。

      注解的关键字使用@interface修饰，它只有成员变量，没有方法（虽然它的书写方式也没有形参的方法类似），在使用时只需要@注解名(属性：值)。代码示例：

      ```java
      @Retention(RetentionPolicy.RUNTIME)
      public @interface Test {
          String v() default "";//使用default指定默认值
          String[] name() default "";
          Class<Object> target() ;
      }
      //使用
      @MyTest(v = "name",name = {"",""},target = MyTest.class)
          public void testMethod(){
              
          }
      
      ```

   3. 实现原理：总体是java反射机制，通过方法 **isAnnotationPresent(Class<? extends Annotation> annotationClass)**判断类是否存在注解，再通过反射获取到该注解示例，最后获取到该成员变量的值。

3. 栈与堆，方法区

   1. 个人总结
      
       *栈内存*：**它只保存方法中的是基本数据类类型变量（不包括类的属性变量）和自定义对象的引用变量**，是低到高的向上生长的方式，所以是先今后出的存取结构，也就是先进去的地址比后进来的小，它是由系统管理并分配；一个线程一个栈，栈与栈之间互不干涉，互不共享；
      
      *堆内存*：用于**存放该应用进程的全部变量实列对象和数组，每个对象示例再方法区都有其对应的类信息**，是由高到低的向下生长的方式，与栈相反，所以是先进先出，有点类似于队列的性质，需用程序员自己申请开辟（比如用new 或者malloc函数），以及释放，未释放其生命周期与程序进程保持一致，**当栈中的没有变量指向时，会在某个时间被回收**；
      
      *方法区*：它属于堆内存的一部分，用来存储已加载类的信息（比如类的属性），static变量，字符常量，已加载的代码等；和堆一样，数据全线程共享；
      
      栈和堆都属于系统对进程占用的内存空间进行管理的方式，也是两种数据结构；
      
      例如：
      
      ```java
      void main(){ //mian函数是程序入口，jvm开辟一端栈内存用来存储main方法中的局部变量a，将方法压栈;
          int[] a=new int[3];// new int[3]会在堆内存开辟一堆空间，并将该首地址返回赋值给x;
          a[0]=30;//再堆内存中 将30赋值给0这个数据元素
          a=null; //将栈中的局部引用变量指向null,堆中a原来指向的数组对象示例会在某个时间被jvm回收
      }
      ```
      
      列如：
      
      ```java
      //main执行，再栈内存中开辟一段栈内存，存放方法中的变量
      static void main(String[] args){
          //jvm会在堆的方法区查找Person类的类信息,如果没有找到通过类加载器加载Person类到方法区中,记录引用,并再堆中开辟内存，将栈中的person指向堆中的Person对象实例,然后将person添加到mian的栈中
      	Person person=new Person("丽丽");
          //栈通过person找到堆中的Person实列,根据堆上对方法区的引用,找到sayHello的字节码文件,执行
          person.sayHello();
      }
      class Person { 
      	String name; 
          public Person(String name) { 
      		this.name = name; 
      	} 
      	public void sayHello() { 
      		System.out.println("hello " + name); 
      	}
      ```

4. Java反射机制

   1. 个人理解

      java反射是java成为动态语言的一个重要表现；再类加载完成之后，会在堆内存的方法区中生成一个Class类型的变量，这个变量记录了一个类的全部信息，也就是可以通过它得到该类的所用属性与方法；由于其整个过程就类似再照镜子一样，所以就称为反射；

      Class类型是实现的关键；来源：程序再执行javax.exe命令后，会生成一个或多个字节码文件(.class)，再通过java.exe运行时，JVM会把这些字节码文件加载到内存中；这个时候，加载到内存中的类就叫运行时类，次类作为一个Class的一个实列；

      每一个字节码文件(.class)就对应一个`Class`类型的对象；每个类都会记得自己是那个Class类型生成的；一个加载的类在 `JVM`中只会有一个`Class`实例；

   2. 常用的API

      1. 参考：[Java-反射机制（超详解）_java反射机制-CSDN博客](https://blog.csdn.net/weixin_52533007/article/details/123312217)

5. Java多线程

   1. 基本概念
      并发：一个对象（进程）被多个线程操作
      并行：多个进程（任务）同时进行
      串行：一个一个任务进行，就跟排队一样
   
   2. 进程三态：
      就绪 ：当进程获取出CPU外所有的资源后，只要再获得CPU就能执行程序，这时的状态叫做就绪态。在一个系统中处于就绪态的进程会有多个，通常把这些排成一个队列，这个就叫就绪队列。
   
      运行：当进程已获得CPU操作权限，正在运行，这个时间就是运行态。在单核系统中，同一个时间只能有一个运行态，多核系统中，会有多个运行态。
   
      阻塞：正在执行的进程，等待某个事件而无法继续运行时，便被系统剥夺了CPU的操作权限，这时就是阻塞态。引起阻塞的原因有很多，比如：等待I/O操作、被更高的优先级的进程剥夺了CPU权限等。
   
   3. 多线程并发实现方式
   
      1. 主要实现是Runnalbe和Callable接口，再创建Tread对象，开启线程；
   
         ```java
          private void test1(){
                 //使用thread开辟一条线程
                 //start()方法会调用TestClass.run()
                 new Thread(new TestClass()).start();
             }
             class TestClass implements Runnable{
                 @Override
                 public void run() {
         			System.out.println("Run()运行！");
                 }
             }
         ```
   
         说明：Callable接口会有返回值；
   
      2.通过线程池创建
   
      ​	通过线程池可以提高线程利用率，不用每次都开辟一条新的线程；
   
      ```java
      private void test1() throws ExecutionException, InterruptedException {
              //Executors可以创建线程池 并初始化线程个数 调用submit执行
              ExecutorService service = Executors.newFixedThreadPool(3);
              Future<?> submit = service.submit(new TestClass());
              //生成的future对象可以返回结果(如实现了Callable接口的对象)
              Object o = submit.get();
          }
          class TestClass implements Callable<Object>{
              @Override
              public Object call() throws Exception {
                  return null;
              }
          }
      ```
   
   4. 线程安全问题
      多线程并发，必然会出现线程安全问题，也就是同一个对象再不同线程操作之后另一个线程并不知晓，就是使用原数据导致结果不如愿；因此就引入了线程锁这一方法；
      参考：[JAVA多线程详解（超详细）-CSDN博客](https://blog.csdn.net/qq_29141913/article/details/125964815?spm=1001.2014.3001.5506)
   
   
   
   