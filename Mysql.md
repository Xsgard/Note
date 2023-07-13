## 1.0.0 MySQL基础

### SQL

> SQL标准是针对关系型数据库管理系统的一套标准，全称是：Structure Query Language，它有多种不同的命令，主要有：

1. DDL命令，Data Definition Language，数据定义语句，主要包含的命令有：
   1. CREATE 命令
   2. DROP 命令
   3. ALTER 命令
2. DCL命令，Data Control Language，数据控制语句，主要包含的命令有：
   1. grant 命令，用来给用户授权
   2. revoke 命令。用来回收权限
3. DQL命令，Data Query Language，数据查询语句，主要包含的命令有：
   1. SELECT 命令 【*】
4. DML命令，Data Manipulate language，数据操作语句，主要命令有：
   1. INSERT 命令，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，
   2. UPDATE 命令
   3. DELETE 命令
5. DTL命令，Data Transaction Language，数据事务语句，主要命令有：
   1. COMMIT 命令
   2. ROLLBACK 命令
   3. SAVEPOINT 命令

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



## 2.0.0 DQL

### 2.1.0 基础查询

```mysql
-- 语法
SELECT 
	[表别名.] 列名1 [as] 列别名，
	[表别名.] 列名2 [as] 列别名，
	[表别名.] ...  [as] 列别名
	[表别名.] 列名N [as] 列别名  |*
FROM 表名 [表别名];
```

MySQL还支持数学运算。

如：

```mysql
select 3+28/7;
select sin(0.5);
```

除了支持数学运算外，还提供很多函数，如：

```mysql
select user();-- 返回当前 用户@主机
select now(); -- 返回当前系统日期和时间
select current_date();  -- 返回当前系统日期，不含 时间
select current_time();  -- 返回房前系统时间，不含 日期
select rand();  -- 返回一个[0,1.0)的随机数
...
```



### 2.2.0 排序子句

语法：

```mysql
SELECT 
	[表别名.] 列名1 [as] 列别名，
	[表别名.] 列名2 [as] 列别名，
	[表别名.] ...  [as] 列别名
	[表别名.] 列名N [as] 列别名  |*
FROM 表名 [表别名]
ORDER BY 列名[,列名2] | 列的位置 | 表达式 [ASC|DESC]
```

> 注：排序子句最后执行

### 2.3.0 条件查询

> 针对数据记录有条件的过滤【检索】，通过WHERE子句，它可以支持各种运算符

```mysql
SELECT 
	[表别名.] 列名1 [as] 列别名，
	[表别名.] 列名2 [as] 列别名，
	[表别名.] ...  [as] 列别名
	[表别名.] 列名N [as] 列别名  |*
FROM 表名 [表别名]
WHERE 子句
ORDER BY 子句;
```

> 针对WHERE子句，它支持各自运算符，如：
>
> 1. 比较运算符：>,<,=,>=,<=,!=,<>
> 2. 逻辑运算符：&&(AND), ||(OR), !(NOT)
> 3. 算术运算
> 4. 通配运算：like和not like，它支持的通配符如下：
>    - _ 通配任一单个字符
>    - % 通配任意多个字符
> 5. IN运算符，语法：IN(List)
> 6. IS NULL和 IS NOT NULL
> 7. BETWEEN start AND end
> 8. REGEXP 采用正则表达式匹配



### 2.4.0 函数 function

> 由RDBMS开发好的一组逻辑代码的整合，可以直接调用

1. **字符函数**

   - length(表达式|列|字面量)	返回参数的字节长度
   - char_length(表达式|列|字面量) 返回参数的字节长度
   - substring(参数)   求子串
   - lpad(参数)   左填充
   - rpad(参数)   右填充
   - ltrim(参数)   左去空字符
   - rtrim(参数)  右去空字符
   - instr(参数)  查询参数位置
   - concat(参数)  拼接
   - upper(参数)  转大写
   - lower(参数)  转小写
   - uuid() 随机生成

2. **日期函数**

   - year(日期)
   - month(日期)
   - day(日期)
   - minute(日期)
   - hour(日期)
   - second(日期)
   - weekday(日期)
   - week(日期)
   - now();
   - current_date();
   - current_time();
   - last_day(日期)
   - datediff(日期1，日期2)

   注：

   在mysql中，日期的默认格式是：yyyy-MM-dd

   而且，mysql中，自动会免除Y2K问题。即使我们录入年份时，采用2位，MYSQL后台会自动转换4位。

   我们输入2位年份时的计算规则：

   1. 大于69年，就以上个世纪来换算成4位年份
   2. 小于69[含]，就以本世纪来换算成4位年份。

3. **数字函数**

   - round(参数)
   - truncate(参数) 截取
   - rand()
   - ceil() 向上取整
   - floor() 向下取整

4. **加密函数**

   - md5()
   - sha1()



## 3.0.0 DML

> 数据定义语言

### 3.1.0  INSERT命令

```mysql
INSERT [INTO] 表名(列名[,列名][,...][,列名]) VALUES (值1[,值2][,...][,值n]);
或一次插入多行
INSERT [INTO] 表名(列名[,列名][,...][,列名]) VALUES 
(值1[,值2][,...][,值n]),
(值1[,值2][,...][,值n]),
(值1[,值2][,...][,值n]),
(值1[,值2][,...][,值n]);
或
INSERT [INTO] 表名 VALUES (值1[,值2][,...][,值n]); -- 要求值与创建表时的列顺序和个数保持一致，并且列的默认值是不起作用的。
```

### 3.2.0 利用子查询来插入

```mysql
-- 语法
INSERT INTO 表名(列名[,列名][,...][,列名])
	SELECT 语句; -- 查询出来的列的个数和类型 都要与 被插入的表中保持一致。
```

### 3.3.0 更新命令 UPDATE

```mysql
-- 语法
UPDATE 表名 SET 列1=值1 [,列2=值2][,...][,列n=值n]
[WHERE 子句];
-- 如果不使用WHERE 子句，则表示更新所有行记录。如果使用了WHERE子句，则只更新满足条件的行记录。
```

### 3.4.0 删除命令 DELETE

```mysql
-- 语法
DELETE [FROM] 表名 [表别名]
[WHERE 子句];
```

### 3.5.0 关联查询 JOIN

> 从多个表中查询数据。

```mysql
-- 语法
SELECT 
	[表别名.] 列名1 [as] 列别名，
	[表别名.] 列名2 [as] 列别名，
	[表别名.] ...  [as] 列别名
	[表别名.] 列名N [as] 列别名  |*
FROM 表名 [表别名] [inner|left outer|right out] JOIN 表名 [表别名] ON 关联条件
WHERE 子句
ORDER BY 子句;
```

关联可以分为：

1. 内联接，使用 inner join, 其中， inner 可以省略

   > 只有当关联条件在左右两边都满足的情况，才会进入到结果集

2. 外联接

   - 左外联, 使用 left outer join, 其中,outer可以省略

     > 以关联的左边为准，即使右边没有与之匹配的记录，那左边的记录也要进入结果集

   - 右外联, 使用 right outer join, 其中,outer可以省略

     > 以关联的右边为准，即使左边没有与之匹配的记录，那右边的记录也要进入结果集

#### 3.5.1 自身关联

> 同一个表，自已和自己产生关联。

例：

```mysql
select e.EMPNO, e.ENAME, d.EMPNO, d.ENAME
from emp e
         join emp d on e.MGR = d.EMPNO;
```

#### 3.5.2 左外关联

```mysql
select e.ENAME "员工名", ifnull( d.ENAME,"董事会") "上司名"
from emp e
        left join emp d on e.MGR = d.EMPNO ;
```

#### 3.5.3 右外关联

```mysql
select e.ENAME "员工名", ifnull( d.ENAME,"董事会") "上司名"
from emp e
        right join emp d on e.MGR = d.EMPNO ;
```

#### 3.5.4 多表关联

```mysql
-- 查询出用户 jack 的角色信息
select u.username,r.*
from sys_user u join sys_user_role ur on u.id = ur.user_id
join sys_role r on ur.role_id=r.id
where u.username='jack';
```



