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

3. 栈与堆

   1. 个人总结
      栈是用来存放函数，局部变量，是高到低的生长方式，是由系统管理并分配；堆内存，用于存放变量实列，生长方式与栈相反，需用程序员自己申请开辟，以及释放，未释放其生命周期与程序进程保持一致；

      栈和堆都属于系统对进程占用的内存空间进行管理的方式，也是两种数据结构；

      ​	

   

   