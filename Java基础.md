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
- boolean remove(T element) 从容器中移除指定的对象
- boolean removeAll() 从当前集合中删除指定集合中的所有元素
- void clear() 从容器中移除所有元素
- boolean contains(T element) 判断当前容器是否包含指定元素
- boolean containsAll(Collection elements) 判断当前容器是否包含集合中所有元素
- int size() 获取当前集合有效元素的个数
- toArray() 把集合转换成数组
- Iterator iterator() 返回指向当前集合的迭代器

#### 3.1.1 Iterator接口

- boolean hasNext() 判断迭代器中是否有下一个可使用的元素
- T next() 取出迭代器指向的元素，并把指针向下移动一次

#### 3.1.2 Iterable接口

- Iterator iterator() 返回当前集合的迭代器



#### 3.1.3 List 【有序、不可重复】

- T get(int index)  根据下标来访问元素
- void set(int index,T element)  把元素Element放到指定的位置
- List subList(int start ,int end) 求子集，含start位置，不含end位置，返回的是新的集合
- boolean isEmpty();

#### 3.1.4 List的实现类

- ArrayList
  - public ArrayList();
  - public ArrayList(int size);
  - public ArrayList(Collection c);
- LinkedList
  - public LinkedList();
  - public LinkedList(Collection c)

#### 3.1.5 栈的特点 Stack

> 先进后出，FILO，一般只提供对栈顶的操作，包括进栈、出栈、判断栈是否为空，以及栈中的个数

#### 3.1.6 队列的特点 Queue

> 先进先出，FIFO，一般提供对队头的操作【增、删、查】，包含入队出队操作，在JCF的API中，有提供这个接口

```java
java.util.Queue [接口]
	\- java.util.Deque [接口]
```

它的方法主要有如下6个，集中在三个功能上：

添加操作

- add(E element) 如果队列容量不够，则抛出异常
- offer(E element) 如果队列容量不够，则执行失败返回false

删除操作

- remove() 如果队列为空，则抛出异常
- poll() 如果队列为空，则返回null

查询操作

- element() 如果队列为空，则抛出异常
- peek() 如果队列为空，则返回null

**Deque 双端队列** 

> double end Queue,简称Deque，它支持两端进行操作。它是Queue的子接口。

同样，由于它是双端操作，所以，它的核心方法比Queue多一倍，也是集中在三个功能。

添加操作，删除操作，查询操作

#### Collection集合的结构类图

```Java
java.lang.Iterable
	\- java.util.Collection
		\- java.util.List
			\- ArrayList
			\- LinkedList
			\- Vector
		\- java.util.Set
			\- HashSet
			\- java.util.SortedSet
				\- TreeSet
		\- java.util.Queue
			\- PriorityQueue
			\- java.util.Deque
				\-ArrayDeque
	//注： 以上带包的都是 接口，不带包的都是 实现类	
```



#### 3.1.7 Set

> 几乎与Collection一样。
>
> 它的特点是：无序、不可重复

**实现类：HashSet**

> 它是如何做到无序及不可重复的呢？

首先， 当我们把一个对象添加到HashSet时，这个容器会调用对象的hashcode()方法，得到一个整数。根据这个整数来计算出此对象应该存放的位置。

其次，当我们再次添加一个对象时，同样会调用此对象的hashcode()方法，得到一个整数，算出他该存储的位置，此时，如果这个位置已经被占用，则会调用它的equals()方法，如果返回true，说明此对象与之前的对象相等，则放弃存入。如果，返回false，则表示对象不相等，则利用红黑树来存储进行纵向扩展。

> 注：
>
> 上面的原理，其实是HashMap的原理，而HashSet中，只是组合了HashMap，并且只是利用了它的Key，而Value永远是同一个Object



#### 3.1.8 TreeSet的使用

> 实现了SortedSet接口

**特点：不可重复，加入即自动排序**

**TreeSet如何实现加入即排序的？**

> 排序的接口：
>
> ​	1.java.lang.Comparable<T>
>
> ​			方法：int compareTo(T other)
>
> ​	2.java.util.Compartor
>
> ​			方法：int compare(T o1,T o2)



### 3.2.0 Map

> 键 值 对的存储

```java
Map [I]
	\- HashMap
	\- SortedMap [I]
		\- TreeMap
```



#### 3.2.1 HashMap

> 基于Hash算法的一种Map实现



**HashMap的key是唯一、不可重复的**

> 他是如何做到的？
>
> 

原理：

作为Map的key的类型，要求：

- 重写hashcode方法

- 重写equals方法

  > 将对象放入HashMap时，首先会调用hashcode方法得到hash码值，根据对象的hash码值决定放入容器的位置。再次放入对象时，还是先hashcode获取到hash码值，根据对象的hash码值确定放入的位置，如果位置已经被占用，会调用equals方法判断是否与之前存入的对象相同，如果返回为true，说明与之前存入的对象为同一个对象，会将后存入对象的value**替换**之前的value。

如果，没有重写这两个方法，则依赖于Object类提供的默认实现（比较对象的内存地址）。

所以不建议使用自定义类型作为Map的key，应该使用JDK自带的如下类型：

- Integer
- Long
- String

> **注：**
>
> 我们也可以使用自定义类型来作为Map的key，只要重写equals和hashcode方法。
>
> value的类型可以是任意类型。
>

 

#### 3.2.2 Map的迭代

> Map分支不由继承Iterable接口，所以，它本身是不能被直接迭代的。
>
> 可以把Map转换成Collection后，再进行迭代
>
> ​	**三种迭代方式**
>
> - **把Map的key取出来变成一个Set**<K>
>
>   ```java
>   Set<Integer> keys=map.keySet();
>   //先迭代Set
>   for(Integer key:keys){
>       //现根据key来获取value
>       String value =map.get(key);//通过key来获取value
>   }
>   ```
>
> - **把Map的value取出来变成一个Collection<V>**
>
>   ```java
>   //
>   Collection<String> values=map.values();//这个values()方法把key丢掉了
>   //迭代Collection
>   for(String value:values){
>       System.out.println(value);//注： 这种方式，只能获取到value，而key不能迭代
>   }
>   ```
>
> - **把Map的key和value封装成Entry类型，形成一个 *Set<Entry<K,V>>***
>
>   ```java
>   //
>   Set<Entry<Integer,String>> entrys=map.entrySet();//把key，value同时取出来
>   //
>   for(Entry<Integer,String> entry:entrys){
>       //通过Entry获取API
>       Integer key=entry.getKey();
>       String value=entry.getValue();
>   }
>   ```



#### 3.2.3 SortedMap

> key不可重复，加入即自动排序



#### 3.2.4 TreeMap

> 底层采用二叉查找树来存储

**构造**

```java
public TreeMap();	//要求：存放的key必须是实现了java.lang.Comparable接口的类型，如：Integer，					   String，Date，LocalDate,...
public TreeMap(Comparator c);
public TreeMap(Map map);
```



#### 3.2.5 TreeMap和TreeSet的关系

> TreeSet的底层就是TreeMap，它采用了组合方式。

#### 3.2.6 HashMap和HashSet的关系

> 同理，HashSet的底层也组合了HashMap，也就是说，利用Map的key作为Set的存储器，而value采用固定的Object来填充。
>



### 3.3.0 JCF小结

![图 1. Collection 接口及其常用实现](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/932cdafb5ea24bb990cd97cf47a0b04c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)



### 补充：二叉树

![1688352269491](C:\Users\Asgard\Desktop\myNote\assets\1688352269491.png)

##### 二叉树分类

**1）、完全二叉树**

在一棵二叉树中，除了最后一层，都是满的，并且最后一次或者是满的，或者是右边确实连续若干节点，成为完全二叉树。如图所示：

![1688352476263](C:\Users\Asgard\Desktop\myNote\assets\1688352476263.png)

**2）、满二叉树**

一颗深度为K，并且有(2^k+1)-1个节点的二叉树，成为满二叉树。如图所示：

![1688352638581](C:\Users\Asgard\Desktop\myNote\assets\1688352638581.png)

**3）、二叉查找树(Binary Search Tree) BST**

又称为二叉搜索树，排序二叉树，可为空树，或节点满足左子树所有节点<根节点<右子树所有节点，不存在相等值的节点，可以拆分成如下三个要求：

- 某节点的左子树节点值仅包含小于该节点的值

- 某节点的右子树节点值仅包含大于该节点的值

- 左右子树每个也必须是二叉树

  如图所示：

![1688352976407](C:\Users\Asgard\Desktop\myNote\assets\1688352976407.png)

**BST的遍历算法：**

1. 前序遍历

   根 -> 左 -> 右

2. 中序遍历

   左 -> 根 -> 右

3. 后序遍历

   左 -> 右 -> 根

**红黑树其实就是去除二叉查找树的顶端优势的解决方案**，从而达到平衡。



**4）、平衡二叉树(Balanced Binary Tree)**

是一种结构平衡的二叉搜索树，即叶子节点深度差不超过1，能够在O(logn)内完成插入、查找和删除操作，结构如图所示，常见的平衡二叉树有AVL树、红黑树等。

![1688354765223](C:\Users\Asgard\Desktop\myNote\assets\1688354765223.png)

**5）、AVL树**

又被称为高度平衡树，是最先发明的平衡二叉查找树，任何节点的两个儿子子树的高度差最大为1，增加和删除可能需要通过一次或者多次树旋转来重新平衡这个树，树如图所示：

平衡前（非AVL树）：

![1688355175984](C:\Users\Asgard\Desktop\myNote\assets\1688355175984.png)

平衡后（AVL树）：

![1688355195798](C:\Users\Asgard\Desktop\myNote\assets\1688355195798.png)

6）、红黑树（Red-black Tree）

是一种自平衡二叉查找树，又成为“对称二叉树”，除了满足所有二叉查找树的要求之外还需要满足以下要求：

- 任意节点的左子树不空，则左子树上的所有节点的值均小于它的根节点的值；
- 任意节点的右子树不空，则右子树上的所有节点的值均大于它的根结点的值；
- 任意节点的左右子树也分别为二叉查找树；
- 没有键值相等的节点；
- 节点是红色或者黑色；
- 根节点是黑色，所有叶子都是黑色；
- 每个红色节点必须有两个黑色的子节点；（从每个叶子到根的所有路径上不能有两个连续的红色节点）
- 从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点；

注：

NIL节点就是空寂欸但，二叉树中用NIL节点代替NULL

> 通过节点颜色，限制了二叉树的高度。
>
> 操作比如插入、删除、查找某个值的最坏情况时间都要求与树的高度成比例，在这个高度上的理论上限允许红黑树在最坏情况下都是高效的，而不同于普通的二叉查找树

![1688356226003](C:\Users\Asgard\Desktop\myNote\assets\1688356226003.png)

**红黑树两大操作**

​	1.recolor(重新标记为黑色或者红色)

​	2.rotation(旋转，这是树达到平衡的关键)



------

普通二叉树

- 完全二叉树
- 满二叉树

二叉查找树，也叫二叉排序树，BST

平衡二叉树，它是通过去除顶端优势，由BST转换过来，从而形成更加平衡的二叉树【左孩子的高度与右孩子的高度差绝对值不超过1】

- AVL
- 红黑树 Red Black Tree



# 4.0.0Lambda表达式

**函数式接口**：接口中只有一个抽象方法

在JDK8中。所有只有一个抽象方法的接口都可以使用Lambda来表示，这是因为JVM中约定了这个规则，并且在JDK中定义了一个注解来表示。

**如：**

java.lang.Comparator接口中，除了compare方法外，还有equals方法【继承于Object类】，所以，他也是符合函数式接口的要求的。

编译器会把任何符合函数式接口定义的接口视为函数式接口，而不管接口声明上是否添加了@FunctionalInterface注解



### 4.1.0 四大核心函数式接口

> JDK8中为了配合Lambda表达式的使用，定义了4种不同功能的接口，分别是：
>
> 1. 消费型接口，让调用者来决定数据的使用。
>2. 供应型接口，让调用者决定数据是怎么来的。
> 3. 判断型接口，【谓词】
>4. 功能型接口

#### 4.1.1 Consumer<T>接口

> 消费型接口，提供了消费函数

源码：

```java
@FunctionalInterface
public interface Consumer<T>{
    /**
     * Performs this operation on the given argument.
     *
     * @param t the input argument
     */
    void accept(T t);
    
default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```

**相应的子接口：**

IntConsumer, LongConsumer, DoubleConsumer, BiConsumer<T,U>

其中，BiConsumer<T,U>接口是可以接受2个参数的消费型接口，在JDK8中，Map接口提供了forEach方法，而这个方法就是以BiConsumer为参数的。



以下为Map接口中的forEach方法的源码：

```java
default void forEach(BiConsumer<? super K, ? super V> action) {
        Objects.requireNonNull(action);
        for (Map.Entry<K, V> entry : entrySet()) {
            K k;
            V v;
            try {
                k = entry.getKey();
                v = entry.getValue();
            } catch (IllegalStateException ise) {
                // this usually means the entry is no longer in the map.
                throw new ConcurrentModificationException(ise);
            }
            action.accept(k, v);//回调BiConsumer接口中的accept方法，传入key和value
        }
    }
```



#### 4.1.2 Supplier<T>接口

> 供应型接口，提供供应函数

源码：

```java
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

可以看出，此接口中定义了一个get函数，用来获取用户提供的对象T。



**相关的接口**

IntSupplier, LongSupplier, DoubleSupplier, BooleanSupplier等

每个接口都只返回相应类型的对象，所以，这些接口没有泛型字母。



#### 4.1.3 Function<T,R>接口

> 功能型接口，提供了apply功能型函数，这个接口中，第一个泛型字母T表示apply函数接收的参数，字母R表示apply函数返回的类型。它的作用是用来转换，将输入数据T转换为另一种形式的输出数据R。

源码：

```java
@FunctionalInterface
public interface Function<T, R> {

    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);
    
    //两个默认方法
    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }
    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }
    
    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```

流式编程API中，经常会使用Function接口

Function接口也有很多相关接口，如下；

IntFunction<R>, DoubleFunction<R>, LongFunction<R>, ToIntFunction<T>, ToDoubleFunction<T>, DoubleToIntFunction



#### 4.1.4 Predicate<T>接口

> 谓词型接口，提供了判断的回调函数

源码：【JDK11】

```java
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);
 
    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }
    
    default Predicate<T> negate() {
        return (t) -> !test(t);
    }
    
    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }
    
    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
    
    @SuppressWarnings("unchecked")
    static <T> Predicate<T> not(Predicate<? super T> target) {
        Objects.requireNonNull(target);
        return (Predicate<T>)target.negate();
    }
}    
```

#### 4.1.5 方法引用

提供以下4种方式的引用

1. **构造器引用**

   语法： Class::new 或 Class<T>::new 

   注：  这里的引用的构造方法是空参的。

   如：

   String::new 转换成对应的Lambda表达式就是:() -> new String()

2. **静态方法引用**

   语法：  Class::static_method

3. **类的任意对象方法引用**

   语法：Class::instanceMethodName

   **注：此方式下，lambda表达式的第一个入参为实例方法的调用者，后面的入参与实例方法的入参一致**

4. **实例方法引用**

   语法：object::instanceMethodName

> 注：带不带参数，是由目标接口的抽象方法决定的。

#### 4.1.6 Optional接口

> Optional不是一个函数式接口，而是一个精巧的工具接口，用来防止NullPointerExpection产生。

Optional是一个简单的值容器，这个值可以是null，也可以是non-null。考虑到一个方法可能会返回non-null的值，也可能返回一个空值。为了不直接返回null，我们在Java8中就返回一个Optional。



### 4.2.0  Stream API详解

> Stream API将处理的数据看作一种Stream（流），Stream（流）在Pipeline（管道）中传输和运算，支持的运算符包含筛选、排序、聚合等，当达到终点后便得到最终的处理结果。

**关键概念：**

1. **元素** 是一个来自数据源的元素队列，Stream本身并不存储元素。
2. **数据源** （即Stream的来源）包含集合、数组、IO channel、generator（发生器）等。
3. **聚合操作** 类似SQL中的filter、map、find、match、sorted等操作
4. **管道运算** Stream在Pipeline中运算后返回Stream对象本身，这样的多个操作串联成一个Pipeline，并形成fluent风格代码。这种方式可以优化操作，如延迟执行（laziness）和短路（short-circuiting）。
5. **内部迭代** 不同于Java8以前对集合的遍历方式（外部迭代），Stream API采用访问者模式（Visitor）实现了内部迭代。
6. **并行运算** Stream API支持串行（stream() ）或并行（parallelStream() ）两种操作

#### 4.2.1 Stream API的特点

1. Stream API的使用和同样是java8新特性的`lambda表达式`密不可分，可以大大提高编码效率和代码可读性。
2. Stream API提供串行和并行两种操作，其中并行操作能发挥多核处理器的优势，使用`fork/join`的方式进行并行做出以提高运行速度。
3. Stream API进行并行操作无需多线程代码即可高效的并发程序，且通常可避免多线程代码出错的问题

**创建流的方式**

1. **集合**直接调用stream()或者parallelStream()方法来创建流
2. **数组**可以通过`Arrays.stream(数组)`来得到一个流
3. 通过`Stream.of(T ... values)`来得到一个流，这个方法的底层就是`Arrays.stream(数组)`
4. 通过`Stream.iterator()`方法
5. 通过`Stream.generate()`方法

#### 4.2.2 流的操作

> 大致可以分为两大类
>
> 1. 中间操作，这些方法返回接口类型，以便可以连续调用，如：filter，map等
> 2. 终端操作，这些方法返回除本接口以外的其他类型，表示本次流操作结束

**中间操作**

- filter()
- limit()
- skip()
- map()
- sorted()
- distinct()

**终端操作**

- forEach()
- forEachOrdered() 适用于并行计算的流
- count()
- anyMatch()
- allMatch()
- noneMatch()



#### 4.2.3 reduce操作

> reduce是一种归约操作，将流归约为一个值的操作叫做归约操作，用函数式编程语言的术语来说，这种叫做折叠（flod）

案例：

```java
public class StreamEndOperation {
    public static void main(String[] args) {
        List<Integer> integerList = Stream.iterate(1, x -> ++x).limit(10).collect(Collectors.toList());
        //求intList集合中的所有元素之和
        int total = integerList.stream().reduce(0, new BinaryOperator<Integer>() {
            //此处的参数t，第一次会被0填充[也就是reduce方法的第1个参数]，从第2次执行，t就是apply方法				的返回值
            //参数u，是被遍历的集合的元素，每执行1次，传入一个元素
            @Override
            public Integer apply(Integer t, Integer u) {
                System.out.println(t + " -> " + u);
                return t + u;
            }
        });
        System.out.println(total);

        total = Stream.iterate(0, (x) -> x + 1).limit(10).reduce(0, (t, u) -> t + u);
        System.out.printf("total: %d\n", total);
        System.out.println("--------------------------");
        
        integerList.stream().reduce(new BinaryOperator<Integer>() {
            //先从流中取出2个元素，分别赋值给t和u，后面操作与reduce(T seed,BinaryOperator)是一样的
            @Override
            public Integer apply(Integer integer, Integer integer2) {
                return integer + integer2;
            }
        });
    }
}
```



#### 4.2.4 collect操作

> 这是一个收集的操作，把归约的操作的结果进行收集，做进一步的处理，比如：以集合方式存储、分组、分区、统计、平均、join操作



#### 4.2.5 Collectors工具类

> 用来创建Collector接口实例的工具类，提供了大量的工具方法，如：toList，toSet，toMap，toCollection,join,mapping,counting,groupingby,toMap,sumarizingXXX,summingXXX等



## 5.0.0 反射

#### 什么是反射？

> Java反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取信息以及调用对象的方法的功能称为Java语言的反射机制。



>任何一个Java类型被JVM加载进来后，在JVM中都会使用Class来描述这个类，换句话说，任意的Java类型在JVM中都拥有唯一的Class实例



**重新认识Class**

> Class就是所有类型在JVM中的类型，也叫描述类型的类型，或元类型。

获取Class的三种方式

- Class.forName("类的全限定名")；
- obj.getClass();
- 类名.class



### 5.1.0 类加载

> 类的加载指的是将类的.class文件中的二进制数据读入到内存中，将其放在运行时数据区的方法内，然后在堆区创建一个java.lang.Class对象，用来封装类在方法区内的数据结构。



#### 5.1.1 类的加载过程

**七步：加载 ==》验证 ==》 准备  ==》 解析 ==》 初始化 ==》 使用 ==》 卸载**



#### 5.1.2 类加载器

**Java语言系统自带有三个类加载器：**

- BootStrap ClassLoader：最顶级的类加载器，主要加载核心类库，也就是我们环境变量下的rt.jar,resources.jar,charsets.jar和class等。
- Extention ClassLoader：扩展的类加载器。**JDK9后改为PlatformClassLoader**
- AppClass Loader：也称为SystemAppClass，加载当前应用的classpath的所有类

BootStrap ClassLoader > Extention ClassLoader > AppClass Loader



#### 5.1.3 双亲委派原则：

> 它的工作流程是：当一个类加载器收到类加载任务，会先交给其父类加载器区完成，因此最终加载任务都会传递到顶层的 启动类加载器，只有当父类加载器无法完成加载任务时，才会回到子类加载器区尝试执行加载任务。



**通过Class可以得到什么？**

> 任何一个Java类型被JVM加载进来后，在JVM中都会使用Class来描述这个类，换句话说，任意Java类型在JVM中都拥有唯一的Class实例【包含基本类型】

通过Class的API，我们可以获取：

- 类的包信息
- 类的修饰符
- 类的父类或者实现的接口
- 类的构造器
- 类的方法
- 类的属性
- ...

**所以，可以说，Class是反射操作的入口。**

**重要的方法**

**Class**

- getDeclaredConstructors();//获取所有声明过的构造器 getConstructors()获取所有非私有的构造器

**Constructor extends Executable**

- newInstance();
- setAccessible();

 ***ParameterizedType和TypeVariable有什么区别**

> TypeVariable是获取泛型字母，ParameterizedType是获取泛型字母所对应的类型



## 6.0.0 多线程

#### **什么是进程**

> 正在进行的程序，现代的操作系统都是多任务【多进程】、多用户的
>
> JVM就是一个进程【process】，当我们启动JVM时，就是启动了一个进程

#### 什么是线程

> 运行在进程内部的一种资源，同样是由操作系统负责调度，一个进程中的所有线程都会共享此进程中的资源，也有线程所独享的资源。
>
> 理论上来说，进程中可以启动很多个线程。
>
> 可以这么说，现代的软件都是基于线程的。

**一个软件程序可以有多个进程，每一个进程又包含多个线程**

注：不管是进程还是线程，都是操作系统级别的资源。

所以，进程和线程执行时，都需要OS的调度，所谓调度，就是给进程或线程所要执行的环境，这个环境就包含两个东西：

1. CPU时间片
2. 内存