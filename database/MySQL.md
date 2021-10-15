# MySQL学习

## 一、初识MySQL

### 1.1 为什么

- 前端：展示数据
- 后台：链接数据库JDBC，链接前端

- ==数据库是所有软件体系中最核心的存在==

### 1.2 什么是

- 数据库(DB，DataBase)

- 概念：数据仓库，软件，安装在操作系统上的SQL可存储大量数据(500w)

- 作用：存储数据、管理数据

- 基本特点：数据库是长期存储在计算机内、有组织的、可共享的大量数据的集合。数据库中的数据按一定的数据模型组织、描述和储存，具有较小的冗余度、较高的数据独立性和易扩展性，并可以为各种用户共享。

    >   概括：永久存储、有组织、可共享

### 1.3 分类

#### 1. 关系型数据库(SQL)

- 常见：MySQL、Orcale、SQL Server、DB2、SQLlite、PostgreSQL
- 特点：通过表和表之间，行和列之间的关系进行数据的存储

#### 2. 非关系型数据库(NoSQL)

- 常见：Redis、MongoDB

- 特点：非关系型数据库的对象存储通过对象自身的属性来决定

#### 3. ==数据库管理系统(DBMS)==

- 管理数据库的软件，属于系统软件，计算机的基础软件
- 能够科学有效的管理我们的数据。维护和获取数据
- MySQL是数据库管理系统

#### 4. MySQL简介

- MySQL是一个**关系型数据库管理系统**
- 前世：瑞典MySQL AB公司
- 今世：美国Oracle公司
- MySQL是最好的RDBMS(Relational Database Management System)应用软件之一。
- 开源的数据软件
- 体积小、速度快、总体拥有成本低
- 常用版本：5.7(稳定、企业常用)
- [官网](https://www.mysql.com)

### 1.4 MySQL下载安装

- 下载压缩包安装

- 解压到目录

- 添加到系统环境

- 新建配置文件`my.ini`

    ```ini
    [mysqld]
    port=3306
    basedir=D:\DevTools\mysql-8.0.11-winx64
    datadir=D:\DevTools\mysql-8.0.11-winx64\Data
    #mysql_native_password
    #skip-grant-tables:取消密码验证
    ```

- 进入`bin`目录以管理员身份运行CMD执行以下命令：

    ```bash
    #安装MySQL
    mysqld -install
    
    #初始化数据文件
    mysqld --initialize-insecure --user=mysql
    
    #启动服务
    net start mysql
    
    #进入mysql
    mysql -u root -p
    
    #更改root密码刷新权限后退出
    update mysql.user set authentication_string=password('xxx') where user='root' and Host='localhost';
    flush privileges;
    
    #重启服务
    net stop mysql
    net start mysql
    ```

### 1.5 SQL简介

**SQL**((Structured Query Language，结构化查询语言)分类：

- **DDL**(Data Definition Language，数据库模式定义语言)：描述数据库中存储现实实体语言
- **DML**(Data Manipulation Language，数据管理语言)：对数据库作插，删，改，排，检等五种操作
- **DCL**(Database Control Language，数据控制语言)：用来设置或者更改数据库用户或角色权限的语句
- **TCL**(Transaction Control Language，事务控制语言)：控制事务
- **DQL**(Database Query Language，数据查询语言)：查询数据

## 二、操作数据库==DDL==

>   操作数据库-->操作数据库中的表-->操作数据库中表的数据
>
>   ==MySQL的sql语句不区分大小写，但推荐使用大写，语句需要以分号(;)或'\g' 或'\G'结尾==
>
>   ==如果表名或字段名是特殊字符(关键字等)需要用``修饰==
>
>   ==sql语句行注释用'-- '块注释用'/**/'==
>
>   ==本文SQL中方括号选中部份为可选部份不是必须的！！！使用时将方括号去掉==

### 2.1 操作数据库(了解)

#### 1. 创建数据库

```sql
create database [if not exists] dbname;
```

#### 2. 删除数据库

```sql
drop database [if exists] dbname;
```

#### 3. 使用数据库

```sql
use dbname;
```

#### 4. 查看数据库

```sql
show databases;
```

### 2.2 数据库列的数据类型

#### 1. 数值

整数：

-   **tinyint**：最小的数值类型，占1B
-   **smallint**：较小的数值类型，占2B
-   **mediumint**：中等大小的数值类型，占3B
-   ==**int**：标准整型，最常用，占4B ，最大长度11==
-   **bigint**：较大的数据类型，占8B

浮点数：

-   **float**：单精度浮点数，占4B
-   **double**：双精度浮点数，占8B
-   ==**decimal**：字符串形式的浮点数，常用于金融计算，形式 **decimal(整数位长度,小数位长度)**==

#### 2. 字符串

-   **char**：固定大小的字符串，长度范围0~255
-   ==**varchar**：可变字符串，最常用，长度范围0~65535==
-   **tinytext**：微型文本，最大长度2^8-1
-   ==**text**：文本串，常用来保存大文本，最大长度2^16-1==

#### 3. 日期时间

-   **date：YYYY-MM-DD** 格式的日期
-   **time：HH:mm:ss** 格式的时间
-   ==**datatime：YYYY-MM-DD HH:mm:ss** 最常用的时间类型==
-   ==**timestamp**：时间戳，1970.1.1到现在的毫秒数，也较为常用==
-   year：年份表示

#### 4. 空值(null)

-   表示没有值或值未知
-   ==不要使用null进行运算(没有意义结果必为null)==
-   **==任何值与null进行比较结果必为false，如not in的原理是依次进行!=判断，如果not in (表达式)中有null值则not in的结果也必是空值，所以在用not in时注意后面的表达式中不能有空值最好加上 where xxx is not null==**

### 2.3 ==数据库的字段属性(约束条件)(重点)==

#### 1. **unsigned**

-   无符号数值，只适用于数值类型

-   声明该列不能为负数

-   例子：

    ```sql
    -- 创建表时添加
    create table if not exists `table_name`(
    	...
        `col_name` int(10) unsigned
        ...
    );
    
    -- 修改时添加和创建表时添加基本相似故在之后不写建表的例子
    alter table `table_name`
    	-- column可加可不加经测试对结果无影响，下文不再重复
    	modify [column] `col_name` int(10) unsigned;
    
    -- 删除 通过不写属性来删除
    alter table `table_name`
    	modify `col_name` int(10);
    ```

#### 2. **zerofill**

-   0填充，只适用于数值类型

-   不足的位数在前面补0，如int(5)  123-->00123 

-   例子：

    ```sql
    -- 修改时添加
    alter table `table_name`
    	modify `col_name` int(10) zerofill;
    
    -- 删除
    alter table `table_name`
    	modify `col_name` int(10);
    ```

#### 3. **auto_increment**

-   自增：默认在上一条记录的基础上 +1(默认)

-   通常用来设计**唯一**的主键，只适用于整数类型，只适用于设置键的字段

-   每个表最多只允许存在一个自增长列，即使它有组合主键。

-   可以自定义设计主键自增的起始值和步长

-   例子：

    ```sql
    -- 修改时添加
    alter table `table_name`
    	modify `col_name` int(10) auto_increment;
    
    -- 查看自增长设置
    show global variables like 'auto_inc%'; -- 针对全局
    show session variables like 'auto_inc%'; -- 针对会话
    
    -- 设置自增初始值为x
    -- 针对单个表
    create table if not exists `tabel_name`(...) auto_increment=x;
    alter table `table_name` auto_increment=x;
    -- 针对当前会话(session，一次连接)过程中创建的所有表，退出连接后恢复为默认值
    set session auto_increment_increment=x;
    -- 针对全局
    set global auto_increment_increment=x;
    
    -- 设置自增步长为x
    set session auto_increment_offset=x;    -- 会话
    set global auto_increment_offset=x;     -- 全局
    
    -- 初始值计算
    -- 假设a为表中id列的最大值，b为auto_increment的初始值，c为步长，则auto_increment真正的初始值为：
    -- auto_increment_real  =  int( a/b) * c + c  ;
    
    -- 删除
    alter table `table_name`
    	modify `col_name` int(10);
    ```

#### 4. **not null**

-   非空约束，当设置为`not null`时，插入数据时该列不能为空值否则报错

-   `null`，如果不填写值，默认就是`null`

-   例子：

    ```sql
    -- 创建表时添加
    create table if not exists `table_name`(
    	...
        `col_name` int(10) not null
        ...
    );
    
    -- 修改时添加
    alter table `table_name`
    	modify `col_name` int(10) not null;
    
    -- 删除
    alter table `table_name`
    	modify `col_name` int(10);
    ```

#### 5. default

-   默认约束，当插入，或修改数据没有给出该列值时会自动填入`default`规定的值

-   不适用于`text`等类型

-   例子：

    ```sql
    -- 创建表时添加
    create table if not exists `table_name`(
    	...
        `col_name` int(10) default 0
        ...
    );
    
    -- 修改时添加
    alter table `table_name`
    	modify `col_name` int(10) default 0;
    
    -- 删除
    alter table `table_name`
    	modify `col_name` int(10);
    ```

#### 6. unique

-   唯一键约束：确保每一个值唯一，可以为空值和，unique index相同

-   与其他数据库系统不同，MySQL将NULL值视为不同的值。 因此，您可以在`UNIQUE`索引中具有多个`NULL`值。

-   例子：

    ```sql
    -- 创建表时添加
    create table if not exists `table_name`(
    	...
        `col_name` int(10) unique
        ...
    );
    create table if not exists `table_name`(
    	...
        `col_name` int(10),
        constraint uni_col unique key(`col_name), -- 将字段x设置为唯一，并为该键起一个别名
        x int(10),
        unique key(x)
    );
    -- 多个unique字段，不能同时一样
    create table if not exists `table_name`(
    	`col_name_1` int(10),
        `col_name-2` decimal(10),
        unique key(`col_name_1`, `col_name_2`)
    );
    -- 修改时添加
    create unique index unique_name on `table_name`(column_1,column_2,...)
    ALTER TABLE `table_name`
    	add constraint constraint_name UNIQUE KEY(column_1,column_2,...)
    
    -- 查看
    show index from `table_name`;
    
    -- 删除
    alter table `table_name`
    	drop index `col_name`;
    ```

#### 7. primary key

-   主键约束：确保每一个值唯一，非空等价于`unique not null`

-   例子：

    ```sql
    -- 创建表时添加
    create table if not exists `table_name`(
    	...
        `col_name` int(10) primary key 
        -- 或者constraint pk_name primary key(id); #创建主键并为其命名pk_name
        ...
    );
    -- 复合主键
    create table if not exists `table_name`(
    	`col_name_1` int(10),
        `col_name-2` decimal(10),
        primary key(`col_name_1`, `col_name_2`)
    );
    
    -- 修改时添加可多可少
    Alter table `table_name`
    	Add primary key(col1, col2...)
    
    -- 删除
    alter table `table_name` drop primary key;                   -- 单列主键
    ALTER TABLE `table_name` DROP PRIMARY KEY ,ADD PRIMARY KEY (`id`);   -- 复合主键
    ```

#### 8. foreign key

-   外键约束：关联2张表

-   例子：

    ```sql
    -- 1、约束1：有了foreign key在创建表时，----必须先建被关联的表dep，才能建关联表emp
    
    create table dep(
        id int primary key auto_increment,
        dep_name char(10),
        dep_comment char(60)
    );               -- 要先创建被关联的表，因为关联的表中有被关联表的id,否则先创建关联的表，此时
    
    
    -- 被关联的字段通常是一个key,
    create table emp(
        id int primary key auto_increment,
        name char(16),
        gender enum('male','female') not null default 'male',
        dep_id int,
        foreign key(dep_id) references dep(id)          -- 自己表中的dep_id关联到dep中的id
    );
    -- 2、约束2：在插入记录时，必须先插被关联的表dep，才能插关联表emp
    insert into dep(dep_name,dep_comment) values
    ('sb教学部','sb辅导学生学习，教授python课程'),
    ('外交部','老男孩上海校区驻张江形象大使'),
    ('nb技术部','nb技术能力有限部门');
    
    
    insert into emp(name,gender,dep_id)  values
    ('alex','male',1),
    ('egon','male',2),
    ('lxx','male',1),
    ('wxx','male',1),
    ('wenzhou','female',3);
    
    -- 删除是则子相反，删除则是关联的表优先，有限成为被删除的对象
    -- 3、约束3：更新与删除都需要考虑到关联与被关联的关系
    -- 解决方案：
    -- 1、先删除关联表emp，再删除被关联表dep，准备重建
    drop table emp;
    
    -- 删除外键
    alter table `table_name` drop foreign key `FK_name`;
    ```

#### 9. costraint关键字

-   **constraint**：约束关键字，创建约束及声明约束和索引名(主要是声明索引名)
-   mysql约束：not null/unique/primary key/foreign key
-   除了not null之外，创建约束就相当于同时创建了约束和索引
-   使用constraint  constraint_name primary key(xxx)创建主键时constraint声明的主键名和索引名无效，默认为系统提供的primary
-   key与index 一样，只创建索引，不创建约束
-   当不使用constraint创建约束时，索引和约束名会由系统自动生成
-   列级约束是定义在列属性中的，而表级约束是定义在列之后的，两者本质上没什么区别，而如果你的约束需要同时对多列进行约束那么就只能采用表级约束，因为表级约束面向的是表（当然就包括所有列），而列级约束只能针对该列进行约束。not null 只有列约束，foreign key只有表约束

###  2.4 创建数据库表(重点)

-   ==格式：背下来==

```sql
CREATE TABLE [IF NOT EXISTS] `table_name`(
    -- 字段名       类型名     约束条件、索引(可以多个)  字段注释
	`field_name_1` type_name [constraint] [index] [comment ''],
    ...
    `field_name_n` type_name [constraint] [index] [comment ''];
-- 引擎     默认编码          表注释
)[engine=][default charset=][comment '']
```

-   常用命令

```sql
show create database `db_name`;	-- 查看建库语句
show create table `table_name`;	-- 查看建表语句
desc `table_name`;				-- 查看表结构
```

### 2.5 表的引擎类型

-   INODB：默认使用
-   MYISAM：早些年使用
-   查看MySQL支持哪些引擎：==show engines;==

|  功能特性  | MYISAM |        INNODB         |
| :--------: | :----: | :-------------------: |
|  事务支持  | 不支持 |         支持          |
| 数据行锁定 | 不支持 |         支持          |
|  外键约束  | 不支持 |         支持          |
|  全文索引  |  支持  | 版本大于等于5.6的支持 |
| 表空间大小 |  较小  |   较大，约为前者2倍   |

常规使用操作的区别：

-   MYISAM：节约空间、速度较快
-   INNODB：安全性高、支持事务处理及多表多用户操作

在物理空间存在的位置：

-   所有数据库文件都存在data目录下，本质还是文件的存储。

MySQL引擎在物理文件上的区别：

-   INODB在数据库表中只有一个`*.frm`文件，以及上级目录下的ibdata1文件。
-   MYISAM对应文件：
    -   `*.frm`：表结构对应文件
    -   `*.MYD`：数据文件(data)
    -   `*.MYI`：索引文件(index)

### 2.6 修改数据表

常用语法：

```sql
-- 重命名表名
alter table `old_name` rename to `new_name`;

-- 添加字段
alter table `table_name` add `col_name` type [constraint];

-- 修改字段    表名                列名       新类型    约束
alter table `table_name` modify `col_name` new_type [constraint]; -- 利用modify不能重命名
-- 修改字段    表名                列名       新列名     新类型    约束
alter table `table_name` change `old_col` `new_col` new_type [constraint];-- change可以

-- 调整字段顺序 将col_1移到col_2后面
alter table `table_name` modify `col_1` type [constraint] after `col_2` type [constraint];

-- 删除字段   表名               列名
alter table `table_name` drop `col_name`;

-- 删除表(如果存在)
drop table if exists `table_name`
```

### 2.7 其他

-   注：

    >    ==**constraint**== ：约束关键字
    >
    >    约束条件往往对顺序和字段类型有要求，auto_increment一般放在最后等

-   拓展

    >   根据阿里巴巴开发手册，每一个表都必须要存在以下五个字段，表示一个记录存在的意义
    >
    >   id				     主键
    >
    >   version		    乐观锁
    >
    >   is_delete	      伪删除
    >
    >   gmt_create     创建时间
    >
    >   gmt_update    修改时间

-   参考：

    1.  [MYSQL创建表的约束条件（可选） - 迎风而来 - 博客园](https://www.cnblogs.com/sui776265233/p/9343690.html#_label5)
    2.  [MySQL中 auto_increment如何修改初始值和步长 -静若清池，动如涟漪_-CSDN博客_](https://blog.csdn.net/wangyongx_123/article/details/90315737)
    3.  [MySQL UNIQUE索引 - MySQL教程](https://www.yiibai.com/mysql/unique.html#:~:text=如果要使用多个列或一组具有唯一值的列，则不能使用主键约束。. 幸运的是，MySQL提供了另一种称为 UNIQUE 索引的 索引 ，它允许您在一个或多个列中强制实现值的唯一性。. 与 PRIMARY,CREATE UNIQUE INDEX index_name ON table_name (index_column_1%2Cindex_column_2%2C...)%3B SQL.)
    4.  [Mysql学习之constraint/key/primary key/unique/foreign key/constraint的关系_Swing_wingS的博客-CSDN博客](https://blog.csdn.net/Swing_wingS/article/details/92801561)
    5.  [MySQL——约束(constraint)详解_浅然的专栏-CSDN博客](

## 三、MySQL数据管理

### 3.1 外键(了解)

#### 1. 创建：

-   法一

```sql
-- 创表时直接创建
create table if not exists `tablename`(
	...
    `colname` int(5),
    ...
    --         键名              要生成外键的列名             要引用的表    要引用的列
    constraint FK_col foreign key (`colname`) references `other_table`(`other_col`)
);
```

-   法二

```sql
-- 添加外键
alter table `tablename`
	add constraint `fk_name` foreign key (`colname`) references `othertable`(`othercol`);
```

-   注意：以上操作都是物理外键，表级别的外键，不建议使用，避免数据表太多造成困扰

#### 2. ==最佳实践==

-   数据表就是单纯的表，只用来存数据，只有行(数据)和列(字段)
-   如果想使用多张表的数据可以依靠程序来实现

### 3.2 ==DML语句(重点，背下来)==

-   数据库意义：数据存储、数据管理
-   DML数据管理语言：关键字：
    -   insert
    -   update
    -   delete

#### 1. insert添加

-   常用语法

    ```sql
    -- 插入语句    表名       字段名(可以省略，省略后，值一一对应)   插入值
    insert into `table_name`[(`col_1`, `col_2`,...)] values(value1, value2,...);-- 插入单条语句
    insert into `table_name`[(`col_1`, `col_2`,...)] 
    	values(value11, value12,...),(value21, value22,...),...;                -- 插入多条语句
    ```

#### 2. update修改

-   常用语法

    ```sql
    -- 修改语句  表名         要修改的列  修改值   where条件语句(没有会修改整个表，不要漏！！！) 
    update `table_name` set `col_name` = xxx where `condition_col` = conditions; -- 修改单个值
    update `table_name` 														 -- 修改多个值
    	set `col_1`= xxx,`col_2`=yyy, ...										 -- 用逗号隔开
    	where `condition_col` = conditions;
    ```

-   where子语句运算符<a name="where table">  </a>

    |     操作符      |      含义      |     范围     | 结果  |
    | :-------------: | :------------: | :----------: | :---: |
    |        =        |      等于      |     5=6      | false |
    |    <> 或 !=     |     不等于     |  5<>6或5!=6  | true  |
    |        >        |      大于      |     5>6      | false |
    |        <        |      小于      |     5<6      | true  |
    |       >=        |    大于等于    |     5>=6     | false |
    |       <=        |    小于等于    |     5<=6     | true  |
    | between a and b | 某个闭区间范围 |    [5,6]     |       |
    |       and       |    逻辑与&&    |  5>1 && 1>2  | false |
    |       or        |   逻辑或\|\|   | 5>1 \|\| 1>2 | true  |
    |       not       |    逻辑非!     |      !3      | false |

-   注意：
    -   update语句后面一定要加上where子语句否则会修改全表
    -   value1，value2...可以是值也可以是变量

#### 3. delete删除

-   常用语法

    ```sql
    -- 删除语句	  表名		 条件(可省略，删除表中所有数据，不建议省略)
    delete from `table_name` [where condition];
    
    -- truncate：清空语句，清空一张表中所有数据
    truncate `table_name`;
    ```

-   **`delete`**和**`truncate`**区别

    |  功能特性  | TRUNCATE | DELETE |
    | :--------: | :------: | :----: |
    |  条件删除  |  不支持  |  支持  |
    |  事务回滚  |  不支持  |  支持  |
    |  清理速度  |    快    |   慢   |
    | 高水位重置 |    是    |   否   |

    -   **事务回滚**：由于DELETE是数据操作语言（DML），操作时原数据会被放到 rollback segment中，可以被回滚；而TRUNCATE是数据定义语言（DDL)，操作时不会进行存储，不能进行回滚。
    -   **清理速度**：在数据量比较小的情况下，DELETE和TRUNCATE的清理速度差别不是很大。但是数据量很大的时候就能看出区别。由于第二项中说的，TRUNCATE不需要支持回滚，所以使用的系统和事务日志资源少。DELETE 语句每次删除一行，并在事务日志中为所删除的每行记录一项，固然会慢，但是相对来说也较安全。
    -   **高水位重置**：随着不断地进行表记录的DML操作，会不断提高表的高水位线（HWM），DELETE操作之后虽然表的数据删除了，但是并没有降低表的高水位，随着DML操作数据库容量也只会上升，不会下降。所以如果使用DELETE，就算将表中的数据减少了很多，在查询时还是很和DELETE操作前速度一样。而TRUNCATE操作会重置高水位线，数据库容量也会被重置，之后再进行DML操作速度也会有提升。高水位重置后自增长归零。

### 3.3 其他

-   参考：
    1.  [MYSQL中TRUNCATE和DELETE的区别 - 简书](https://www.jianshu.com/p/ddc5b65e63af)

## 四、==DQL查询数据(最重要)==

### 4.1 DQL

-   数据查询语言
-   关键字 ==**select**==
-   所有查询都要用，简单的复杂的都支持
-   ==**数据库中最核心最重要的语句**==
-   使用频率最高的语句

### 4.2 指定查询字段

-   完整语法：

    ```sql
    SELECT [ALL | DISTINCT]
    {* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,...]]} -- {}为必选
    FROM table_name [as table_alias]
      [left | right | inner join table_name2]  -- 联合查询
      [WHERE ...]  -- 指定结果需满足的条件
      [GROUP BY ...]  -- 指定结果按照哪几个字段来分组
      [HAVING]  -- 过滤分组的记录必须满足的次要条件
      [ORDER BY ...]  -- 指定查询记录按一个或多个条件排序
      [LIMIT {[offset,]row_count | row_countOFFSET offset}];
       -- 指定查询的记录从哪条至哪条
    ```

-   常用语法：

    ```sql
    -- 查询表中所有数据
    select * from `table_name`;
    
    -- 查询指定字段
    select `col_name` from `table_name`;
    
    -- 查询指定字段，并利用as给结果字段和表取别名，别名可以直接是中文，无需加引号，as可以省略无影响
    --      列名          列别名             表名            表别名
    select `col_name` [as] new_col_name from `table_name` [as] new_table_name;
    
    -- 使用函数 concat(a,b) 拼接字符串a,b 可以都是字段也可以一个是一个不是
    select concat(a, b) [as] new_col_name from `table_name`;
    
    -- 查询无重复的结果集使用关键字 distinct 重复的记录只展示一条
    select distinct * from `table_name`;
    ```

-   数据库的列

    ```sql
    select version();                    -- 查询系统版本(函数)
    select 100*10+1 as result;           -- 用来计算(算术表达式)
    select @@auto_increment_increment;   -- 查询自增步长(变量)
    ```

-   ==数据库中的表达式：文本值、列、null、函数、算术表达式、系统变量...==

-   基础语法：`select 表达式 from 数据源`

### 4.3 where条件子句

-   作用：检索数据中**符合**条件的值

-   逻辑运算符：[见此表最后三行](#where table)

-   `where id !=xxx`等价于`where not id=xxx`

-   ==**糢糊查询：比较运算符**==

    |     运算符      |         语法         |                  描述                  |
    | :-------------: | :------------------: | :------------------------------------: |
    |   **IS NULL**   |      a is null       |         如果a是null则结果为真          |
    | **IS NOT NULL** |    a is not null     |        如果a不是null则结果为真         |
    |   **BETWEEN**   |  a between b and c   |     如果a在[b, c]区间内则结果为真      |
    |   **`LIKE`**    |       a like b       |          如果a匹配b则结果为真          |
    |    **`IN`**     | a in (a₀，a₁，a₂...) | 如果a是a₀，a₁，a₂...中的一个则结果为真 |

    -   like通配符：

        -   `%`：匹配0到任意个字符，不匹配null
        -   `_`：匹配一个字符
        -   **`BINARY`** 关键字：使like区分大小写

    -   例子

        ```sql
        -- 匹配a开头的记录
        select * from `table_name` where `col_name` like binary 'a%';
        ```

        

### 4.4 join联表查询

-   MySQL 7种连接示意图

![](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/join.png)

#### 1. cross join笛卡尔乘积

-   要理解各种JOIN首先要理解笛卡尔积。笛卡尔积就是将A表的每一条记录与B表的每一条记录强行拼在一起。所以，如果A表有n条记录，B表有m条记录，笛卡尔积产生的结果就会产生n*m条记录。。有五种产生笛卡尔积的方式如下。

    ```sql
    -- cross join
    select * from `table_1` cross join `table_2`;		-- 常用，推荐
    select * from `table_1`, `table_2`;        			-- 强行将2张表拼在一起
    select * from `table_1` inner join `table_2`;		-- 利用内连接不设on条件来连接
    select * from `table_1` nature join `table_2`;		-- nature 和 natura不是关键字，不知道有什
    select * from `table_1` natura join `table_2`;		-- 么用不推荐使用
    ```

#### 2. inner join内连接

-   内连接INNER JOIN是最常用的连接操作。从数学的角度讲就是求两个表的交集，==从笛卡尔积的角度讲就是从笛卡尔积中挑出ON子句条件成立的记录，(左表右表都有数据的记录)==。有INNER JOIN，WHERE（等值连接），STRAIGHT_JOIN,JOIN(省略INNER)四种写法。

    ```sql
    -- inner join
    select * from `table_1`  t1 								-- 常用，推荐
    inner join `table_2` t2 on t1.id = t2.id [where condition];
    
    select * from `table_1`  t1 								-- inner可省略
    join `table_2` t2 on t1.id = t2.id [where condition]; 
    
    select * from `table_1`  t1 								-- 使用staight_join
    straight_join `table_2` t2 on t1.id = t2.id [where condition];
    
    select * from `table_1` t1, `table_2` t2 where t1.id = t2.id;
    ```

#### 3. left join左连接

-   左连接LEFT JOIN的含义就是求两个表的交集外加左表剩下的数据。依旧从笛卡尔积的角度讲，就是先从笛卡尔积中挑出ON子句条件成立的记录，然后加上左表中剩余的记录（见最后三条）。==即返回左表中的所有记录，即使右表中没有与之匹配的记录。(左表有数据，右表随意的记录)==

    ```sql
    -- left join
    select * from `table_1` t1 left join `table_2` t2 on t1.id = t2.id [where condition]; 
    ```

#### 4. right join右连接

-   同理右连接RIGHT JOIN就是求两个表的交集外加右表剩下的数据。再次从笛卡尔积的角度描述，右连接就是从笛卡尔积中挑出ON子句条件成立的记录，然后加上右表中剩余的记录（见最后一条）。==返回右表中的所有记录，即使左表中没有与之匹配的记录。(右表有数据，左表随意的记录)==

    ```sql
    -- right join
    select * from `table_1` t1 right join `table_2` t2 on t1.id = t2.id [where condition];
    ```

#### 5. outer join外连接

-   外连接就是求两个集合的并集。从笛卡尔积的角度讲就是从笛卡尔积中挑出ON子句条件成立的记录，然后加上左表中剩余的记录，最后加上右表中剩余的记录。另外MySQL不支持OUTER JOIN，但是我们可以对左连接和右连接的结果做UNION操作来实现。

    ```sql
     SELECT * FROM t_blog LEFT JOIN t_type ON t_blog.typeId=t_type.id
        UNION
        SELECT * FROM t_blog RIGHT JOIN t_type ON t_blog.typeId=t_type.id;
    ```

#### 6. using子语句

-   MySQL中连接SQL语句中，ON子句的语法格式为：table1.column_name = table2.column_name。当模式设计对联接表的列采用了相同的命名样式时，就可以使用 USING 语法来简化 ON 语法，格式为：USING(column_name)。
    所以，==USING的功能相当于ON，区别在于USING指定一个属性名用于连接两个表，而ON指定一个条件。另外，SELECT *时，USING会去除USING指定的列(因为是2张表所以有2个，留一个)，而ON不会==。实例如下。

    ```sql
    SELECT * FROM t_blog INNER JOIN t_type ON t_blog.typeId =t_type.id;
        +----+-------+--------+----+------+
        | id | title | typeId | id | name |
        +----+-------+--------+----+------+
        |  1 | aaa   |      1 |  1 | C++  |
        |  2 | bbb   |      2 |  2 | C    |
        |  7 | ggg   |      2 |  2 | C    |
        |  3 | ccc   |      3 |  3 | Java |
        |  6 | fff   |      3 |  3 | Java |
        |  4 | ddd   |      4 |  4 | C#   |
        |  5 | eee   |      4 |  4 | C#   |
        +----+-------+--------+----+------+
        SELECT * FROM t_blog INNER JOIN t_type USING(typeId);
        ERROR 1054 (42S22): Unknown column 'typeId' in 'from clause'
        SELECT * FROM t_blog INNER JOIN t_type USING(id); -- 因为t_blog的typeId与t_type的id不同名，无法用Using，这里用id代替下。
        +----+-------+--------+------------+
        | id | title | typeId | name       |
        +----+-------+--------+------------+
        |  1 | aaa   |      1 | C++        |
        |  2 | bbb   |      2 | C          |
        |  3 | ccc   |      3 | Java       |
        |  4 | ddd   |      4 | C#         |
        |  5 | eee   |      4 | Javascript |
        +----+-------+--------+------------+
    ```


#### 7. natural join自然连接

-   自然连接就是USING子句的简化版，它找出两个表中相同的列作为连接条件进行连接。有**左自然连接**，**右自然连接**和**普通自然连接**之分。在t_blog和t_type示例中，两个表相同的列是id，所以会拿id作为连接条件。

    ```sql
    -- natural join
    select * from `table_1` natural join `table_name`;   -- 普通自然连接
    -- 自然连接的内连接实现不推荐
    select * from `table_1`  t1 								
    inner join `table_2` t2 on t1.id = t2.id [where condition];
    
    select * from `table_1`  t1 								
    inner join `table_2` t2 using (id) [where condition];
    
    -- natural left join
    select * from `table_1` natural left join `table_name`; 
    
    -- natural right join
    select * from `table_1` natural right join `table_name`; 
    ```

#### 8. 自连接

-   自己和自己连接，核心：**==一张表拆为两张一样的表用==**

-   常用语法

    ```sql
    select a.categoryname 父类, b.categoryname 子类 from category a, category b where a.categoryid = b.pid;
    ```

#### 9. 特殊连接

-   图中7种连接除了内连、外连、左连、右连还有3种特殊情况。

    ```sql
    -- special 1
    select * from `table_1`  t1 								
    left join `table_2` t2 on t1.id = t2.id
    where t2.id is null;
    
    -- special 2
    select * from `table_1`  t1 								
    right join `table_2` t2 on t1.id = t2.id
    where t1.id is null;
    
    -- special 3
    select * from `table_1`  t1 								
    left join `table_2` t2 on t1.id = t2.id
    where t2.id is null
    union
    select * from `table_1`  t1 								
    right join `table_2` t2 on t1.id = t2.id
    where t1.id is null;
    ```

### 4.5 limit分页和 order by排序

1.  分页：`limit`

    -   缓解数据库压力，给人的体验更好，瀑布流

    -   常用语法：

        ```sql
        -- limit                         起始值  页面大小
        select * from `table_name` limit start, pageSize;
        -- 第n页 limit (n-1)*pageSize, pageSize
        -- n:当前页
        -- (n-1)*pageSize:起始值
        -- pageSize:页面大小
        -- 数据总数/页面大小=总页数
        -- 或者直接limit条数
        select * from `table_name` limit num; -- 查询num条
        ```

2.  排序：`order by`

    -   **==desc==**：降序
    -   ==**asc**==：升序(默认)

    -   常用语法：

        ```sql
        -- order by 默认降序
        select * from `table_name` order by `col_name` [desc | asc];
        ```

### 4.6 group by分组和 having过滤

#### 1. guoup by：分组查询

-   GROUP BY 语句根据一个或多个列对结果集进行分组。在分组的列上我们可以使用 COUNT, SUM, AVG,等[聚合函数](#5.2 聚合函数)。

-   常用语法

    ```sql
    select `col_name`, xxxx from `table_name` where condition group by `col_name`;
    ```

#### 2. having子语句 过滤

-   having与where区别：
    -   WHERE 关键字无法与聚合函数一起使用。HAVING 子句可以让我们筛选分组后的各组数据。
    -   `HAVING`子句通常与GROUP BY子句一起使用，以根据指定的条件过滤分组。如果省略`GROUP BY`子句，则`HAVING`子句的行为与`WHERE`子句类似。
    -   `HAVING`子句将过滤条件应用于每组分行，而`WHERE`子句将过滤条件应用于每个单独的行。
    -   having是在内存层面进行过滤。

#### 3. 示例

```sql
-- 查询不同课程的平均分,最高分,最低分
-- 前提:根据不同的课程进行分组

select subjectname, avg(studentresult) as 平均分, max(studentresult) as 最高分, min(studentresult) as 最低分
from result as r
         inner join `subject` as s
                    on r.subjectno = s.subjectno
group by r.subjectno
having 平均分 > 80;

/*
where写在group by前面.
要是放在分组后面的筛选
要使用having..
因为having是从前面筛选的字段再筛选，而where是从数据表中的>字段直接进行的筛选的
*/
```



### 4.7 子查询和嵌套查询

-   子查询：在查询语句中的WHERE条件子句中,又嵌套了另一个查询语句,嵌套查询可由多个子查询组成,求解的方式是由里及外;子查询返回的结果一般都是集合,故而建议使用IN关键字;

    ```sql
    select * from `table_name` where `col_name` in (select `col_name` from `tabel_2`);
    -- 等价于
    select * from `table_name` inner join `table_2` using(`col_name`);
    ```
### 4.8 其他

-   参考：
    1.  [MySQL的JOIN（一）：用法 - 付大石 - 博客园](https://www.cnblogs.com/fudashi/p/7491039.html)
    2.  [mysql学习之完整的select语句 - 随风行云 - 博客园](https://www.cnblogs.com/progor/p/8786133.html#:~:text=完整语法：select 去重选项 字段列表 [as 字段别名] from 数据源 [where子句],子句] [having子句] [order by 子句] [limit子句]%3B 注意：去重针对的是查询出来的记录，而不是存储在表中的记录。 如果说仅仅查询的是某些字段，那么去重针对的是这些字段。)
    3.  [SQL概述 - MaxCompute - 阿里云](https://help.aliyun.com/document_detail/27860.html?spm=a2c4g.11186623.6.718.64ec370flAglce)

## 五、MySQL函数

### 5.1 常用函数

-   逻辑执行函数

    ```sql
    select ifnull(condition, exp) -- 如果condition非空则输出condition值否则输出exp
    select if(condition, t_exp, f_exp) -- 类似三元表达式
    select case -- s
    ```

-   数值函数

    ```sql
     select abs(-8);  /*绝对值*/
     select ceiling(9.4); /*向上取整*/
     select floor(9.4);   /*向下取整*/
     select rand();  /*随机数,返回一个0-1之间的随机数*/
     select sign(0); /*符号函数: 负数返回-1,正数返回1,0返回0*/
    ```

-   字符串函数

    ```sql
    select char_length('狂神说坚持就能成功'); /*返回字符串包含的字符数*/
    select concat('我','爱','程序');  /*合并字符串,参数可以有多个*/
    select insert('我爱编程helloworld',1,2,'超级热爱');  /*替换字符串,从某个位置开始替换某个长度*/
    select lower('kuangshen'); /*小写*/
    select upper('kuangshen'); /*大写*/
    select left('hello,world',5);   /*从左边截取*/
    select right('hello,world',5);  /*从右边截取*/
    select replace('狂神说坚持就能成功','坚持','努力');  /*替换字符串*/
    select substr('狂神说坚持就能成功',4,6); /*截取字符串,开始和长度*/
    select reverse('狂神说坚持就能成功'); /*反转*/
    ```

-   **==日期和时间函数==**

    ```sql
    select current_date();   /*获取当前日期*/
    select curdate();   /*获取当前日期*/
    select now();   /*获取当前日期和时间*/
    select localtime();   /*获取当前日期和时间*/
    select sysdate();   /*获取当前日期和时间*/
    
    -- 获取年月日,时分秒
    select year(now());
    select month(now());
    select day(now());
    select hour(now());
    select minute(now());
    select second(now());
    
    -- 计算
    -- 在mysql当中怎么计算两个日期的“年差”，差了多少年？
    TimeStampDiff(间隔类型, 前一个日期, 后一个日期)
    	
    timestampdiff(YEAR, hiredate, now())
    
    -- 间隔类型：
    -- SECOND   秒，
    -- MINUTE   分钟，
    -- HOUR   小时，
    -- DAY   天，
    -- WEEK   星期
    -- MONTH   月，
    -- QUARTER   季度，
    -- YEAR   年
    ```

-   系统信息函数

    ```sql
    select system_user();
    select version(); /*版本*/
    select user(); /*用户*/
    ```

### 5.2 **==聚合函数==**

| **函数名称** |                           **描述**                           |
| :----------: | :----------------------------------------------------------: |
|   COUNT()    | 返回满足Select条件的记录总和数，如 select count(*) 【不建议使用 *，效率低】 |
|    SUM()     |        返回数字字段或表达式列作统计，返回一列的总和。        |
|    AVG()     |        通常为数值字段或表达列作统计，返回一列的平均值        |
|    MAX()     |   可以为数值字段，字符字段或表达式列作统计，返回最大的值。   |
|    MIN()     |   可以为数值字段，字符字段或表达式列作统计，返回最小的值。   |

-   示例

    ```sql
    -- 聚合函数
    /*count:非空的*/
    select count(studentname) from student;
    select count(*) from student;
    select count(1) from student;  /*推荐*/
    
    -- count 条件统计 统计 大于200的num的个数
    select count(num > 200 or null) from a;
    select count(if(num > 200, 1, null)) from a
    select count(case when num > 200 then 1 end) from a
    
    -- 从含义上讲，count(1) 与 count(*) 都表示对全部数据行的查询。
    -- count(字段) 会统计该字段在表中出现的次数，忽略字段为null 的情况。即不统计字段为null 的记录。
    -- count(*) 包括了所有的列，相当于行数，在统计结果的时候，包含字段为null 的记录；
    -- count(1) 用1代表代码行，在统计结果的时候，包含字段为null 的记录 。
    /*
    很多人认为count(1)执行的效率会比count(*)高，原因是count(*)会存在全表扫描，而count(1)可以针对一个字段进行查询。其实不然，count(1)和count(*)都会对全表进行扫描，统计所有记录的条数，包括那些为null的记录，因此，它们的效率可以说是相差无几。而count(字段)则与前两者不同，它会统计该字段不为null的记录条数。
    
    下面它们之间的一些对比：
    
    1）在表没有主键时，count(1)比count(*)快
    2）有主键时，主键作为计算条件，count(主键)效率最高；
    3）若表格只有一个字段，则count(*)效率较高。
    */
    
    select sum(studentresult) as 总和 from result;
    select avg(studentresult) as 平均分 from result;
    select max(studentresult) as 最高分 from result;
    select min(studentresult) as 最低分 from result;
    ```


### 5.3 MD5加密

#### 1. MD5简介

-   MD5即Message-Digest Algorithm 5（信息-摘要算法5），**用于确保信息传输完整一致。是计算机广泛使用的杂凑算法之一（又译摘要算法、哈希算法），主流编程语言普遍已有MD5实现**。将数据（如汉字）运算为另一固定长度值，是杂凑算法的基础原理，MD5的前身有MD2、MD3和MD4。
-   主要增强算法的复杂度和不可逆性
-   MD5不可逆，具体值相同的MD5值也相同
-   MD5破解网站原理：有一个字典，包含{MD5原来的值：MD5加密后的值}

#### 2. 示例

```sql
-- 新建一个表 testmd5
create table `testmd5`
(
    `id`   int(4)      not null,
    `name` varchar(20) not null,
    `pwd`  varchar(50) not null,
    primary key (`id`)
) engine = innodb
  default charset = utf8;

-- 插入一些数据
insert into testmd5
values (1, 'kuangshen', '123456'),
       (2, 'qinjiang', '456789');

-- 如果我们要对pwd这一列数据进行加密，语法是：
update testmd5
set pwd = md5(pwd);

-- 如果单独对某个用户(如kuangshen)的密码加密：
insert into testmd5
values (3, 'kuangshen2', '123456')
update testmd5
set pwd = md5(pwd)
where name = 'kuangshen2';

-- 插入新的数据自动加密
insert into testmd5
values (4, 'kuangshen3', md5('123456'));

-- 查询登录用户信息（md5对比使用，查看用户输入加密后的密码进行比对）
select *
from testmd5
where `name` = 'kuangshen'
  and pwd = md5('123456');
```

### 5.4 其他

-   参考：
    1.  [MySQL官方文档](https://dev.mysql.com/doc/refman/5.7/en/built-in-function-reference.html)
    2.  [MySQL函数大全，MySQL常用函数汇总](http://c.biancheng.net/mysql/function/)

-   其他函数

    ```sql
    -- ================ 内置函数 ================
    -- 数值函数
    abs(x)            -- 绝对值 abs(-10.9) = 10
    format(x, d)    -- 格式化千分位数值 format(1234567.456, 2) = 1,234,567.46
    ceil(x)            -- 向上取整 ceil(10.1) = 11
    floor(x)        -- 向下取整 floor (10.1) = 10
    round(x)        -- 四舍五入去整
    mod(m, n)        -- m%n m mod n 求余 10%3=1
    pi()            -- 获得圆周率
    pow(m, n)        -- m^n
    sqrt(x)            -- 算术平方根
    rand()            -- 随机数
    truncate(x, d)    -- 截取d位小数
    
    -- 时间日期函数
    now(), current_timestamp();     -- 当前日期时间
    current_date();                    -- 当前日期
    current_time();                    -- 当前时间
    date('yyyy-mm-dd hh:ii:ss');    -- 获取日期部分
    time('yyyy-mm-dd hh:ii:ss');    -- 获取时间部分
    date_format('yyyy-mm-dd hh:ii:ss', '%d %y %a %d %m %b %j');    -- 格式化时间
    unix_timestamp();                -- 获得unix时间戳
    from_unixtime();                -- 从时间戳获得时间
    
    -- 字符串函数
    length(string)            -- string长度，字节
    char_length(string)        -- string的字符个数
    substring(str, position [,length])        -- 从str的position开始,取length个字符
    replace(str ,search_str ,replace_str)    -- 在str中用replace_str替换search_str
    instr(string ,substring)    -- 返回substring首次在string中出现的位置
    concat(string [,...])    -- 连接字串
    charset(str)            -- 返回字串字符集
    lcase(string)            -- 转换成小写
    left(string, length)    -- 从string2中的左边起取length个字符
    load_file(file_name)    -- 从文件读取内容
    locate(substring, string [,start_position])    -- 同instr,但可指定开始位置
    lpad(string, length, pad)    -- 重复用pad加在string开头,直到字串长度为length
    ltrim(string)            -- 去除前端空格
    repeat(string, count)    -- 重复count次
    rpad(string, length, pad)    --在str后用pad补充,直到长度为length
    rtrim(string)            -- 去除后端空格
    strcmp(string1 ,string2)    -- 逐字符比较两字串大小
    
    -- 聚合函数
    count()
    sum();
    max();
    min();
    avg();
    group_concat(); --将值串连
    
    -- 其他常用函数
    md5(); -- md5加密
    default(); -- 获取字段默认值
    ```

## 六、事务

### 6.1 事务简介

-   什么是：**将一组sql放在一个批次中去执行，==要么都成功，要么都失败==(只要有一句sql报错就算失败)**

-   事务原则：ACID原则

    1.  **原子性(Atomicity)**：原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生，不可能停滞在中间某个环节。事务在执行过程中发生错误，会被回滚（ROLLBACK）到事务开始前的状态，就像这个事务从来没有执行过一样。
    2.  **一致性(Consistency)**：一个事务可以封装状态改变（除非它是一个只读的）。事务必须始终保持系统处于一致的状态，不管在任何给定的时间并发事务有多少。也就是说：如果事务是并发多个，系统也必须如同串行事务一样操作。其主要特征是保护性和不变性(Preserving an Invariant)，以转账案例为例，假设有五个账户，每个账户余额是100元，那么五个账户总额是500元，如果在这个5个账户之间同时发生多个转账，无论并发多少个，比如在A与B账户之间转账5元，在C与D账户之间转账10元，在B与E之间转账15元，五个账户总额也应该还是500元，这就是保护性和不变性。
    3.  **隔离性(Isolated)**：隔离状态执行事务，使它们好像是系统在给定时间内执行的唯一操作。如果有两个事务，运行在相同的时间内，执行相同的功能，事务的隔离性将确保每一事务在系统中认为只有该事务在使用系统。这种属性有时称为串行化，为了防止事务操作间的混淆，必须串行化或序列化请求，使得在同一时间仅有一个请求用于同一数据。
    4.  **持久性(Durable)**：持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来即使数据库发生故障也不应该对其有任何影响。

-   隔离级别

    -   **脏读**：指一个事务读取了另外一个事务未提交的数据。
    -   **不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）
    -   **虚读(幻读)**：是指在一个事务内读取到了别的事务插入的数据，导致前后读取数量总量不一致。
        (一般是行影响)

-   隔离设置

    -   mysql

        ```sql
        set transaction isolation level xxx; -- 设置事务隔离级别
        select @@tx_isolation; -- 查询当前事务隔离级别
        ```

        |     **设置**     |                      **描述**                      |
        | :--------------: | :------------------------------------------------: |
        |   Serializable   | 可避免脏读、不可重复读、虚读情况的发生。（串行化） |
        | Repeatable read  |   可避免脏读、不可重复读情况的发生。（可重复读）   |
        |  Read committed  |          可避免脏读情况发生。（读已提交）          |
        | Read uncommitted |      最低级别，以上情况均无法保证。(读未提交)      |

    -   java

        -   适当的 Connection 方法，比如 setAutoCommit 或 setTransactionIsolation

        |           **设置**           |                           **描述**                           |
        | :--------------------------: | :----------------------------------------------------------: |
        |   TRANSACTION_SERIALIZABLE   |         指示不可以发生脏读、不可重复读和虚读的常量。         |
        | TRANSACTION_REPEATABLE_READ  |     指示不可以发生脏读和不可重复读的常量；虚读可以发生。     |
        | TRANSACTION_READ_UNCOMMITTED | 指示可以发生脏读 (dirty read)、不可重复读和虚读 (phantom read) 的常量。 |
        |  TRANSACTION_READ_COMMITTED  |     指示不可以发生脏读的常量；不可重复读和虚读可以发生。     |

### 6.2 执行事务

-   流程、语法：

```sql
-- mysql 是默认开启事务自动提交的
set autocommit = 0; -- 关闭
set autocommit = 1; -- 开启(默认开启)
select @@autocommit; -- 查询当前状态

-- 手动处理事务
set autocommit = 0; -- 关闭自动提交

-- 开启事务
start transaction;  -- 标记一个事务的开始，从这之后的sql都在同一个事务内

-- ...
-- ...
-- ...

-- 提交，持久化成功！
commit;

-- 回滚，回到原来的样子
rollback;

-- 事务结束
set autocommit = 1;  -- 开启自动提交

savepoint 保存点名;   -- 设置一个事务保存点
rollback to 保存点名;  -- 回滚到保存点
release savepoint 保存点名; -- 撤销保存点
```

-   示例：

```sql
/*
示例

A在线买一款价格为500元商品,网上银行转账.
A的银行卡余额为2000,然后给商家B支付500.
商家B一开始的银行卡余额为10000

创建数据库shop和创建表account并插入2条数据
*/
create database if not exists `shop` character set utf8 collate utf8_general_mysql500_ci;
use shop;
CREATE TABLE IF NOT EXISTS `account`(
    id int(3) auto_increment,
    name varchar(30) not null,
    money decimal(9, 2) not null,
    primary key (id)
)ENGINE=INNODB DEFAULT CHARSET=utf8 COMMENT='帐号表';

insert into account(name, money)
values ('a', 2000.00),('b', 10000.00);


-- 模拟事务: a给b转账500
set autocommit = 0;
start transaction;

update account set money = money - 500 where name = 'a';
update account set money = money + 500 where name = 'b';

commit;
rollback;

set autocommit = 0;
-- 在Java中执行事务
method(){
	...
	try(){
		业务代码;
		commit();
	}catch(){
		rollback()
	}
	...
}
```



### 6.3 其他

-   参考：
    1.  [事务ACID理解_dengjili的专栏-CSDN博客](https://blog.csdn.net/dengjili/article/details/82468576)

## 七、索引

>MySQL官方对索引的定义为：索引（Index）是帮助MySQL高效获取数据的数据结构。提取句子主干，就可以得到索引的本质：索引是数据结构。

### 7.1 索引分类

-   **[主键索引(Primary Key)](#7. primary key)**

    -   唯一标识，主键不能为空，不能重复，一般情况(复合/联合主键除外)，一张表有且只有一个主键。

-   **[唯一索引(Unique Key)](#6. unique)**

    -   避免列中重复元素出现，可以有多个使用unique的列。

-   **常规索引(Key/Index)**

    -   默认的，使用index/key关键字创建。
    -   快速定位数据
    -   不宜添加太多常规索引,影响数据的插入,删除和修改操作

-   **全文索引(FullText)**

    -   特定的数据库引擎才支持，如MYISAM，1.2及以上的INODB。
    -   快速定位数据。
    -   只能用于CHAR , VARCHAR , TEXT数据列类型
    -   适合大型数据集

    ```sql
    /*使用全文索引*/
    -- 全文搜索通过 MATCH() 函数完成。
    -- 搜索字符串作为 against() 的参数被给定。搜索以忽略字母大小写的方式执行。对于表中的每个记录行，MATCH() 返回一个相关性值。即，在搜索字符串与记录行在 MATCH() 列表中指定的列的文本之间的相似性尺度。
    EXPLAIN SELECT * FROM `table_name` WHERE MATCH(`col_name`) AGAINST('xxx');
    
    /*
    开始之前，先说一下全文索引的版本、存储引擎、数据类型的支持情况
    
    MySQL 5.6 以前的版本，只有 MyISAM 存储引擎支持全文索引；
    MySQL 5.6 及以后的版本，MyISAM 和 InnoDB 存储引擎均支持全文索引;
    只有字段的数据类型为 char、varchar、text 及其系列才可以建全文索引。
    测试或使用全文索引时，要先看一下自己的 MySQL 版本、存储引擎和数据类型是否支持全文索引。
    */
    ```

    

### 7.2 索引的使用

-   基础语法

    ```sql
    -- 索引的使用
    -- 1.建表的时候添加
    -- 2.建表后添加
    
    -- 显示表的索引信息
    select index from `table_name`;
    
    -- 建表后添加索引
    -- 法一      表名             索引类型                索引名        添加的列
    alter table `table_name` add index_type [key|index] [index_name](`col_name`);
    -- 法二  索引类型    索引名           表名         添加的列
    create index_type [index_name] on `table_name`(`col_name`); -- 不能创建主键
    
    -- 删除索引
    drop index index_name on `table_name`; -- 法一
    alter table `table_name` drop index index_name; -- 法二
    
    -- explain 分析sql执行具体情况
    explain select * from `table_name`...
    ```
    
-   示例

    ```sql
    CREATE TABLE `app_user`
    (
        `id`          bigint(20) unsigned NOT NULL AUTO_INCREMENT,
        `name`        varchar(50)              DEFAULT '' COMMENT '用户昵称',
        `email`       varchar(50)         NOT NULL COMMENT '用户邮箱',
        `phone`       varchar(20)              DEFAULT '' COMMENT '手机号',
        `gender`      tinyint(4) unsigned      DEFAULT '0' COMMENT '性别（0:男；1：女）',
        `password`    varchar(100)        NOT NULL COMMENT '密码',
        `age`         tinyint(4)               DEFAULT '0' COMMENT '年龄',
        `create_time` datetime                 DEFAULT CURRENT_TIMESTAMP,    -- 创建时间
        `update_time` timestamp           NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
        PRIMARY KEY (`id`)
    ) ENGINE = InnoDB
      DEFAULT CHARSET = utf8mb4 COMMENT ='app用户表';
    
    -- 插入100万条数据
    delimiter $$  -- 自定义函数
    
    create function mock_data()
        returns int
    begin
        declare num int default 1000000;
        declare i int default 0;
    
        while i < num
            do
                insert into app_user (name, email, phone, gender, password, age)
                values (concat('user', i), '12345678@qq.com',
                        concat('18', floor(rand() * ((999999999 - 100000000) + 100000000))),
                        floor(rand() * 2), uuid(), floor(rand() * 100));
                set i = i + 1;
            end while;
        return i;
    end;
    select mock_data();
    
    select * from app_user where name='user19999';
    explain select  * from app_user where name='user19999';
    -- 普通索引名 id_表名_字段名
    create index id_app_user_name on app_user(name);
    ```

### 7.3 索引原则

-   索引不是越多越好。
-   不要对经常变动的变量加索引
-   小数据量的表不需要加索引
-   索引一般加在常用查询的字段上
-   索引的数据结构类型：
    -   hash：
    -   btree：innodb的默认索引类型

### 7.4 其他

-   参考：

    1.  **[==CodingLabs - MySQL索引背后的数据结构及算法原理==](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)**
    2.  [【MySQL优化】——看懂explain_漫漫长途，终有回转；余味苦涩，终有回甘-CSDN博客](https://blog.csdn.net/jiadajing267/article/details/81269067)
    3.  [MySQL索引知识总结_CrankZ的博客-CSDN博客](https://blog.csdn.net/CrankZ/article/details/80468760)


## 八、权限管理和备份

### 8.1 用户管理

-   用户表：mysql.user

-   语法：用户名和ip地址可以加单引号(')

    ```sql
    -- 创建用户   用户名     ip地址                 密码
    create user user_name@host identified by 'pwd444WWW!@#';-- 不加@host默认是@%，%表示所有ip皆可访问
    
    -- 修改密码
    set password = password ('new_pwd'); -- 修改当前用户
    set password for user_name@host = password ('new_pwd'); -- 修改指定用户
    
    -- 重命名用户名
    rename user user_name@host to new_name@new_host;
    
    -- 用户授权
    grant all privileges on *.* to user_name@host; -- 授与所有权限，除了给别人授权，其他都能干
    --    权限名       库名.表名  用户
    grant select,... on *.* to user_name@host; -- *指代所有库(表)
    
    -- 查看权限
    show grants for root;
    
    -- root用户的权限
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
    
    -- 撤销权限
    revoke all privileges on *.* from user_name;
    
    -- 删除用户
    drop user user_name@host;
    
    -- 进行权限操作后需要进行刷新权限
    flush privileges;
    ```

-   规则： 权限控制主要是出于安全因素，因此需要遵循一下几个经验原则：

      1、只授予能满足需要的最小权限，防止用户干坏事。比如用户只是需要查询，那就只给select权限就可以了，不要给用户赋予update、insert或者delete权限。

      2、创建用户的时候限制用户的登录主机，一般是限制成指定IP或者内网IP段。

      3、初始化数据库的时候删除没有密码的用户。安装完数据库的时候会自动创建一些用户，这些用户默认没有密码。

      4、为每个用户设置满足密码复杂度的密码。

      5、定期清理不需要的用户。回收权限或者删除用户。

### 8.2 数据库备份

-   为什么要备份：

    -   保证数据不丢失
    -   可以数据转移

-   备份方式：

    1.  拷贝物理文件：data文件
    2.  在可视化工具中手动导出
    3.  **使用命令行导出msqldump**

-   语法

    ``` bash
    msqldump -h'host' -uroot -p dbname table_name > path
    #mysqldump -h% -uroot -p'Wang666hhby!@#' school student >D:/a.sql;
    mysqldump -u root -p --all-databses > all-data-$(date +%F).sql ###备份所有数据库
    mysqldump -u root -p -databases auth mysql > auth-mysql.sql ###备份auth和mysql库
    mysqldump -u root -p auth > auth-$(data +%F).sql ###备份auth数据库
    mysqldump -u root -p mysql user > mysql-user-$(date +%F).sql ###备份mysql的user表
    mysqldump -u root -p -d mysql user > /tmp/desc-mysql-user.sql ###备份mysql库user表的结构
    mysqldump -uroot -pabc123 --all-databases > /backup/all.sql
    
    #加载sql文件
    #登录mysql
    mysql -h'host' -uroot -p
    #切换数据库
    use dbname;
    #加载sql文件
    source /xxx/xxx.sql;
    ```

### 其他

-   参考

    1.  [MySQL之权限管理 - I’m Me! - 博客园](https://www.cnblogs.com/Richardzhu/p/3318595.html)
    2.  [学习MySQL备份一篇就够了！！！（完全备份、增量备份、备份恢复）_下一个艺术家-CSDN博客_mysql备份数据库](https://blog.csdn.net/qyf158236/article/details/109220563)

-   MySQL具体权限：

    | CREATE                  | 数据库、表或索引       | 创建数据库、表或索引权限                                     |
    | ----------------------- | ---------------------- | ------------------------------------------------------------ |
    | DROP                    | 数据库或表             | 删除数据库或表权限                                           |
    | GRANT OPTION            | 数据库、表或保存的程序 | 赋予权限选项                                                 |
    | REFERENCES              | 数据库或表             |                                                              |
    | ALTER                   | 表                     | 更改表，比如添加字段、索引等                                 |
    | DELETE                  | 表                     | 删除数据权限                                                 |
    | INDEX                   | 表                     | 索引权限                                                     |
    | INSERT                  | 表                     | 插入权限                                                     |
    | SELECT                  | 表                     | 查询权限                                                     |
    | UPDATE                  | 表                     | 更新权限                                                     |
    | CREATE VIEW             | 视图                   | 创建视图权限                                                 |
    | SHOW VIEW               | 视图                   | 查看视图权限                                                 |
    | ALTER ROUTINE           | 存储过程               | 更改存储过程权限                                             |
    | CREATE ROUTINE          | 存储过程               | 创建存储过程权限                                             |
    | EXECUTE                 | 存储过程               | 执行存储过程权限                                             |
    | FILE                    | 服务器主机上的文件访问 | 文件访问权限                                                 |
    | CREATE TEMPORARY TABLES | 服务器管理             | 创建临时表权限                                               |
    | LOCK TABLES             | 服务器管理             | 锁表权限                                                     |
    | CREATE USER             | 服务器管理             | 创建用户权限                                                 |
    | PROCESS                 | 服务器管理             | 查看进程权限                                                 |
    | RELOAD                  | 服务器管理             | 执行flush-hosts, flush-logs, flush-privileges, flush-status, flush-tables, flush-threads, refresh, reload等命令的权限 |
    | REPLICATION CLIENT      | 服务器管理             | 复制权限                                                     |
    | REPLICATION SLAVE       | 服务器管理             | 复制权限                                                     |
    | SHOW DATABASES          | 服务器管理             | 查看数据库权限                                               |
    | SHUTDOWN                | 服务器管理             | 关闭数据库权限                                               |
    | SUPER                   | 服务器管理             | 执行kill线程权限                                             |

## 九、**==规范数据库设计(三大范式)==**

>   **==当数据库比较复杂时，我们就需要设计数据库==**

### 9.1 对比

-   糟糕的数据库设计：
    -   数据冗余，浪费空间
    -   数据库插入和删除都会麻烦、异常(==屏蔽使用物理外键==)
    -   程序性能差
-   良好的数据库设计：
    -   节省内存空间
    -   保证数据库的完整性
    -   方便开发系统

### 9.2 软件开发中，关于数据库的设计

#### 1. 要点

-   分析需求：分析业务和需要处理的数据库需求
-   概要设计：设计关系图E-R图

#### 2. 步骤(以个人博客为例)

1.  收集信息，分析需求

    -   用户表(用户登录注销、用户个人信息、写博客、创建分类)
    -   分类表(文章分类、作者)
    -   文章表(文章信息)
    -   评论表(评论信息)
    -   友链表(友情链接信息)
    -   说说表(说说，心情)
    -   自定义表(系统信息、某个关键字，或者一些主字段)key：value

2.  标识实体(把需求落实)

3.  标识实体之间的关系

    -   写博客：user --> blog

    -   创建分类：user --> category

    -   关注：user --> user

    -   友链：links

    -   评论：user --> user --> blog

        ......

    ```sql
    CREATE TABLE IF NOT EXISTS `user`
    (
        id         int(10) auto_increment comment '用户唯一id',
        username   varchar(60)     not null COMMENT '用户名',
        `password` varchar(60)     not null COMMENT '密码',
        sex        varchar(2)      not null default '未知' COMMENT '性别',
        age        int(3) unsigned not null COMMENT '年龄',
        sign       varchar(200)    not null COMMENT '签名',
        primary key (id)
    ) ENGINE = INNODB
      DEFAULT CHARSET = utf8 COMMENT ='用户表';
    create table if not exists `category`
    (
        id             int(10) auto_increment COMMENT '分类唯一id',
        category       varchar(30) not null COMMENT '分类标题',
        create_user_id int(10)     not null COMMENT '创建者id',
        primary key (id),
        constraint uk_category unique key (category)
    ) engine = INNODB
      default charset = utf8 comment ='分类表';
    create table if not exists `blog`
    (
        id          int(10) auto_increment comment '文章唯一id',
        title       varchar(200)     not null COMMENT '文章标题',
        author_id   int(10)          not null COMMENT '作者id',
        content     text             not null COMMENT '文章内容',
        `like`      int(10) unsigned not null default 0 COMMENT '点赞数',
        create_time datetime         not null default current_timestamp COMMENT '创建时间',
        update_time timestamp        null     default current_timestamp on update current_timestamp COMMENT '',
        primary key (id)
    ) engine = INNODB
      default charset = utf8 comment ='文章表';
    create table if not exists `comment`
    (
        id               int(10) auto_increment comment '主键id',
        `blog_id`        int(10)       not null COMMENT '文章id',
        `user_id`        int(10)       not null COMMENT '评论人id',
        `content`        varchar(2000) not null COMMENT '评论内容',
        `user_id_parent` int(10)       not null default 0 COMMENT '回复的人的id',
        create_time      datetime      not null default current_timestamp comment '创建时间',
        update_time      timestamp     null     default current_timestamp on update current_timestamp comment '更新时间',
        primary key (id)
    ) engine = INNODB
      default charset = utf8 comment ='文章表';
    create table if not exists `links`
    (
        id          int(10) auto_increment comment '主键id',
        `link`      varchar(50)      not null COMMENT '网站名称',
        `href`      varchar(2000)    not null COMMENT '网站链接',
        `sort`      int(10) unsigned not null COMMENT '排序',
        create_time datetime         not null default current_timestamp comment '创建时间',
        update_time timestamp        null     default current_timestamp on update current_timestamp comment '更新时间',
        primary key (id)
    ) engine = INNODB
      default charset = utf8 comment ='友链表';
    
    alter table user
        add column `open_id` varchar(1000) not null default '无' comment '微信id' after sign;
    alter table user
        add column `avatar` varchar(1000) not null default '无' comment '头像链接地址' after open_id;
    create table if not exists `user_follow`
    (
        `id`          int(10) auto_increment comment '主键id',
        `user_id`     int(10)   not null COMMENT '被关注人的id',
        `follow`      int(10)   not null COMMENT '关注人的id',
        `create_time` datetime  not null default current_timestamp comment '创建时间',
        `update_time` timestamp null     default current_timestamp on update current_timestamp comment '更新时间',
        primary key (`id`)
    ) engine = INNODB
      default charset = utf8 comment ='粉丝中间表';
    ```

### 9.2 三大范式

#### 1. 为什么需要数据规范化？

没有数据规范会导致：

-   信息重复
-   更新异常
-   插入异常
    -   无法正常显示数据
-   删除异常
    -   丢失有效信息

#### 2. **==三大范式理解==**

>   目前[关系数据库](https://baike.baidu.com/item/关系数据库/1237340)有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、[第四范式](https://baike.baidu.com/item/第四范式/3193985)(4NF）和[第五范式](https://baike.baidu.com/item/第五范式/5025271)（5NF，又称完美范式）。而通常我们用的最多的就是第一范式（1NF）、第二范式（2NF）、第三范式（3NF），也就是本文要讲的“三大范式”。

1.  **第一范式(1FN)**：**要求数据库表的每一列都是不可分割的原子数据项。**
2.  **第二范式(2FN)**：**在1NF的基础上，非码属性必须完全依赖于候选码（在1NF基础上消除非主属性对主码的部分函数依赖）第二范式需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）。**
3.  **第三范式(3FN)**：**在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。**

#### 3. 规范性和性能的问题

>   阿里巴巴开发手册规定：关联查询的表不得关联超过三张(多表查询性能太差)

-   考虑商业化的需求和目标，(成本，用户体验)数据库的性能更重要。
-   在规范性能问题时，需要适当考虑一下规范性。
-   有时会故意给一些表增加冗余字段，使其从多表查询变为单表查询。
-   有时会故意增加一些计算列，使之从大数据量的查询降低为小数据量的查询如索引。

### 9.3 其他

-   参考：
    1.  [关系型数据库设计：三大范式的通俗理解 - 景寓6号 - 博客园](https://www.cnblogs.com/wsg25/p/9615100.html)
    2.  [【数据库】数据库入门（七）: 函数依赖（Functional Dependencies） - 简书](https://www.jianshu.com/p/f525c2e91fb4)
    3.  [关系型数据库的设计理论（异常、函数依赖、范式）_u013617791的专栏-CSDN博客](https://blog.csdn.net/u013617791/article/details/83041560)

## 十、**==JDBC(重点)==**

### 10.1 数据库驱动

-   定义：数据库驱动是不同数据库开发商（比如oracle mysql等）为了某一种开发语言环境（比如java）能够实现数据库调用而开发的一个程序，他的作用相当于一个翻译人员，将Java中对数据库的调用语言翻译成数据库自己的数据库语言，当然这个翻译（数据库驱动）是由各个开发商针对统一的接口自定义开发的。

### 10.2 JDBC简介

>   JDBC 指 Java 数据库连接，是一种标准Java应用编程接口（ JAVA API），用来连接 Java 编程语言和广泛的数据库。JDBC API 库包含下面提到的每个任务，都是与数据库相关的常用用法。

-   java开发使用包

    -   java.sql

    -   javax.sql

    -   驱动jar包：mysql-connector-java-5.xx.xx.jar

    -   maven依赖：

        ```xml
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.11</version>
        </dependency>
        ```

        

<img src="./../markdownRes/mysql/jdbc.jpg" style="zoom:150%;" />

### 10.3 第一个JDBC程序

```java
package com.wlq.lesson1;

import java.sql.*;

/**
 * program: jdbc-study
 * <br>description: jdbc demo1
 *
 * @author by 王林清 on 2021/7/30
 * @version Java1.9 IntelliJ IDEA
 */
public class JdbcFirstDemo {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        // 1.加载驱动  固定写法加载驱动
        Class.forName("com.mysql.cj.jdbc.Driver");

        // 2.用户信息和url
        String url = "jdbc:mysql://localhost:3306/jdbc_study?userUnicode=true&characterEncoding=utf8&useSSL=false";
        String userName = "root";
        String password = "1248";

        // 3.连接成功，数据库对象
        Connection connection = DriverManager.getConnection(url, userName, password);

        // 4.执行sql对象
        Statement statement = connection.createStatement();

        // 5.执行sql对象去执行sql可能存在的结果，查看返回结果
        String sql = "select * from users";

        // 返回的结果集，其中封装了我们所有查询到的数据
        ResultSet resultSet = statement.executeQuery(sql);

        while (resultSet.next()) {
            System.out.println("id=" + resultSet.getObject("id"));
            System.out.println("name=" + resultSet.getObject("name"));
            System.out.println("password=" + resultSet.getObject("password"));
            System.out.println("email=" + resultSet.getObject("email"));
            System.out.println("birthday=" + resultSet.getObject("birthday"));
            System.out.println("=======================================================");
        }
        // 6.释放连接
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```

-   步骤连接

1.  加载驱动
    -   jdbcurl参数：userUnicode=true&characterEncoding=utf8&useSSL=false
2.  连接数据库DriverManager
3.  获得执行sql的对象Statement
4.  获得返回结果集ResultSet
5.  释放连接

### 10.4 Statement类

>   **==JDBC中的Statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查的sql语句即可==**
>
>   Statement对象的executeUpdate()方法用于向数据库发送增删改的sql语句，执行完成后返回一个整数即增删改语句导致了几行数据变化。
>
>   Statement对象的executeQuery()方法用于向数据库发送查询语句，执行完成后返回代表查询结果的ResultSet对象。

#### 1. CURD操作

-   create

    ```java
    Statement statement = connection.createStatement();
        String sql = "insert into users(id, name, password, email, birthday) values (5, 'hhby', '1248', " +
            "'2360039845@qq.com', '2001-10-10')";
        int num = statement.executeUpdate(sql);
        if (num > 0) {
            System.out.println("插入成功");
        }
    ```

-   delete

    ```sql
    Statement statement = connection.createStatement();
        String sql = "delete from users where id = 1";
        int num = statement.executeUpdate(sql);
        if (num > 0) {
            System.out.println("删除成功");
        }
    ```

-   udate

    ```java
    Statement statement = connection.createStatement();
        String sql = "update users set password='3306' where id = 1";
        int num = statement.executeUpdate(sql);
        if (num > 0) {
            System.out.println("更新成功");
        }
    ```

-   read

    ```java
    Statement statement = connection.createStatement();
        String sql = "select * from users";
        ResultSet rs = statement.executeQuery(sql);
        while(rs.next()){
            ...
        }
    ```

#### 2. 代码实现

-   抽取工具类

    ```java
    package com.wlq.lesson2.util;
    
    import java.io.IOException;
    import java.io.InputStream;
    import java.sql.*;
    import java.util.Properties;
    
    /**
     * program: jdbc-study
     * <br>description: JDBC mysql 工具类
     *
     * @author by 王林清 on 2021/7/30
     * @version Java1.9 IntelliJ IDEA
     */
    public class JdbcUtil {
        private static String driver = null;
        private static String url = null;
        private static String username = null;
        private static String password = null;
    
        static {
            try {
                InputStream inputStream = JdbcUtil.class.getClassLoader().getResourceAsStream("db.properties");
                Properties properties = new Properties();
                properties.load(inputStream);
    
                driver = properties.getProperty("driver");
                url = properties.getProperty("url");
                username = properties.getProperty("username");
                password = properties.getProperty("password");
                // 1.驱动只用加载一次
                Class.forName(driver);
            } catch (IOException | ClassNotFoundException e) {
                e.printStackTrace();
            }
    
        }
    
        // 获取连接
        public static Connection getConnection() throws SQLException {
            return DriverManager.getConnection(url, username, password);
        }
    
        // 释放连接资源
        public static void release(Connection conn, Statement st, ResultSet rs) {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (st != null) {
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```

-   增删改

    ```java
    package com.wlq.lesson2.util;
    
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    /**
     * program: jdbc-study
     * <br>description: test
     *
     * @author by 王林清 on 2021/7/30
     * @version Java1.9 IntelliJ IDEA
     */
    public class InsertTest {
        public static void main(String[] args) {
            Connection conn = null;
            Statement st = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                st = conn.createStatement();
                String sql = "insert into users(id, name, password, email, birthday) values (5, 'hhby', '1248', " +
                        "'2360039845@qq.com', '2001-10-10')";
                int i = st.executeUpdate(sql);
                if (i > 0) {
                    System.out.println("插入成功！");
                }
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            } finally {
                JdbcUtil.release(conn, st, rs);
            }
        }
    }
    ```

-   查询

    ```java
    package com.wlq.lesson2.util;
    
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/30
     * @version Java1.9 IntelliJ IDEA
     */
    public class SelectTest {
        public static void main(String[] args) {
            Connection conn = null;
            Statement st = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                st = conn.createStatement();
                String sql = "select * from users";
                rs = st.executeQuery(sql);
                while (rs.next()) {
                    System.out.println(rs.getString("name"));
                }
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            } finally {
                JdbcUtil.release(conn, st, rs);
            }
        }
    }
    ```

#### 3. SQL注入

>   SQL 注入（SQL Injection）是发生在 Web 程序中数据库层的安全漏洞，是网站存在最多也是最简单的漏洞。主要原因是程序对用户输入数据的合法性没有判断和处理，导致攻击者可以在 Web 应用程序中事先定义好的 SQL 语句中添加额外的 SQL 语句，在管理员不知情的情况下实现非法操作，以此来实现欺骗数据库服务器执行非授权的任意查询，从而进一步获取到数据信息。

-   例子

    ```java
    package com.wlq.lesson2;
    
    import com.wlq.lesson2.util.JdbcUtil;
    
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    /**
     * program: jdbc-study
     * <br>description: SQL 注入
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class SqlIn {
        public static void main(String[] args) {
            //sql 注入
            login("", "' or '1'='1");
    
            login("wlq", "1248");
        }
        //登录业务
        public static void login(String username, String password) {
            Connection conn = null;
            Statement st = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                st = conn.createStatement();
                String sql = "select * from users where name='" + username + "' and password='" + password +
                        "'";
                System.out.println(sql);
                rs = st.executeQuery(sql);
                while (rs.next()) {
                    System.out.println(rs.getString("name"));
                }
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            } finally {
                JdbcUtil.release(conn, st, rs);
            }
        }
    }
    // 运行结果
    select * from users where name='' and password='' or '1'='1'
    zhangsan
    lisi
    wangwu
    wlq
    select * from users where name='wlq' and password='1248'
    wlq
    ```

### 10.4 PreparedStatement类

>   PrepareStatement类是Statement的子类，通过预编译sql语句在传入参数来执行，相比于Statement可以防止SQL注入，效率更高。

#### 1. 代码实现

-   增删改(除sql语句不一样其他相同)

    ```java
    package com.wlq.lesson3;
    
    import com.wlq.lesson2.util.JdbcUtil;
    
    import java.sql.Connection;
    import java.sql.Date;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class InsertTest {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement ps = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                // 区别
                // 使用？占位符代替参数
                String sql = "insert into users(id, name, password, email, birthday) values (?, ?, ?, ?, ?)";
                // 预编译sql 先不执行
                ps = conn.prepareStatement(sql);
    
                // 手动赋值
                ps.setInt(1, 4);
                ps.setString(2, "qshh");
                ps.setString(3, "1234");
                ps.setString(4, "abc@cczu.edu.cn");
    
                //数据库的时间类型：java.sql.Date java用的时间：java.util.Date
                //System.currentTimeMills()获取系统当前时间戳
                System.out.println(System.currentTimeMillis());
                System.out.println(new java.util.Date().getTime());
                ps.setDate(5, new Date(System.currentTimeMillis()));
    
                //执行
                if (ps.executeUpdate() > 0) {
                    System.out.println("插入成功！");
                }
    
    
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                JdbcUtil.release(conn, ps, rs);
            }
        }
    }
    ```

-   查

    ```java
    package com.wlq.lesson3;
    
    import com.wlq.lesson2.util.JdbcUtil;
    
    import java.sql.Connection;
    import java.sql.Date;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class SelectTest {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement ps = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                // 区别
                // 使用？占位符代替参数
                String sql = "select * from users where char_length(name) > ?";
                // 预编译sql 先不执行
                ps = conn.prepareStatement(sql);
    
                // 手动赋值
                ps.setInt(1, 4);
    
                //执行,获取数据集
                rs = ps.executeQuery();
                while (rs.next()) {
                    System.out.println(rs.getString("name"));
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                JdbcUtil.release(conn, ps, rs);
            }
        }
    }
    ```

-   防止SQL注入

    ```java
    package com.wlq.lesson3;
    
    import com.wlq.lesson2.util.JdbcUtil;
    
    import java.sql.*;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class Login {
        public static void main(String[] args) {
            login("", "1248' or '1'='1");
    
            login("wlq", "1248");
        }
        //登录业务
        public static void login(String username, String password) {
            Connection conn = null;
            PreparedStatement ps = null;
            ResultSet rs = null;
            try {
                conn = JdbcUtil.getConnection();
                String sql = "select * from users where name=? and password=?";
                System.out.println(sql);
                ps = conn.prepareStatement(sql);
                ps.setString(1, username);
                ps.setString(2, password);
    
                rs = ps.executeQuery();
    
                while (rs.next()) {
                    System.out.println(rs.getString("name"));
                }
            } catch (SQLException throwables) {
                throwables.printStackTrace();
            } finally {
                JdbcUtil.release(conn, ps, rs);
            }
        }
    }
    //输出结果
    select * from users where name=? and password=?
    select * from users where name=? and password=?
    wlq
    ```

### 10.5 JDBC事务

#### 1. 代码实现

1.  开启事务：**`conn.setAutoCommit(false)`**
2.  一组业务执行完毕，提交事务
3.  可用在catch语句中显式的定义回滚语句，但是默认失败就会回滚

```java
import com.wlq.lesson2.util.JdbcUtil;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * program: jdbc-study
 * <br>description:
 *
 * @author by 王林清 on 2021/7/31
 * @version Java1.9 IntelliJ IDEA
 */
public class TestTransaction1 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement ps = null;
        ResultSet rs = null;

        try {
            conn = JdbcUtil.getConnection();

            // 关闭数据库的自动提交，相当于开启事务
            conn.setAutoCommit(false);

            String sql1 = "update account set money = money - 100 where name ='A'";
            ps = conn.prepareStatement(sql1);
            ps.executeUpdate();

            // 报错
//            int x = 1 / 0;

            String sql2 = "update account set money = money + 100 where name ='B'";
            ps = conn.prepareStatement(sql2);
            ps.executeUpdate();

            conn.commit();
            System.out.println("成功");

        } catch (Exception e) {
            //如果失败自动回滚，即使不写rollback()
//            try {
//                conn.rollback();
//            } catch (SQLException throwables) {
//                throwables.printStackTrace();
//            }
            e.printStackTrace();
        } finally {
            JdbcUtil.release(conn, ps, rs);
        }
    }
}
```

### 10.6 数据库连接池

>   数据库连接 --> 执行完毕 --> 释放 --> 再连接......  释放   十分浪费系统资源
>
>   数据库连接池负责分配、管理和释放数据库连接，它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个。
>
>   **池化技术**准备一些预先连接好了的资源，要用的时候就先连接准备好的，用完再放回去。
>
>   自己实现数据库连接池需要实现`DataSource`接口

#### 1. 常用参数

-   **最小连接数(minConnection)**：是连接池一直保持的数据库连接,所以如果应用程序对数据库连接的使用量不大,将会有大量的数据库连接资源被浪费。
-   **最大连接数(maxConnection)**：是连接池能申请的最大连接数,如果数据库连接请求超过次数,后面的数据库连接请求将被加入到等待队列中,这会影响以后的数据库操作。
-   **最大空闲时间**
-   **获取连接超时时间**
-   **超时重试连接次数**

#### 2. 开源数据库连接池实现

>   使用开源数据库连接池后，项目开发中就无需再自己编写数据库连接池了

-   DBCP：使用不多，tomcat使用的连接池
-   C3P0：已淘汰
-   Druid：阿里巴巴开源项目，功能全面
-   HikariCP：性能高

#### 3. DBCP

-   使用到的jar包：commons-dbcp-1.4、commons-pool-1.6

-   Maven依赖

    ```xml
    <dependency>
        <groupId>commons-dbcp</groupId>
        <artifactId>commons-dbcp</artifactId>
        <version>1.4</version>
    </dependency>
    <dependency>
        <groupId>commons-pool</groupId>
        <artifactId>commons-pool</artifactId>
        <version>1.6</version>
    </dependency>
    ```

-   配置文件：dbcpconfig.properties

    ```properties
    #连接设置
    driverClassName=com.mysql.cj.jdbc.Driver
    url=jdbc:mysql://localhost:3306/jdbc_study?useSSL=false
    username=root
    password=1248
    
    #!-- 初始化连接 --
    initialSize=10
    
    #最大连接数量
    maxActive=50
    
    #!-- 最大空闲连接 --
    maxIdle=20
    
    #!-- 最小空闲连接 --
    minIdle=5
    
    #!-- 超时等待时间以毫秒为单位 6000毫秒/1000等于60秒 --
    #JDBC驱动建立连接时附带的连接属性属性的格式必须为这样：【属性名=property;】
    maxWait=60000
    #注意：user 与 password 两个属性会被明确地传递，因此这里不需要包含他们。
    connectionProperties=useUnicode=true;characterEncoding=utf8
    
    #指定由连接池所创建的连接的自动提交（auto-commit）状态。
    defaultAutoCommit=true
    
    #driver default 指定由连接池所创建的连接的只读（read-only）状态。
    #如果没有设置该值，则“setReadOnly”方法将不被调用。（某些驱动并不支持只读模式，如：Informix）
    defaultReadOnly=false
    
    #driver default 指定由连接池所创建的连接的事务级别（TransactionIsolation）。
    #可用值为下列之一：（详情可见javadoc。）NONE,READ_UNCOMMITTED, READ_COMMITTED, REPEATABLE_READ, SERIALIZABLE
    defaultTransactionIsolation=READ_COMMITTED
    ```

-   工具类：DbcpUtil.java

    ```java
    import org.apache.commons.dbcp.BasicDataSourceFactory;
    
    import javax.sql.DataSource;
    import java.io.InputStream;
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    import java.util.Properties;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class DbcpUtil {
        private static DataSource dataSource = null;
    
        static {
            try {
                InputStream in = DbcpUtil.class.getClassLoader().getResourceAsStream("dbcpconfig.properties");
                Properties properties = new Properties();
                properties.load(in);
    
                //创建数据源 工厂模式 --> 创建
                dataSource = BasicDataSourceFactory.createDataSource(properties);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
        // 获取连接
        public static Connection getConnection() throws SQLException {
            return dataSource.getConnection();
        }
    
        // 释放连接资源
        public static void release(Connection conn, Statement st, ResultSet rs) {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (st != null) {
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```

-   代码实现

    ```java
    import com.wlq.lesson2.util.JdbcUtil;
    import com.wlq.lesson5.util.DbcpUtil;
    
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class DbcpTest {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement ps = null;
            ResultSet rs = null;
            try {
                conn = DbcpUtil.getConnection();
                // 区别
                // 使用？占位符代替参数
                String sql = "update users set name=? where id=?";
                // 预编译sql 先不执行
                ps = conn.prepareStatement(sql);
    
                // 手动赋值
                ps.setString(1, "wlq");
                ps.setString(2, "1");
    
                //执行
                if (ps.executeUpdate() > 0) {
                    System.out.println("修改成功！");
                }
    
    
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                DbcpUtil.release(conn, ps, rs);
            }
        }
    }
    ```

#### 4. C3P0

-   Maven依赖：

    ```xml
    <dependency>
      <groupId>com.mchange</groupId>
      <artifactId>c3p0</artifactId>
      <version>0.9.5.2</version>
    </dependency>
    ```

-   配置文件：c3p0-config.xml

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <c3p0-config>
        <!--使用默认的配置读取连接池对象-->
        <default-config>
            <!--连接参数-->
            <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
            <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbc_study?useSSL=false&amp;useUnicode=true
                &amp;characterEncoding=utf8
            </property>
            <property name="user">root</property>
            <property name="password">1248</property>
            <property name="acquireIncrement">50</property>
            <!--连接池参数-->
            <!--初始化申请的连接数量。在初始化时就申请的连接数-->
            <property name="initialPoolSize">5</property>
            <!--超时时间-->
            <property name="checkoutTimeout">3000</property>
            <property name="maxIdleTime">30</property>
            <!--最大的连接数量。超过该数目不会再申请多的连接-->
            <property name="maxPoolSize">10</property>
            <property name="minPoolSize">5</property>
            <property name="maxStatements">200</property>
        </default-config>
    
        <!--配置连接池mysql-->
        <named-config name="mysql">
            <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
            <property name="jdbcUrl">jdbc:mysql://localhost:3306/jdbc_study?useSSL=true&amp;useUnicode=true
                &amp;characterEncoding=utf8
            </property>
            <property name="user">root</property>
            <property name="password">1248</property>
    
            <property name="acquireIncrement">50</property>
            <property name="initialPoolSize">100</property>
            <property name="minPoolSize">50</property>
            <property name="maxPoolSize">1000</property>
            <property name="maxStatements">0</property>
            <property name="maxStatementsPerConnection">5</property>
            <!--超时时间-->
            <property name="checkoutTimeout">30000</property>
            <property name="maxIdleTime">30</property>
        </named-config>
    
        <!--配置连接池2-->
        <!--......-->
    </c3p0-config>
    ```

-   工具类：C3p0Util.java

    ```java
    import com.mchange.v2.c3p0.ComboPooledDataSource;
    
    import javax.sql.DataSource;
    import java.sql.Connection;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class C3p0Util {
        private static DataSource dataSource = null;
    
        static {
            try {
                //代码版配置
    //            ComboPooledDataSource dbSource = new ComboPooledDataSource();
    //            dbSource.setDriverClass();
    //            dbSource.setJdbcUrl();
    //            dbSource.setUser();
    //            dbSource.setPassword();
    //            dbSource.setMaxPoolSize();
    //            dbSource.setMinPoolSize();
                //配置文件创建数据源 不写参数是默认配置
                //写了参数是用的参数名的配置
                //如dataSource = new ComboPooledDataSource("mysql")就是用的
                //配置文件中的<named-config name="mysql">下的配置
                dataSource = new ComboPooledDataSource();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
        // 获取连接
        public static Connection getConnection() throws SQLException {
            return dataSource.getConnection();
        }
    
        // 释放连接资源
        public static void release(Connection conn, Statement st, ResultSet rs) {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (st != null) {
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```

-   代码实现

    ```java
    import com.wlq.lesson5.util.C3p0Util;
    
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class C3p0Test {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement ps = null;
            ResultSet rs = null;
            try {
                conn = C3p0Util.getConnection();
                // 区别
                // 使用？占位符代替参数
                String sql = "update users set name=? where id=?";
                // 预编译sql 先不执行
                ps = conn.prepareStatement(sql);
    
                // 手动赋值
                ps.setString(1, "wlq");
                ps.setInt(2, 2);
    
                //执行
                if (ps.executeUpdate() > 0) {
                    System.out.println("修改成功！");
                }
    
    
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                C3p0Util.release(conn, ps, rs);
            }
        }
    }
    ```

#### 5. **==Druid==**

-   maven依赖

    ```xml
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.2.6</version>
    </dependency>
    ```

-   配置文件：druid.properties

    ```properties
    #druid的配置和DBCP相似
    url=jdbc:mysql://localhost:3306/jdbc_study
    #这个可以缺省的，会根据url自动识别
    #driverClassName=com.mysql.cj.jdbc.Driver
    username=root
    password=1248
    
    #设置连接属性
    connectionProperties=useUnicode=true;characterEncoding=utf8;useSSL=false
    #初始连接数，默认0
    initialSize=10
    #最大连接数，默认8
    maxActive=30
    #最小闲置数
    minIdle=10
    #获取连接的最大等待时间，单位毫秒
    maxWait=2000
    #缓存PreparedStatement，默认false
    poolPreparedStatements=true
    #缓存PreparedStatement的最大数量，默认-1（不缓存）。大于0时会自动开启缓存PreparedStatement，所以可以省略上一句设置
    maxOpenPreparedStatements=20
    ```

-   工具类：

    ```java
    package com.wlq.lesson5.util;
    
    import com.alibaba.druid.pool.DruidDataSourceFactory;
    
    import javax.sql.DataSource;
    import java.io.InputStream;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.util.Properties;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class DruidUtil {
        private static DataSource dataSource = null;
    
        static {
            try {
                InputStream in = DruidUtil.class.getClassLoader().getResourceAsStream("druid.properties");
                Properties properties = new Properties();
                properties.load(in);
    
                //创建数据源 工厂模式 --> 创建
                dataSource = DruidDataSourceFactory.createDataSource(properties);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
        /**
         * 获取一个Druid连接池中的一个连接
         *
         * @return conn 数据库连接
         * @throws SQLException 数据库异常
         * @author 王林清
         * @since 2021/7/31 16:45
         */
        public static Connection getConnection() throws SQLException {
            return dataSource.getConnection();
        }
    
        /**
         * 销毁查询时用到的数据库资源
         *
         * @param conn 数据库连接资源
         * @param ps   sql预编译资源
         * @param rs   查询到的结果集资源
         * @author 王林清
         * @since 2021/7/31 16:43
         */
        public static void release(Connection conn, PreparedStatement ps, ResultSet rs) {
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            release(conn, ps);
        }
    
        /**
         * 在关闭增删改事务时释放资源的函数，无ResultSet资源
         *
         * @param conn 数据库连接资源
         * @param ps   sql预编译资源
         * @author 王林清
         * @since 2021/7/31 16:41
         */
        public static void release(Connection conn, PreparedStatement ps) {
            if (ps != null) {
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```

-   代码实现：

    ```java
    package com.wlq.lesson5;
    
    import com.wlq.lesson5.util.DruidUtil;
    
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    
    /**
     * program: jdbc-study
     * <br>description:
     *
     * @author by 王林清 on 2021/7/31
     * @version Java1.9 IntelliJ IDEA
     */
    public class DruidTest {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement ps = null;
            try {
                conn = DruidUtil.getConnection();
                // 区别
                // 使用？占位符代替参数
                String sql = "update users set name=? where id=?";
                // 预编译sql 先不执行
                ps = conn.prepareStatement(sql);
    
                // 手动赋值
                ps.setString(1, "wlq");
                ps.setString(2, "1");
    
                //执行
                if (ps.executeUpdate() > 0) {
                    System.out.println("修改成功！");
                }
    
    
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                DruidUtil.release(conn, ps);
            }
        }
    }
    ```

    

#### 6. 总结

>   ==**无论使用什么数据库连接池，其本质不会变，都是实现DataSource接口，JDBC操作不会变。**==

### 其他

-   参考：
    1.  [JDBC 简介_w3cschool](https://www.w3cschool.cn/jdbc/84pl1my8.html)
    2.  [JDBC URL参数配置](https://www.cnblogs.com/EasonJim/p/7659475.html)
    3.  [数据库驱动 - 炎泽 - 博客园](https://www.cnblogs.com/yanze/p/9714703.html#:~:text=数据库驱动. 定义：数据库驱动是不同数据库开发商（比如oracle,mysql等）为了某一种开发语言环境（比如java）能够实现数据库调用而开发的一个程序，. 他的作用相当于一个翻译人员，将Java中对数据库的调用语言翻译成数据库自己的数据库语言，当然这个翻译（数据库驱动）是由各个开发商针对统一的接口自定义开发的。. 常用驱动：.)
    4.  [SQL注入是什么，如何避免SQL注入？](http://c.biancheng.net/view/8283.html)
    5.  [Spring Boot（六）：那些好用的数据库连接池们 - 知乎](https://zhuanlan.zhihu.com/p/139950940)
    6.  [数据库连接池 - wenxuehai - 博客园](https://www.cnblogs.com/wenxuehai/p/15058811.html)
    7.  [数据库连接池学习：原理介绍+常用连接池介绍_CrankZ的博客-CSDN博客_数据库连接池](https://blog.csdn.net/CrankZ/article/details/82874158)

# 附录

## 1. MySQL关键字及保留字集合

|        ADD         |         ALL         |       ALTER        |
| :----------------: | :-----------------: | :----------------: |
|      ANALYZE       |         AND         |         AS         |
|        ASC         |     ASENSITIVE      |       BEFORE       |
|      BETWEEN       |       BIGINT        |       BINARY       |
|        BLOB        |        BOTH         |         BY         |
|        CALL        |       CASCADE       |        CASE        |
|       CHANGE       |        CHAR         |     CHARACTER      |
|       CHECK        |       COLLATE       |       COLUMN       |
|     CONDITION      |     CONNECTION      |     CONSTRAINT     |
|      CONTINUE      |       CONVERT       |       CREATE       |
|       CROSS        |    CURRENT_DATE     |    CURRENT_TIME    |
| CURRENT_TIMESTAMP  |    CURRENT_USER     |       CURSOR       |
|      DATABASE      |      DATABASES      |      DAY_HOUR      |
|  DAY_MICROSECOND   |     DAY_MINUTE      |     DAY_SECOND     |
|        DEC         |       DECIMAL       |      DECLARE       |
|      DEFAULT       |       DELAYED       |       DELETE       |
|        DESC        |      DESCRIBE       |   DETERMINISTIC    |
|      DISTINCT      |     DISTINCTROW     |        DIV         |
|       DOUBLE       |        DROP         |        DUAL        |
|        EACH        |        ELSE         |       ELSEIF       |
|      ENCLOSED      |       ESCAPED       |       EXISTS       |
|        EXIT        |       EXPLAIN       |       FALSE        |
|       FETCH        |        FLOAT        |       FLOAT4       |
|       FLOAT8       |         FOR         |       FORCE        |
|      FOREIGN       |        FROM         |      FULLTEXT      |
|        GOTO        |        GRANT        |       GROUP        |
|       HAVING       |    HIGH_PRIORITY    |  HOUR_MICROSECOND  |
|    HOUR_MINUTE     |     HOUR_SECOND     |         IF         |
|       IGNORE       |         IN          |       INDEX        |
|       INFILE       |        INNER        |       INOUT        |
|    INSENSITIVE     |       INSERT        |        INT         |
|        INT1        |        INT2         |        INT3        |
|        INT4        |        INT8         |      INTEGER       |
|      INTERVAL      |        INTO         |         IS         |
|      ITERATE       |        JOIN         |        KEY         |
|        KEYS        |        KILL         |       LABEL        |
|      LEADING       |        LEAVE        |        LEFT        |
|        LIKE        |        LIMIT        |       LINEAR       |
|       LINES        |        LOAD         |     LOCALTIME      |
|   LOCALTIMESTAMP   |        LOCK         |        LONG        |
|      LONGBLOB      |      LONGTEXT       |        LOOP        |
|    LOW_PRIORITY    |        MATCH        |     MEDIUMBLOB     |
|     MEDIUMINT      |     MEDIUMTEXT      |     MIDDLEINT      |
| MINUTE_MICROSECOND |    MINUTE_SECOND    |        MOD         |
|      MODIFIES      |       NATURAL       |        NOT         |
| NO_WRITE_TO_BINLOG |        NULL         |      NUMERIC       |
|         ON         |      OPTIMIZE       |       OPTION       |
|     OPTIONALLY     |         OR          |       ORDER        |
|        OUT         |        OUTER        |      OUTFILE       |
|     PRECISION      |       PRIMARY       |     PROCEDURE      |
|       PURGE        |        RAID0        |       RANGE        |
|        READ        |        READS        |        REAL        |
|     REFERENCES     |       REGEXP        |      RELEASE       |
|       RENAME       |       REPEAT        |      REPLACE       |
|      REQUIRE       |      RESTRICT       |       RETURN       |
|       REVOKE       |        RIGHT        |       RLIKE        |
|       SCHEMA       |       SCHEMAS       | SECOND_MICROSECOND |
|       SELECT       |      SENSITIVE      |     SEPARATOR      |
|        SET         |        SHOW         |      SMALLINT      |
|      SPATIAL       |      SPECIFIC       |        SQL         |
|    SQLEXCEPTION    |      SQLSTATE       |     SQLWARNING     |
|   SQL_BIG_RESULT   | SQL_CALC_FOUND_ROWS |  SQL_SMALL_RESULT  |
|        SSL         |      STARTING       |   STRAIGHT_JOIN    |
|       TABLE        |     TERMINATED      |        THEN        |
|      TINYBLOB      |       TINYINT       |      TINYTEXT      |
|         TO         |      TRAILING       |      TRIGGER       |
|        TRUE        |        UNDO         |       UNION        |
|       UNIQUE       |       UNLOCK        |      UNSIGNED      |
|       UPDATE       |        USAGE        |        USE         |
|       USING        |      UTC_DATE       |      UTC_TIME      |
|   UTC_TIMESTAMP    |       VALUES        |     VARBINARY      |
|      VARCHAR       |    VARCHARACTER     |      VARYING       |
|        WHEN        |        WHERE        |       WHILE        |
|        WITH        |        WRITE        |        X509        |
|        XOR         |     YEAR_MONTH      |      ZEROFILL      |

## 2. 习题及解答

```sql
use mysql_practice;
-- 第一题：取得每个部门最高薪水的人员名称
-- 这种写法是找出各一个最高的 可能会漏数据 不行
/*select ename, deptno, max(SAL) maxsal
from emp
group by DEPTNO;*/
select e.ename, t.maxsal, t.deptno
from emp as e
         join (select deptno, max(SAL) as maxsal
               from emp
               group by DEPTNO) as t on t.maxsal = e.SAL and t.DEPTNO = e.DEPTNO;


-- 第二题：哪些人的薪水在部门的平均薪水之上
-- 先求出每个部门的平均薪水
select deptno, avg(SAL) as avgsal
from emp
group by deptno;
-- 再联表查询
select e.ename, e.deptno, e.sal
from emp as e
         join (select deptno, avg(SAL) as avgsal
               from emp
               group by deptno) as t on t.DEPTNO = e.DEPTNO and t.avgsal < e.SAL;


-- 第三题：取得部门中（所有人的）平均的薪水等级
-- 平均的薪水等级：先计算每一个薪水的等级，然后找出薪水等级的平均值。
-- 平均薪水的等级：先计算平均薪水，然后找出每个平均薪水的等级值。
-- 基于子查询
-- 先计算所有人的薪水等级
select e.ename, e.sal, (select GRADE from salgrade as sg where e.sal between sg.LOSAL and sg.HISAL) as level
from emp as e;
-- 获取平均值
select t.DEPTNO, avg(`level`)
from (select e.sal,
             e.deptno,
             (select GRADE from salgrade as sg where e.sal between sg.LOSAL and sg.HISAL) as level
      from emp as e) as t
group by t.DEPTNO;

-- 联表查询
select e.ENAME, e.DEPTNO, e.SAL, sg.grade
from emp as e
         join salgrade as sg
              on e.SAL between sg.LOSAL and sg.HISAL;
select e.DEPTNO, avg(sg.GRADE) as avg_grade
from emp as e
         join salgrade as sg
              on e.sal between sg.LOSAL and sg.HISAL
group by e.DEPTNO;


-- 第四题：不准用组函数（Max），取得最高薪水（给出两种解决方案）
-- 法一：使用降序取第一条
select *
from emp
order by sal desc
limit 0, 1;
-- 法二：使用自连接
-- 自连接实现求出所有不是最大的sal
select a.SAL
from emp as a
         join emp as b on a.SAL < b.SAL;
-- 再从emp中选出不属于上表的数据，即是最大的
select distinct sal
from emp
where sal not in (select a.SAL
                  from emp as a
                           join emp as b on a.SAL < b.SAL
);


-- 第五题：取得平均薪水最高的部门的部门编号（至少给出两种解决方案）
-- 法一：降序，取第一条
select deptno
from emp
group by deptno
order by avg(sal) desc
limit 0,1;
-- 法二: 使用max
select avg(SAL)
from emp
group by deptno;
select max(t.avgsal)
from (select avg(SAL) as avgsal from emp group by deptno) as t;
select deptno
from emp
group by deptno
having avg(SAL) = (select max(t.avgsal) from (select avg(SAL) as avgsal from emp group by deptno) as t);


-- 第六题：取得平均薪水最高的部门的部门名称
-- 法一：利用第五题结果
select distinct DNAME
from dept
where DEPTNO = (select deptno
                from emp
                group by deptno
                order by avg(sal) desc
                limit 0,1);
select d.DNAME
from emp as e
         join dept as d using (deptno)
group by DEPTNO
order by avg(e.SAL) desc
limit 0, 1;

-- 第七题：求平均薪水的等级最低的部门的部门名称
-- 平均薪水的等级：先计算平均薪水，然后找出每个平均薪水的等级值。
-- 计算平均薪水
select DEPTNO, avg(SAL) as avgsal
from emp
group by DEPTNO;
-- 计算等级
select d.DNAME
from (select DEPTNO, avg(SAL) as avgsal from emp group by DEPTNO) as t
         join salgrade as s
              on t.avgsal between s.LOSAL and s.HISAL
         join dept as d using (deptno)
order by s.GRADE
limit 1;

-- ==============================等价于平均薪水最低====================================
select d.DNAME
from (select DEPTNO, avg(SAL) as avgsal from emp group by DEPTNO) as t
         natural join dept as d
order by t.avgsal
limit 1;


-- 第八题：取得比普通员工(员工代码没有在 mgr 字段上出现的)的最高薪水还要高的领导人姓名
-- 找到普通员工
select empno, sal
from emp
where EMPNO not in (select mgr from emp where mgr is not null);
-- 取得薪水最高的
-- 任何值与null进行比较结果必为false，
-- 如not in的原理是依次进行!=判断，如果not in (表达式)中有null值则not in的结果也必是空值，
-- 所以在用not in时注意后面的表达式中不能有空值最好加上 where xxx is not null
select ENAME, SAL
from emp as e
where sal > (select max(SAL) from emp where EMPNO not in (select mgr from emp where mgr is not null));


-- 第九题：取得薪水最高的前五名员工
-- 降序取前五条
select *
from emp
order by sal desc
limit 0, 5;


-- 第十题：取得薪水最高的第六到第十名员工
-- 降序，分页
select ENAME, SAL
from emp
order by SAL desc
limit 1, 5;


-- 第十一题：取得最后入职的 5 名员工
select ENAME, HIREDATE
from emp
order by HIREDATE desc
limit 0, 5;


-- 第十二题：取得每个薪水等级有多少员工
select s.GRADE, count(e.EMPNO) as num
from emp as e
         join salgrade as s on e.SAL between s.LOSAL and s.HISAL
group by s.GRADE;


create database if not exists `student` character set utf8 collate utf8_general_ci;
use student;


-- 第十三题：面试题
-- 有 3 个表 S(学生表)，C（课程表），SC（学生选课表）
-- S（SNO，SNAME）代表（学号，姓名）
-- C（CNO，CNAME，CTEACHER）代表（课号，课名，教师）
-- SC（SNO，CNO，SCGRADE）代表（学号，课号，成绩）
-- 问题：请用标准 SQL 语言写出答案，方言也行（请说明是使用什么方言）。
-- 1，找出没选过“黎明”老师的所有学生姓名。
-- 先找出选过课的学生
select distinct sno -- 子查询
from sc
where cno in (select cno from c where CTEACHER = '黎明');
select distinct sc.sno -- 联表查询
from sc
         join c on sc.CNO = c.CNO and c.CTEACHER = '黎明';
-- 再not in
select s.sname
from s
where s.sno not in (select distinct sno
                    from sc
                    where cno in (select cno from c where CTEACHER = '黎明'));
select distinct s.SNAME
from s
where sno not in (select distinct sc.sno
                  from sc
                           join c on sc.CNO = c.CNO and c.CTEACHER = '黎明');

-- 2，列出 2 门以上（含 2 门）不及格学生姓名及平均成绩。
-- 法一 count条件查询
select s.sname, avg(sc.SCGRADE) as avggrade
from sc
         natural join s
group by SNO
-- count 条件查询三种形式
-- having count(if(sc.scgrade < 60, 1, null)) > 2;
-- having count(case when sc.scgrade < 60 then 1 end) >2;
having count(sc.SCGRADE < 60 or null) > 2;
-- 法二子查询
select SNO, count(SNO) as nopass -- 求出不及格门书大于2的学号
from sc
where SCGRADE < 60
group by SNO
having nopass >= 2;
select s.SNAME, avg(sc.SCGRADE) -- 联表查询
from sc
         join s on s.SNO = sc.SNO and s.SNO in (select SNO
                                                from sc
                                                where SCGRADE < 60
                                                group by SNO
                                                having count(s.SNO) >= 2)
group by s.SNO;
-- 3，即学过 1 号课程又学过 2 号课所有学生的姓名。
select distinct s.sname
from sc
         right join s on sc.sno = s.SNO and sc.cno in (1, 2)
group by s.SNO
having count(s.SNO) = 2;

use mysql_practice;
-- 第十四题：列出所有员工及领导的姓名
-- 自连接
select distinct a.ename, ifnull(b.ENAME, '无') as leader
from emp as a
         left join emp as b on a.MGR = b.EMPNO;


-- 第十五题：列出受雇日期早于其直接上级的所有员工的编号,姓名,部门名称
-- 子查询
select e.DEPTNO, e.ENAME, d.DNAME
from emp as e
         join dept as d using (deptno)
where e.HIREDATE < (select HIREDATE from emp where EMPNO = e.MGR);
-- 自连接
select a.deptno, a.ename, d.dname
from emp as a
         join emp as b on b.empno = a.mgr and a.HIREDATE < b.HIREDATE
    -- 有三个deptno字段所以不能使用natural 或 using
         join dept as d on a.DEPTNO = d.DEPTNO;


-- 第十六题：列出部门名称和这些部门的员工信息,同时列出那些没有员工的部门.
select d.DNAME, emp.*
from emp
         natural right join dept as d;


-- 第十七题：列出至少有 5 个员工的所有部门
select d.DNAME, count(e.EMPNO) as num
from emp as e
         natural join dept as d
group by e.DEPTNO
having num >= 5;


-- 第十八题：列出薪金比"SMITH"多的所有员工信息.
select *
from emp
where sal > (select sal from emp where ENAME = 'SMITH');


-- 第十九题：列出所有"CLERK"(办事员)的姓名及其部门名称,部门的人数.
select e.DEPTNO, d.dname, count(e.EMPNO) as num
from emp as e
         natural join dept as d
group by e.DEPTNO;

select e.ENAME, t.DNAME, t.num
from emp as e
         natural join (select e.DEPTNO, d.dname, count(e.EMPNO) as num
                       from emp as e
                                natural join dept as d
                       group by e.DEPTNO) as t
where e.JOB = 'CLERK';


-- 第二十题：列出最低薪金大于 1500 的各种工作及从事此工作的全部雇员人数.
-- 找出各JOB的最低薪金
select JOB, count(EMPNO) as num
from emp
group by JOB
having min(SAL) > 1500;


-- 第二十一题：列出在部门"SALES"<销售部>工作的员工的姓名,假定不知道销售部的部门编号.
select d.DNAME, e.ENAME
from emp as e
         natural join dept as d
where d.DNAME = 'SALES';


-- 第二十二题：列出薪金高于公司平均薪金的所有员工,所在部门,上级领导,雇员的工资等级.
select avg(SAL)
from emp;
select distinct a.ENAME as 员工姓名, d.DNAME as 部门名, ifnull(b.ENAME, '无') as 领导姓名, s.grade as 薪水等级
from emp as a
         left join emp as b on a.MGR = b.EMPNO
         join dept as d on a.DEPTNO = d.DEPTNO
         join salgrade as s on a.SAL between s.LOSAL and s.HISAL
where a.sal > (select avg(SAL)
               from emp);


-- 第二十三题：列出与"SCOTT"从事相同工作的所有员工及部门名称.
select JOB, DEPTNO
from emp
where ENAME = 'SCOTT';
select e.ename, d.dname
from emp as e
         natural join dept as d
where e.JOB = (select JOB from emp where ENAME = 'SCOTT')
  and e.ENAME != 'scott';


-- 第二十四题：列出薪金等于部门 30 中员工的薪金的其他员工的姓名和薪金.
select sal
from emp
where DEPTNO = 30;
select ENAME, SAL
from emp
where sal in (select sal from emp where DEPTNO = 30 and sal is not null)
  and DEPTNO <> 30;


-- 第二十五题：列出薪金高于在部门 30 工作的所有员工的薪金的员工姓名和薪金.部门名称.
select max(SAL)
from emp
where DEPTNO = 30;
select e.ENAME, e.SAL, d.DNAME
from emp as e
         join dept as d using (deptno)
where e.SAL > (select max(SAL) from emp where DEPTNO = 30);


-- 第二十六题：列出在每个部门工作的员工数量,平均工资和平均服务期限.
select d.DEPTNO,
       d.DNAME,
       ifnull(count(EMPNO), 0)                                as empnum,
       ifnull(avg(SAL), 0)                                    as avgsal,
       ifnull(avg(timestampdiff(year, e.HIREDATE, now())), 0) as avgdate
from emp as e
         right join dept as d using (deptno)
group by e.DEPTNO;


-- 第二十七题：列出所有员工的姓名、部门名称和工资。
select e.empno, e.ename, e.sal, d.dname
from emp as e
         natural left join dept as d;


-- 第二十八题：列出所有部门的详细信息和人数
select d.DEPTNO, d.DNAME, count(e.EMPNO) as dnum
from dept as d
         natural left join emp as e
group by d.DEPTNO;


-- 第二十九题：列出各种工作的最低工资及从事此工作的雇员姓名
select JOB, min(SAL)
from emp
group by JOB;
select e.ENAME, t.minsal, t.job
from emp as e
         join (select JOB, min(SAL) as minsal from emp group by JOB) as t on e.JOB = t.JOB and e.SAL = t.minsal;


-- 第三十题：列出各个部门的 MANAGER(领导)的最低薪金
select distinct b.SAL, b.DEPTNO
from emp as a
         join emp as b on a.mgr = b.EMPNO;
select d.DNAME, min(t.SAL)
from dept as d
         join (select distinct b.SAL, b.DEPTNO
               from emp as a
                        join emp as b on a.mgr = b.EMPNO) as t using (deptno)
group by d.DEPTNO;


-- 第三十一题：列出所有员工的年工资,按年薪从低到高排序
select ename, sal * 12 as annaysal
from emp
order by annaysal;


-- 第三十二题：求出员工领导的薪水超过 3000 的员工名称与领导名称
select a.ENAME, b.ENAME
from emp as a
         join emp as b on a.mgr = b.EMPNO and b.sal > 3000;


-- 第三十三题：求出部门名称中,带'S'字符的部门员工的工资合计、部门人数.
select d.DNAME, sum(e.SAL) as sumsal, count(e.EMPNO) as enum
from dept as d
         left join emp as e using (deptno)
where d.DNAME like '%S%'
group by d.DEPTNO;


-- 第三十四题：给任职日期超过 30 年的员工加薪 10%.
update emp
set sal = sal * 1.1
where timestampdiff(year, HIREDATE, now()) > 30;
```

## 3. 参考(总)

1.  [【狂神说Java】MySQL最新教程通俗易懂_哔哩哔哩_](https://www.bilibili.com/video/BV1NJ411J79W)

2.  [狂神说Java MySQL文档](http://mp.weixin.qq.com/mp/homepage?__biz=Mzg2NTAzMTExNg==&hid=4&sn=044c8767bd3c1825a329c2b98fff2ffe&scene=18#wechat_redirect)

