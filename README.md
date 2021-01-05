
# 类加载器 classloader，加载.class文件进内存
 - !!!!!重要
 - 描述：加载字节码到内存的方法区的代码区存储，并为之创建一个与其对应的.class字节码文件对象  * 补充jvm的内存模型
    - BootStrapClassLoader 根类 启动类 加载器，加载jre/lib/rt.jar 
    - ExtClassLoader: 扩展类 加载器  加载jre/lib/ext/*.jar 
    - AppClassLoader: 应用程序类加载器， 加载用户自定义的类 配置，classpath+用户自定义的类
    - 自定义的类加载器 了解
    - 以上BootStrapClassLoader,ExtClassLoader先启动无误后加载Appclasssloader与自定义的类
 - 1.clazz读内存创建对象
 - 2.类连接，验证阶段，验证解析
 - 3.类初始化条件
    - 第一次使用时字节码文件在内存中未存在就加载
 - 加载机制
    - 全盘加载（加载cat会加载animal），父类委托（问父级能不能做，如果所有父级都不行，报错），缓存机制(加载后不再释放)
    
 -     

# 反射,一般情况下只能javac在编译情况下运行，反射可以在字节码文件加载到内存后形成字节码对象，即使在运行期间，也可以通过字节码文件对象使用其中成员的过程
 - 根据配置文件实现对应的方法，配置文件可以随时修改
 - 3种方法  .class  用于锁对象    .getClasss()  一般用于判断两个类的对象是否是同一个对象     Class.forName("全类名")
 - 1.获取字节码文件对象，2.根据字节码文件获取成员对象 ， 3.设置暴力反射（可选）私有成员则为必选con.setAccessiable  ， 4.操作类中指定的成员对象。
 - getMethod() getConstructor() getField() getDeclaredConstructors
 ## 操作成员对象，成员变量，成员方法
  - getMethod()会获取父类的方法，而getDeclareMethod 只拿自己的包括私有方法
 ## 反射越过泛型检验
    越过arraylist中的int类型限制
    (```)
      步骤1.获取字节码文件对象 a = Class.getName("java.util.Array")
      步骤2.修改arrylist的add方法为object类型插入，* 注意string与int并不兼容，若要在被泛型限制的arraylist中插入字符串应用object
      步骤3.调用add
      步骤4.查看结果
    (```)
# 注解
 - properties
 - 边写文档
 - 代码分析：用于替代配置文件，通过反射的技术获取配置的信息
 - 编译检查
## 常用注解
  - override ，deprecated, suppresswarnings("类型")
 
 
 
