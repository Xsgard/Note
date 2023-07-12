## 1.0.0 MySQL基础

### 1.1.0 数据类型

1. 数字型

   tinyint  //相当于byte 1个字节

   samllint //相当于short 2个字节

   mediumint  //3个字节

   int  //4个字节

   bigint  //相当于long  8个字节

   float

   double

2. 字符型

   char(length)  //定长字符

   varchar(length)  //可变长字符

   text  //文本类型

   json

3. 日期型

   date

   time

   datetIme

   timestamp

4. 枚举

   enum

5. 二进制类型

   clob [character large object]

   blob [binary large object]

### 1.2.0 约束信息

> 约束[constraints]，它是在原有数据类型的基础上作进一步限制。
>
> 1. 主键约束，也叫primary key，简称PK，它表示非空且唯一。一个表中最多只能定义一个主键约束。
> 2. 非空约束，也叫NOT NULL
> 3. 唯一性约束，也叫UNIQUE，表示列值不允许重复
> 4. 外键约束，叫做foreign key，简称FK，表示列值来自于其他列的值。注：只有主键列或唯一性列才能被引用为外键列。
> 5. 自定义约束，也叫Check约束，

#### 1.2.1 添加约束到列

1. 在列定义结束之前添加约束【列级语法】

   例：

   ```mysql
   CREATE table t_student_1(
   	id int auto_increment PRIMARY KEY,
   	name VARCHAR(128) NOT NULL,
   	age mediumint CHECK(age >5 and age<127),
   	brith date,
   	gender enum('男','女') DEFAULT '男'
   )
   ```

   **注：此语法不能跨列添加约束**

   

2. 在列定义结束之后添加约束【表级语法】

   ```mysql
   CREATE table t_student_2(
   	id int auto_increment ,
   	name VARCHAR(128),
   	age mediumint,
   	brith date,
   	gender enum('男','女') DEFAULT '男',
      -- 添加约束
       primary key(id),
       unique(name,gender), -- 跨列
       check(age>5 and age<127)
   )
   ```

   **注：此语法不能支持NOT NULL约束。**

   

```sql
CREATE table t_student(
	id int auto_increment,
	name VARCHAR(128),
	age mediumint,
	brith date,
	gender enum('男','女') DEFAULT '男',
	PRIMARY KEY(id)
)
```



#### 1.2.2 删除表结构

```mysql
DROP TABLE 表名 [cascade contraints]
```



#### 1.2.3 修改表结构

```mysql
ALTER TABLE 表名 
	子命令
-- 常用子命令：
-- 1.添加列
ALTER TABLE 表名 add colum_name datatype [default value] [约束信息]

-- 2.删除列
ALERT TABLE 表名 drop colum_name；

-- 3.修改列名
ALTER TABLE 表名 rename COLUMN column_name to new_colum_name;

-- 4.修改数据类型
ALTER TABLE 表名 modify colum_name datatype [default value] [约束信息]
```



























