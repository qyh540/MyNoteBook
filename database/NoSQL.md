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





# 三、Redis