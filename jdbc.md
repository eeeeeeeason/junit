# jdbc6步
 - 1.注册驱动
    - 1.1 不要用DriverManager.registerDriver(new Driver()) mysql.Driver继承了java.sql.Driver并且为静态static方法，在加载时触发激活Driver。
    - 1.2 利用反射注册驱动，Class.forName("com.mysql.jdbc.Driver") // 8.0 mysql.cj.jdbc.Driver
 - 2.获取连接对象DriverManager.getConnection("地址/仓库","zh","mm");
 - 3.获取执行sql的对象
    - 3.1 createStatement : 无转译功能可sql注入。。。太low了，早就没人玩了
    - 3.2 prepareStatement: ?设置占位符，将非法字符转译使其成为字符串而无sql功能,避免sql注入
    - 3.3 管理事务，事务是指多个操作，其中一个操作失败则集体回滚
        - 3.31 setAutoCommit commit rollback setTransactionIsolation(int level)  ****
 - 4.执行sql
    - 4.1 executeQuery(String sql);
    - 4.2 executeUpdate(sql);
    - 4.3 批处理 AddBatch(String sql); //仅用于更新语句
 - 5.获取sql执行结果
 - 6.输出
## 连接池相关内容
  - 背景: 当我们业务要求使用大量生命周期短的连接对象，频繁创建连接对象导致损耗开销巨大，连接池的原理是存储多个连接对象，在池中，有需要时取出，用完时归还
  - 弊端: 并不是说连接池一定比直接连接更加有效，例如：仅进行一次连接，连接池中其他的连接对象则会闲置，导致利用率更低
  - DBCP(不能自动回收空闲连接),C3P0(重写了close方法可以自动回收),DRUID(分布式事务结构，更好支持大数据业务)
      - c3p0使用 1. 导包 2. src下加载c3p0-config.xml配置文件 new ComboPooledDataSource();
  - 自定义数据库连接池所需的设计模式 。 适配器模式 + 模板方法模式
  
## 事务
setAutoCommit(false)
