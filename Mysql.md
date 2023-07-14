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



## 4.0.0 分组查询

```mysql
-- 语法
SELECT 
 [表别名.]列名 [as] [列别名],
 [表别名.]列名 [as] [列别名],
 ...,
 [表别名.]列名 [as] [列别名]
FROM 表名 [表别名] [inner|left outer|right out]JOIN 表名 [表别名] ON 关联条件
WHERE 子句     -- 行记录的过滤
GROUP BY 子句  -- 看待过滤后的数据记录的角度
HAVING 子句    -- 分组之后的进一步过滤
ORDER BY 子句;
```

**注：SELECT 后面的列要与GROUP BY 的列保持一致，除非使用组函数修饰**

#### 4.0.1 组函数

> 也叫多行函数/聚合函数，主要有：
>
> COUNT([DISTINCT] * | 列名 | 表达式) -- 统计行记录数
>
> SUM([DISTINCT] 列名 | 表达式) -- 统计列值之和
>
> AVG([DISTINCT] 列名 | 表达式))
>
> MIN([DISTINCT] 列名 | 表达式))
>
> MAX([DISTINCT] 列名 | 表达式))
>
> GROUP_CONCAT(列名|表达式)

**分组后的进一步过滤**

```sql
-- 找出平均工资超过2500的部门
select deptno,avg(sal) from emp group by deptno having avg(sal) > 2500;
```

> 注： where 子句是不能使用组函数的。而 having 子句可以。



### 4.1.0 子查询

> 查询中嵌套其它的查询，叫子查询，子查询的语法与普通查询一样，它可以放在任意位置，比如：做为子表，也就是放在select后面存在或做为查询条件【放在where子句中】、having子句中、分组子句、排序子句中。
>
> 注：子查询一定要使用() 括起来。
>
> ```sql
> select 列名[,...] ，(子查询)
> FROM 表名 (子查询) JOIN 表名 ON 关联条件
> WHERE 子句 (子查询)
> GROUP BY 子句
> HAVING 子句 （子查询)
> ORDER BY 子句(子查询)
> ```
>
> > **所以，子查询可以嵌套**



#### 4.1.1 子查询的分类

> 我们根据子查询中是否要与外部查询产生关系来分类，可以分为：
>
> 1. 相关子查询
>
>    > 就是指在子查询内部要使用外部查询的变量(外联查询中定义的别名)，这种子查询也可以使用关联查询来改写。
>
> 2. 无关子查询
>
>    > 就是指子查询内部不与外部查询产生关联(不使用外部查询的变量).

#### 4.1.2 TOPn 解决方案

-- 找出工资排名前3的员工

```sql
select ename,sal from emp order by sal desc limit 3;
-- 处此，limit 3 表示只取前3条记录
-- 或者：
select a.* from ( 
    select ename,sal from emp order by sal desc
) a
limit 3;
```

#### 4.1.3 子查询的特殊操作符

1. **exists 和 not exists** 用来判断某个子查询是否存在结果集

   ```sql
   --  找出各部门工资最高的员工
   select * from emp my
   where not exists
   -- 子查询
   (    select 1 from emp other      
    	where my.sal < other.sal and my.deptno=other.deptno) 
   order by my.deptno;
   ```

2. union 和 union all 用来求两个子查询结果并集，union all 含 重复记录。

   ```sql
   --
   select * from emp where sal > 1500
   UNION select * from emp where deptno = 10;
   --
   select * from emp where sal > 1500
   UNION ALLselect * from emp where deptno = 10;
   ```

   > 注：这种操作符要求两个子查询的列，在类型、顺序、个数上要保持一致。

3. intersect 用来求两个子查询的交集

   ```sql
   -- 
   select * from emp where sal > 1500
   intersect
   select * from emp where deptno = 10;
   ```

4. minus 求两个子查询的差集【一个子查询的结果减去另一个子查询的结果】

   ```sql
   -- 
   select * from emp where sal > 1500 minus
   select * from emp where deptno = 10;
   --  使用关联来模拟
   select distinct b1.* from
   (select * from emp where sal > 1500) b1
   JOIN
   (select * from emp where deptno = 10) b2
   -- 关联条件
   ON b1.empno != b2.empnoWHERE b1.deptno != b2.deptno;
   -- 
   select * from emp where sal > 1500 and deptno != 10;
   ```



## 5.0.0 数据库设计

> 把业务系统中的所有数据按照二维表的关系和格式进行设计，以满足业务系统数据支撑。
>
> 这里最主要的一个环节就是如何把业务系统中的数据结构类型转换成表结构。
>
> 业务系统中的数据结构类型 也就是 实体类【它是业务系统数据的载体】

**实体与表之间的映射，遵守如下规则：**

1. 实体类名 映射成 表名
2. 属性名 映射成 列名
3. 对象在内存中的标识【地址】映射主键【PRIMARY KEY】
4. 对象关系 映射成 外键【Foreign key】

> 不管在实体关系中是一对一、一对多、还是多对多，在 RDBMS中都是采用 外键 来表示关系。
>
> 一对一的情况下， 外键可以定义在任意表中，但是要加 唯一性约束 【是一种特殊的一对多】
>
> 一对多的情况下，外键定义在多的那一边。【外键 值是可重复的】
>
> 多对多的情况下， 要添加中间表【因为RDBMS中不能直接表达多对多】，把外键都定义在中间表中。



### 5.1.0 范式

#### 5.1.1 第一范式

> 表中的所有列都是原子的，不可以再分。

#### 5.1.2 第二范式

> 在满足1NF的基础上，表中的所有非主键列不存在**部份依赖**于主键列。
>
> 所谓部份依赖是指在一个具有联合主键的表中，有些列只是依赖于这个联合主键中的其中一列，而不是多列。

#### 5.1.3 第三范式

> 在满足2NF 的基础上，表中的所有非主键列不存在**传递依赖**于主键列。
>
> 所谓传递依赖是指非关键列A依赖于另一个非关键列B，而B又依赖于候选关键列C,则我们可以说，非关键列A传递依赖于候选 关键列C。

> 范式不是万能的，有时候还会故意违反。



## 6.0.0 视图

> 也是一种数据库对象，它是基于表的，并且与表共享存储空间。
>
> 可以把视图想象成表的“**窗户**”，我们在操作视图时，方法与表是一样的，同样可做CRUD操作，需要注意的是，我们对视图进行CUR操作时，会影响所在表的数据。

```sql
-- 语法
CREATE VIEW View_name[(column_list)]
AS
	select_statement
[WITH [CASCADE | LOCAL] CHECK OPTION]
```

备注：

> 使用是某个普通用户，则需要授予：CREATE VIEW 和 DROP VIEW权限
>
> ALGORITHM 指定系统采用何种算法来创建视图，默认是 UNDEFINED, 表示由系统自动选择
>
> WITH [CASCADE | LOCAL] CHECK OPTION , 默认是 CASCADE
>
> 表示在对视图进行CUD操作时，是否要遵守原来创建此视图时的SELECT语句的约束以及原表中的约束。

### 6.1.0 视图的分类

1. 简单视图

   > 视图的数据来源于一张表，并且创建视图的查询语句中没有使用表达式、函数。
   >
   > 简单视图可以做CUD操作【具体还要视情况而定】。

2. 复杂视图

   > 视图来源于多张表的联合查询，并且创建视图的查询语句中可以使用表达式、函数（含组函数）。
   >
   > 复杂视图大多数情况下都不能做 CUD 操作。

#### 6.1.1 视图操作

1. 用户要有创建视图的权限 [CREATE VIEW]
2. 如果要删除视图，额外要授予 删除视图 的权限 [?]
3. 管理者应该创建多种不同的视图，并分配不同的权限给予不同的用户，以便他们可以自动管理指定的视图。

>所以，我们使用视图，一般都是要与权限管理配合使用。



## 7.0.0 E-R图

> E-R 图的全称： Entity Relationship Diagram, 实体关系图
>
> 在JAVA的模型中，叫实体类图
>
> 在数据库模型中，叫关系图
>
> 所以，通过ER图，可以清晰地看到 实体类之间的关系，以及表之间的关系。
>
> 我们昨天讲过，实体类之间的多样性关系有：
>
> 一对一
>
> 一对多
>
> 多对多
>
> 这三种多样式关系，在RDBMS中，都是以 外键来表示的。
>
> 我们利用工具可以把已有的表结构生成E-R 图，也可以手动绘制好E-R图后，再重新生成表结构。

## 8.0.0 数据库事务

> 在MYSQL中，事务默认情况下是自动提交的[auto commit]. 也就是说，我们每执行一条命令，事务就自动提交一次。

### 8.1.0 事务的定义

> 一组相关的SQL操作， 也就是说事务的边界由业务来决定。

#### 8.1.1 事务的特性

> 四大特性 【ACID】
>
> 1. 原子性 Atomicity
>
>    > 处在同一个事务的操作不可分割。要么一起成功，要么一起失败。
>
> 2. 一致性 Consistency
>
>    > 事务结束后，内存中的数据状态与底层磁盘中的数据状态保持一致。
>
> 3. 隔离性 Isolation
>
>    > 多个事务之间互相隔离
>    >
>    > 所以，当多个事务同时去对同一个数据库对象【表】进行操作时，就会造成并发。此时，数据库提供了“锁”机制来做并发处理。
>    >
>    > 针对这个锁而言，在mysql数据库中，INNODB 引擎即支持表级锁，也支持行级锁。而MYISAM引擎只支持表级锁。
>
> 4. 持久性 Durability
>
>    > 事务一旦正确提交，则RDBMS要保证数据不再丢失。

#### 8.1.2 事务并发

> 当多个事务同时去对同一个数据库对象【表】进行操作时，就会造成并发
>
> MYSQL 采用锁机制来解决事务并发问题，而MYSQL的INNODB引擎支持两个级别的锁，分别是：
>
> 1. 表级锁， 粒度较大，性能开销较小，但是并发性低
>
>    语法：
>
>    ```sql
>    LOCK TABLE table_name READ | WRITE   -- 显示调用
>    ```
>
> 2. 行级锁， 粒度较小，性能开销较大， 但是并发性能高， 行级锁是自动申请的，其中，我们执行DML操作都，RDBMS都会自动为当前事务分配行级排它锁。
>
>    一个表只有1个表级锁，它的每一行记录都有1把行级锁。

#### 8.1.3 事务操作

1. 手动开始事务

   ```sql
    begin
    -- 或
    start transaction
   ```

2. 调用你的SQL命令

   ```sql
   insert ...
   update ...
   delete ...
   ```

3. 结束事务

   ```sql
   -- 提交事务
   commit;
   -- 回滚事务
   rollback;
   ```

#### 8.1.4 事务的隔离级别

> 在mysql中，采用INNODB存储引擎时，默认的事务隔离级别是 **REPEATABLE READ**

1. READ UNCOMMITTED 可以读取没有提交的事务中的数据，也就是允许脏读[dirty read]

2. READ COMMITTED 可以读取已提交的事务中的数据。 不允许脏读

3. REPEATABLE READ 不可重复读，在同一个事务中，连续执行2次相同的SELECT命令，读到的列值不一样。

   > 因为**查询语句默认情况下是不申请行级排它锁**的，所以，在T1事务的2次执行SELECT命令的间隔之中，T2事务可以去执行更新命令，并且提交事务。
   >
   > 所以，才会造成 不可重复读的现象。

4. Serializable 串行化，不可幻读， 在同一个事务中，连续执行的2次SELECT count(*) 命令，得到的结果不一样。

> 幻读, 是指在T1事务的2次执行SELECT命令的间隔之中，T2事务可以去执行 INSERT 命令，并且提交事务。
>
> 所以，才会造成 幻读。

所以，如果把事务的隔离级别调整到 Serializable，那么可以防止 幻读、不可重复读、脏读。 但是，并发性是最低的。

事务隔离级设为 REPEATABLE READ ， 可以防止 不可重复读、脏读，但是可以 幻读

事务隔离级别设为 READ COMMITTED, 可以防止 脏读，不能防止 不可重复读和幻读

事务隔离级别设为 READ UNCOMMITED, 允许脏读、 不可重复读和幻读

### 不可重复读和幻读 是如何加锁的

不可重复读 就是针对 SELECT 语句进行加锁，通过 FOR UPDATE 子句。

```sql
select * from t_student FOR UPDATE [nowait];   
```

幻读 是通过锁表实现的，如下：

```sql
LOCK TABLE table_name READ | WRITE;
-- 备注：
-- 在 READ 模式下，其它事务可以做 SELECT 操作
-- 在 WRITE 模式下，其它事务不能做任何操作，完全的串行化。
-- 释放锁UNLOCK TABLES;
```

### 查看和设置当前会话的事务隔离级别

```sql
--  查看
select @@transaction_isolation
-- 设置 set session transaction isolation level 
级别级别有如下四种：
read uncommitted
read committed
repeatable read
serializable
```



## 9.0.0 索引【index】

> 是数据库在查询时的一种优化、提高查询效率的一种方式。
>
> 它本身也是数据库对象，有独立的存储空间和命名空间。默认情况下，索引采用BTREE结果来存储。

### 9.1.0 索引创建的方式

1. 自动创建

   > 当我们给表中的列添加了 主键约束或唯 一性约束时，RDMBS会自动帮我们创建唯一性索引。
   >
   > 注：只有当我们的查询条件是创建了索引的列时，RDBMS才会帮助我们使用索引进行查询。

2. 手动创建

   ```sql
   -- 语法
   CREATE INDEX index_name ON table_name(column_name[,column_name]) [visible]
   ```

#### 9.1.1 何时该创建 索引？

1. 列中的NULL太多时，不适合创建索引
2. 列中的值重复率高时，不适合创建索引
3. 列经常做更新时，不适合创建索引

所以，与上面情况相反的情况，就比较适合建索引。

#### 9.1.2 有了索引后，RDBMS是如何做查询的？

1. RDBMS会自动判断出你的查询条件列是否加了索引
2. 首先，去查询索引，找到“行记录的物理位置”
3. 其次，再根据“行记录的物置位置”去表中定位记录。
4. 最后，把记录返回给结果集

#### 9.1.3 索引失效

> 1. 你的查询条件没有使用 添加了索引列
> 2. 查询条件中使用了表达式或函数

### 索引小结：

1. 查询条件尽可能使用主键或唯一性建。
2. 能不用函数尽量不要在查询条件中使用函数或表达式。

