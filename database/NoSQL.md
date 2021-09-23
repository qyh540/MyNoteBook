# NoSQL数据库学习

>   作业：
>
>   1.  安装MongoDB并运行
>   2.  安装Redis并运行
>   3.  使用命令行完成MongoDB的基本功能
>   4.  使用命令行完成Redis的基本功能
>   5.  使用程序接口使用MongoDB
>   6.  使用程序接口使用Redis

>   考试：
>
>   1.  30道单选
>   2.  1~3道问答题

# 一、关系型(SQL)数据库和非关系型(NoSQL)数据库

>   NoSQL：非关系型数据库，主要用于处理数据量很大或者对数据访问效率要求很高的从而必须将数据放在集群上的场景。抑或是想采用一种更为方便的数据交互方式来提高应用程序开发效率。
>
>   -   关系型数据库二十多年来一直很成功，能够持久保存数据，控制并发访问，同时也提供了一套集成机制。
>
>   -   由于关系模型与内存中的数据结果不匹配，所以应用程序开发人员一直为这种阻抗失谐的问题所困扰。
>   -   数据库领域的迁移方式是：原来，各个应用程序都把同一份数据库当成共用的集成点，而现在，各个应用程序都会封装自己的数据库，并通过服务彼此集成。
>   -   促使数据存储方式发生变化的重要原因是：需要在集群上运行大量数据，而关系型数据库不能在集群上高效运行。
>   -   NoSQL是偶然出现的新名词，它没有规范的定义，我们只能描述此类数据库所共有的特征。
>   -   各种NoSQL数据库的共同特性是：
>       -   不使用关系模型
>       -   在集群中运行良好
>       -   开源
>       -   适用于21世纪的互联网公司
>       -   无模式
>   -   NoSQL崛起所产生的重要影响是混合持久化。
>   -   NoSQL技术与传统的关系型数据库相比，一个最明显的转变就是抛弃了关系模型。每种NoSQL解决方案的模型都不同，大致分为4类："键值"、"文档"、"列族"和"图"。前三类数据模型有一个共同特征，我们称其为"面向聚合"。

<img src="https://img-blog.csdnimg.cn/2019111715455711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Zlc2ZzZWZncw==,size_16,color_FFFFFF,t_70" alt="区别" style="zoom:150%;" />

NoSQL数据库按照其存储类型可以大致分为以下几类：

| 类型       | 部分代表                      | 特点                                                         |
| ---------- | ----------------------------- | ------------------------------------------------------------ |
| 列族数据库 | HBase Cassandra Hypertable    | 顾名思义是按列存储数据的。最大的特点是方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的I/O优势，适合于批量数据处理和即时查询。 |
| 文档数据库 | MongoDB CouchDB ElasticSearch | 文档数据库一般用类JSON格式存储数据，存储的内容是文档型的。这样也就有机会对某些字段建立索引，实现关系数据库的某些功能，但不提供对参照完整性和分布事务的支持。 |
| KV数据库   | DynamoDB Redis LevelDB        | 可以通过key快速查询到其value，有基于内存和基于磁盘两种实现方案。 |
| 图数据库   | Neo4J FlockDB JanusGraph      | 使用图结构进行语义查询的数据库，它使用节点、边和属性来表示和存储数据。图数据库从设计上，就可以简单快速的检索难以在关系系统中建模的复杂层次结构。 |
| 对象数据库 | db4o Versant                  | 通过类似面向对象语言的语法操作数据库，通过对象的方式存取数据。 |

# 二、MongoDB

## 1.基本概念

-   MongoDB数据库属于文档数据库，可以存放并获取文档。

-   MySQL和MongoDB的术语间的对应关系

| SQL                   | MongoDB            |
| --------------------- | ------------------ |
| database              | database           |
| table（表）           | collection（集合） |
| row（行）             | document（文档）   |
| column（列）          | field（字段）      |
| index                 | index              |
| table joins（表连接） | （嵌套文档）       |
| primary key           | primary key        |

## 2. 常用命令

### 1. 连接Mongo Shell

-   常用参数：`host、port、username、password、authenticationDatabase`

```bash
# 使用mongo直接连接本地默认端口
mongo

# 使用host(主机) port(端口) 等可以指定连接主机端口的数据库
mongo --host <host> --port <port>
# 等价于
mongo --host <host>:<port>
# 抑或
mongo "mongodb://<host>:<port>"

# 使用用户名密码直接验证登录
mongo --username <username> --password <password> --authenticationDatabase <database>
```

-   其他操作

```shell
# 查看当前数据库
db

# 查看可用数据库
show databases
show dbs

# 查看集合
show collections

# 查看用户
show users

# 查看可定义角色
show roles

# 切换数据库
use dbname

# 用户验证
db.auth('username', 'password')

# 退出
exit
quit()
ctrl + c

# 帮助
db.help()
db.colleciton.help()
```

### 2. CRUD操作

#### 1. 插入(Create)

>   如果插入数据库、集合不存在，则创建新的数据库、集合。
>
>   多行操作：以`(`、`[`或`{`开头，省略`)`、`[`、`}`结尾就可以换行进行多行操作，最后添加`)`、`[`、`}`

```bash
# 插入单条记录
db.collection.insertOne({xx:xx, ...})

#插入多条记录
db.collection.insertMany([{xx:xx, ..}, {...}])
```

#### 2. 查找(Read)

```bash
# 查询
db.collection.find({xx:xx})
```

#### 3. 更新(Update)

```bash
db.collection.updateOne()
db.collection.updateMany()
db.collection.replaceOne()
```

#### 4. 删除(Delete)

```bash
db.collection.deleteOne()
db.collection.deleteMany()
```

### 3. 用户角色管理

#### 1. 角色管理

>   MongoDB内部提供了一系列内置的角色，这些角色是为了完成一些基本的数据库操作。每个内置角色提供了用户在角色数据库内数据库级别所有非系统类集合的访问权限，也提供了对集合级别所有系统集合的访问权限。MongoDB在每个数据库上都提供内置的数据库用户角色和数据库管理角色，但只在admin数据库中提供其它的内置角色。
>
>   内置角色分类：
>
>   数据库用户角色(Database User Roles)
>   数据库管理角色(Database Administration Roles)
>   集群管理角色(Cluster Administration Roles)
>   备份和恢复角色(Backup and Restoration Roles)
>   全数据库级角色(All-Database Roles)
>   超级用户角色(Superuser Roles)
>   内部角色(Internal Role)

-   常用内置角色

| 角色                 | 权限描述                                                     |
| -------------------- | ------------------------------------------------------------ |
| read                 | 可以读取指定数据库中任何数据。                               |
| readWrite            | 可以读写指定数据库中任何数据，包括创建、重命名、删除集合。   |
| readAnyDatabase      | 可以读取所有数据库中任何数据(除了数据库config和local之外)。  |
| readWriteAnyDatabase | 可以读写所有数据库中任何数据(除了数据库config和local之外)。  |
| dbAdmin              | 可以读取指定数据库以及对数据库进行清理、修改、压缩、获取统计信息、执行检查等操作。 |
| dbAdminAnyDatabase   | 可以读取任何数据库以及对数据库进行清理、修改、压缩、获取统计信息、执行检查等操作(除了数据库config和local之外)。 |
| clusterAdmin         | 可以对整个集群或数据库系统进行管理操作。                     |
| userAdmin            | 可以在指定数据库创建和修改用户。                             |
| userAdminAnyDatabase | 可以在指定数据库创建和修改用户(除了数据库config和local之外)。 |

```bash
db.createRole()	#创建一个角色并指定其特权。
db.dropRole()	#删除用户定义的角色。
db.dropAllRoles()	#删除与数据库关联的所有用户定义角色。
db.getRole()	#返回指定角色的信息。
db.getRoles()	#返回数据库中所有用户定义角色的信息。
db.grantPrivilegesToRole()	#将特权分配给用户定义的角色。
db.revokePrivilegesFromRole()	#从用户定义的角色中删除指定的特权。
db.grantRolesToRole()	#指定用户定义角色从中继承特权的角色。
db.revokeRolesFromRole()	#从角色中删除继承的角色。
db.updateRole()	#更新用户定义的角色。
```

#### 2. 用户管理

>   MongoDB是基于角色的访问控制，所以创建用户需要指定用户的角色，在创建用户之前需要满足：
>
>   先在admin数据库中创建角色为userAdmin或userAdminAnyDatabase的用户作为管理用户的用户；
>   启用访问控制，进行登录用户验证，这样创建用户才有意义。

```bash
db.auth()	#向数据库验证用户。
db.changeUserPassword()	#更改现有用户的密码。
db.createUser()	#创建一个新用户。
db.dropUser()	#删除一个用户。
db.dropAllUsers()	#删除与数据库关联的所有用户。
db.getUser()	#返回有关指定用户的信息。
db.getUsers()	#返回有关与数据库关联的所有用户的信息。
db.grantRolesToUser()	#向用户授予角色及其特权。
db.removeUser()	#不推荐使用。从数据库中删除用户。
db.revokeRolesFromUser()	#从用户删除角色。
db.updateUser()	#更新用户数据。
passwordPrompt()	#提示输入密码，以作为在各种mongoShell用户身份验证/管理方法中直接指定密码的替代方法。
```



# 三、Redis

## 1. 基本概念

### 1. 简介

-   Redis是属于键值数据库，运行在内存中

### 2. 5种数据结构

#### 1. `String`字符串

-   Redis的字符串和其他编程语言或者其他键值存储提供的字符串非常相似。

![image-20210922184225795](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210922184225795.png)

-   字符串的方法：
    -   GET：获取存储在给定键中的值。
    -   SET：设置存储在给定键中的值。
    -   DEL：删除存储在给定键中的值（这个命令可以用于所有类型）。

#### 2. `List`列表

![image-20210922185101606](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210922185101606.png)

-   列表的方法
    -   RPUSH：将给定值推入列表的右端。
    -   LRANGE：获取列表在给定范围上的所有值。
    -   LINDEX：获取列表在给定位置上的单个元素。
    -   LPOP：从列表的左端弹出一个值，并返回被弹出的值。

#### 3. `Set`集合

-   Redis 的集合和列表都可以存储多个字符串，它们之间的不同在于，列表可以存储多个相同的字符串，而集合则通过使用散列表来保证自己存储的每个字符串都是各不相同的（这些散列表只有键，但没有与键相关联的值）。
-   因为Redis的集合使用无序（unordered）方式存储元素，所以用户不能像使用列表那样，将元素推入集合的某一端，或者从集合的某一端弹出元素。不过用户可以使用SADD命令将元素添加到集合，或者使用SREM命令从集合里面移除元素。另外还可以通过SISMEMBER命令快速地检查一个元素是否已经存在于集合中，或者使用SMEMBERS命令获取集合包含的所有元素（如果集合包含的元素非常多，那么SMEMBERS命令的执行速度可能会很慢，所以请谨慎地使用这个命令）

![image-20210922192039071](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210922192039071.png)

-   集合的方法
    -   sadd：将给定元素添加到集合
    -   smembers：返回集合包含的所有元素
    -   sismember：检查给定元素是否存在于集合中
    -   srem：如果给定的元素存在于集合中，那么移除这个元素
    -   sinter：计算交集
    -   sunion：计算并集
    -   sdiff：计算差集

#### 4. `Hash`散列

-   Redis的散列可以存储多个键值对之间的映射。和字符串一样，散列存储的值既可以是字符串又可以是数字值，并且用户同样可以对散列存储的数字值执行自增操作或者自减操作。

![image-20210922195124165](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210922195124165.png)

-   散列的方法
    -   HSET：在散列里面关联起给定的键值对。
    -   HGET：获取指定散列键的值
    -   HGETALL：获取散列包含的所有键值对
    -   HDEL：如果给定键存在于散列里面，那么移除这个键

#### 5. `Zset`有序集合

-   有序集合和散列一样，都用于存储键值对：有序集合的键被称为成员（member），每个成员都是独各不相同；而有序集合的值则被称为分值（score），**==分值必须为浮点数==**。有序集合是Redis里面唯一一个既可以根据成员访问元素（这一点和散列一样），又可以根据分值以及分值的排列顺序来访问元素的结构。

![image-20210922233253954](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210922233253954.png)

-   有序集合的方法
    -   zadd：将一个带有给定分值的成员添加到有序集合里面
    -   zrange：根据元素在有序排列中所处的位置，从有序集合里面获取多个元素
    -   zrangebyscore：获取有序集合在给定分值范围内的所有元素
    -   zrem：如果给定成员存在于有序集合，那么移除这个成员

