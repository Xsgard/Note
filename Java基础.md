## 1.0 内部类

就是类中嵌套另一个类型，根据内部类位置不同，可以有如下形式：

- 成员内部类 【一个类作为另一个类的普通成员】
- 静态内部类 【一个类作为另一个类的静态成员】
- 局部内部类 【一个类作为方法的成员】
- 匿名内部类 【特殊的局部内部类，也是方法的成员】

#### 1.1 成员内部类

**优点：**

- 成员内部类可以直接访问外部类的所有成员
- 对于私有的成员内部类来说，只供这个外部类使用，外界不能访问私有成员

**缺点**

- 内部类语法比较特殊，不方便调用



#### 1.2 静态内部类

**优点：**

-  可以直接访问外部类的静态成员
- 在外部类看来，公开静态内部类可以“上升”为外部类

> 静态内部类多作为算法及功能的载体，一般不作为数据载体，这个算法或功能只为所外外部类去服务。



#### 1.3 局部内部类

> 定义在外部类的成员方法中
>
> 局部内部类可以访问外部类的所有成员还可以访问所在方法的局部变量
>
> **在JDK8之前，局部内部类要访问所在方法的局部变量时，要去局部变量必须是final
>
> 因为：Java虚拟机的加载机制，会将Class类编译为字节码加载进虚拟机，而方法只有当调用的时候局部变量才会有值，所以会要求局部变量加上final修饰，要求其不可变。



#### 1.4 匿名内部类

利用抽象父类或接口来完成

特点：

> 同局部内部类



## 2.0 IO流

> 用于操作文件内容。文件内容可以分为两个类别：
>
> - 二进制文件，【所以除文本文件之外的文件，如：音频、视频、图片、Word、PPT、Excel等】
> - 文本文件，能用记事本打开的，使用者可以直接读懂的文件，如【.txt、.java、.md等】

注：

**不管二进制文件，还是文本文件，其本质都是010101的存储，不同在于他们的编码方式不同**

***文本文件***

> 是以字符集进行编码的，而字符集是由不同国家和地区根据自己的情况指定的，并且得到国际上的认可。
>
> 如：中国地区的字符集编码就是GBK，西区地区字符集时ISO-8859-1，国际编码字符集是UTF-8，...
>
> 每个国家的字符集都是公开的

***二进制文件***

>一般来讲，都是软件厂商自定义的编码规则，有的是公开的，有的是商业机密，这些编码规则往往与创建此类格式的软件和解析此类格式软件形成一个闭环。比如：Word格式的文件，就必须使用微软公司出品的Office办公软件去创建和解析。

文本文件也是一种二进制文件，之所以把他单列出来，是因为它使用较为频繁，而且不方便使用二进制处理它，

而且使用字符去处理他更为方便。

所以，文本文件是以**字符**为单位进行处理的，二进制文件是以**字节**为单位进行处理的。

> IO流API
>
> 包：java.io

### 2.1 字节流

#### 2.1.1 字节输入流

```Java
java.io.InputStream    ---抽象父类
	\- java.io.FileInputStream
	\- java.io.ByteArrayInputStream
	\- java.io.FilterInputStream
		\- java.io.BufferInputStream
    	\- java.io.DataInputStream
    	\- java.io.PushBackInputStream
    \- java.io.ObjectInputStream
抽象出一些共性接口
java.io.DataInput
	\- java.io.ObjectInput
```

**InputStream中的共性方法**

- int read() --> 读取一个字节,效率很低。返回值 -1表示读到了文件尾【EOF】,非-1的返回值表示读到的字节值本身
- int read(byte[] buf) -->尝试最多读取buf.length个字节，方法返回值表示实际读到的字节个数。如果读到文件尾【EOF】,则返回-1。
- int read(byte[] buf,int offset,int length)  --> 从offset位置尝试最多读取length个字节，返回值意义同第2个方法
- void close() --> 释放流资源。
- available() --> 返回从该流中可以读取的字节数的估计值

#### 2.1.2 字节输出流

```java
java.io.OutputStream    ---抽象父类
	\- java.io.FileOutputStream
	\- java.io.BufferedOutputStream
	\- java.io.DataOutputStream
	\- java.io.ObjectOutputStream
	\- java.io.ByteOutputStream
抽象出一些共性接口
java.io.DataOutput
	\- java.io.ObjectOutput
```

**OutputStream中的共性方法**

- void write(int byte)；写入单个字节
- void write(byte[] buf); 写入buf.length个字节
- void write(byte[] buf,int offset int length); 写入length个字节
- void close()

**以上这些流又可以分为两种，一种是本身就具备流读写能力的，一种是在原有流基础上的，添加新的功能的流。**



#### 2.1.3 节点流

> **本身拥有流的读写能力，如：FileInputStream/FileOutputStream，ByteArrayInputStream/ByteArrayOutputStream**
>
> **从构造器的参数也可以看出来，这类流的构造是以“源”为参数的。**



#### 2.1.4 过滤流

> **本身并没有流的读写能力，他必须要借助节点流来构造。比如：DataInputStream/DataOutputStream,**
>
> **BufferedInputStream/BufferedOutputStream等**
>
> **从构造器的参数也可以看出来，这类流的构造是以“流”为参数的。**

这是一种装饰模式



#### 2.1.5 基本数据类型读写的流

> **DataInputStream/DataOutPutStream**
>
> 利用此类型可以把基本数据类型持久化到文件中



#### 2.1.6 读写对象的流

> ObjectInputStream/ObjectOutPutStream
>
> 这个可以进行对象读写，要求对象的类型必须要实现java.io.Serializable接口
>
> 这个接口可以持久化对象状态 。

有关对象的读写操作，有两个细节需要注意：

- 被持久化的对象必须要实现java.io.Serializable接口
- 如果某些属性不想被持久化，可以使用transient修饰符修饰



#### 2.1.7 随机读写流

> **RandomAccessFile**
>
> 是一个即支持读，也支持写的节点流，它实现了DataInput和DataOutPut接口。
>
> 支持移动访问的位置  

常用方法：

- public RandomAccessFile(String path,String mode)

- public RandomAccessFile(File path,String mode)

- seek(long pos)

- getFilePointer() -> long

- ...

  > 主要的打开模式有：
  >
  > - "r"以只读模式打开
  > - "rw"以读写模式打开



### 2.2 字符流

> 字符流是以字符为单位处理的流，它实际上是jvm针对字符文件做的特殊处理。
>
> 本质上，有了字节流就可以处理字符文件，但不方便。

#### 2.2.1 字符输入流

```java
java.io.Reader
	\- FileReader
	\- CharArrayReader
	\- FilterReader 
		\- PushbackReader
	\- BufferedReader	[*]自带换成，支持整行的读取
	\- InputStreamReader (字节流到字符流的桥接器)
    \- ....
```

**Reader常用方法**

- read()  -》	去读单个字符
- read(char[] buf) -》 尝试读取buf.length个字符
- read(char[] buf,int offset,int length)  -》尝试从偏移量offset处读取length个字符
- close()  -》 释放

**BufferedReader的方法**

- readLine() -> String 此方法以换行符为终止符，但是，返回的字符串不包含终止符



#### 2.2.2 字符输出流

```java
java.io.Writer
	\- FileWriter
	\- CharArrayWriter
	\- OutputStreamWriter [字节输出流到字符输出流的桥接器]
	\- BufferedReader
	\- PrintWriter [*]自带换成，支持整行的写入， println()
    \- ....
```

**Writer常用方法**

- write(int c) 写入传入的单个字符
- write(char[] buf)  把buf中的字符写入到输出流，写入的是buf.length个字符
- write(char[] buf,int offset,int length)同上，写入的是len个字符
- close()



#### 2.2.3 有关字节流到字符流的桥接器

> 有些标准输入输出设备被定义成了字节流，我们需要把他们转换为字符流，这里就可以使用桥接器，
>
> 如下：
>
> BufferedReader br=new BufferedReader(new FIleReader("hello.txt")); //指向文本的字符输入流
>
> 再看：
>
> BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
>
> 再，有一个指向文本文件的字节流,并重新指定字符集为GBK
>
> BufferedReader br=new BufferedReader(
>
> ​											new InputStreamReader(
>
> ​													new FileInputStream("hello.txt"),"GBK"));

**InputStreamReader的构造器**

- InputStreamReader(InputStream in) 采用默认字符集做转换器
- InputStreamReader(InputStream in,String charsetName) 指定字符集做转换器



## 3.0 集合框架 【JCF】

> Java Collection Framework，它是由一组API组成，主要针对容器封装，底层有不同的实现，比如有基于数组的实现，有链表、哈希算法、二叉树的实现。
>
> 在Java中，数据容器有两种
>
> ​	1.基于值的存储，有：List，Set
>
> ​	2.基于键、值对的存储，有Map

#### 3.0.1 基于值的存储

```Java
Java.util.Collection
		\- List  有序、可排序、可重复
			\- ArrayList   基于数组实现
			\- LinkedList  基于链表实现
			\- Vector      同ArrayList，它是多线程安全的、一个重量级的集合（synchronized）所有方法						    都是同步方法
		\- Set   无序、不可排序、不可重复
			\- HashSet 	   使用哈希算法实现的
			\- SortedSet   是Set的一个子接口，他是可排序的，不可重复
				\- TreeSet 使用二叉树实现
```

> 注：由于在Java中，数组容器在操作上有诸多不便，所以，API提供了JCF供我们使用。如此多的类型，他们各自的特点是不同的。
>

针对List来说，它的特点是元素有序、可排序、可重复，提供了基于数组和双向链表的不同实现，我们在选择时，可根据实际情况进行选择。



### 3.1.0 Collection的操作方法

- boolean add(T element) 往容器中添加一个新元素
- boolean AddAll(Collection allElement) 往容器中添加指定容器的所有元素





























