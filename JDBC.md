## 1.0.0 JDBC基础(Java Data Base Connectivity)

> JDBC其实是定义了Java语言访问数据库的规范。
>
> 中间层框架（访问数据库）都是基于JDBC实现的。

### 1.1.0 连接数据库的步骤

1. 注册驱动（只做一次）

2. 建立连接（Connection）
3. 创建执行SQL的语句（Statement）
4. 执行语句
5. 处理执行结果（ResultSet）
6. 释放资源 *

#### 1.1.1  注册驱动

```java
//反射技术
Class.forName("com.mysql.jdbc.Driver");
```

在获得Driver.class文件的时候，会触发类加载机制，其中在Dirver类中有一段静态代码块(DriverManager.registerDriver(com.mysql.jdbc.Driver))

**注册驱动的三种方式**

- Class.forName("com.mysql.jdbc.Driver") **推荐这种方式，不会对具体的驱动类产生依赖**
- DirverManager.registerDriver(com.mysql.jdbc.Driver);**真正注册驱动的功能** 但会造成DriverManager中产生两个一样的驱动，并会对具体的驱动产生依赖
- System.setProperty("jdbc.drivers","driver1:driver2"); 虽然不会对具体的驱动类产生依赖，但注册不太方便，所以使用很少。

#### 1.1.2 建立连接

```java
// 获取数据库连接
Connection connection = DriverManager.getConnection(url, user, password);
//url: 数据库的地址 
JDBC:子协议:子名称//主机名:端口/数据库名?属性名=属性值&...
jdbc:mysql://localhost:3308/demo
//其他参数：
useUnicode=true&characterEncoding=UTF-8 采用utf-8字符集编码格式
```

#### 1.1.3 创建执行器

```java
//通过数据库连接获取到执行器
Statement statement = connection.createStatement(); 
```

#### 1.1.4 执行SQL语句

```java
//执行静态sql语句
statement.execute(sql); 
```

#### 1.1.5 处理执行结果

```java
//处理执行结果 查询操作返回结果封装进结果集ResultSet
ResultSet resultSet = statement.executeQuery(sql);
```

#### 1.1.6 释放资源【*】

```java
//关闭数据库连接
connection.close();
```



### 1.2.0 PreparedStatement

#### 1.2.1 SQL注入

> 在SQL中包含特殊字符或SQL的关键字（如：‘**or 1=1**’）时Statement将出现不可预料的结果（出现异常或查询结果不正确），可用PreparedStatement来解决。

#### 1.2.2 PreparedStatement

> 从Statement扩展而来，具有**预编译**功能的执行器，提高访问数据库的性能
>
> 语句中通过**'?'**进行占位预编译

> PreparedStatement执行语句会先到PreparedStatement缓存中去寻找这个语句，
>
> 如果缓存未命中，则将这条语句编译后存入PreparedStatement缓存中，然后发送给数据库。
>
> 如果缓存命中，就不会再将语句发送给数据库，只会把相关的值发送给数据库

数据库效率：

- sql编译	占性能10%
- 数据库连接的建立 占80-90%

相对Statement的**优点**：

1. 没有SQL注入的问题
2. Statement会使数据库频繁编译SQL，可能会造成数据库缓冲区溢出。
3. 数据库和驱动可以对PreparedStatement进行优化（只有在相关联的数据库连接没有关闭的情况下有效）

### 1.3.0 特殊数据类型

#### 1.3.1 日期时间

> mysql 日期类型 date（只有日期）time（只有时间）datetime（日期时间都有）timestamp（日期时间都有）
>
> ** datetime和timestamp表现形式上完全相同，区别就在于timestamp在数据库可以自定义更新（当前时间）

#### 1.3.2 大数据类型CLOB

* CLOB -> text clob

  ```java
  //存
  ps.setCharacterStream(index,reader,length);
  ps.setString(i,s);
  //取
  reader = rs.getCharacterStream(i);
  reader = rs.getClob(i).getCharacterStream();
  string = rs.getString();
  ```

* BLOB -> blob

  ```java
  //存
  ps.setBinaryStream(i,inputStream,length);
//取
  rs.getBinaryStream(i);
  rs.getBlob(i).getBinaryStream();
  ```
  
