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

<img src="https://img-blog.csdnimg.cn/2019111715455711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Zlc2ZzZWZncw==,size_16,color_FFFFFF,t_70" alt="区别" style="zoom:150%;" />

NoSQL数据库按照其存储类型可以大致分为以下几类：

| 类型       | 部分代表                            | 特点                                                         |
| ---------- | ----------------------------------- | ------------------------------------------------------------ |
| 列族数据库 | HBase<br>Cassandra<br>Hypertable    | 顾名思义是按列存储数据的。最大的特点是方便存储结构化和半结构化数据，方便做数据压缩，对针对某一列或者某几列的查询有非常大的I/O优势，适合于批量数据处理和即时查询。 |
| 文档数据库 | MongoDB<br>CouchDB<br>ElasticSearch | 文档数据库一般用类JSON格式存储数据，存储的内容是文档型的。这样也就有机会对某些字段建立索引，实现关系数据库的某些功能，但不提供对参照完整性和分布事务的支持。 |
| KV数据库   | DynamoDB<br>Redis<br>LevelDB        | 可以通过key快速查询到其value，有基于内存和基于磁盘两种实现方案。 |
| 图数据库   | Neo4J<br>FlockDB<br>JanusGraph      | 使用图结构进行语义查询的数据库，它使用节点、边和属性来表示和存储数据。图数据库从设计上，就可以简单快速的检索难以在关系系统中建模的复杂层次结构。 |
| 对象数据库 | db4o<br>Versant                     | 通过类似面向对象语言的语法操作数据库，通过对象的方式存取数据。 |

# 二、MongoDB

# 三、Redis