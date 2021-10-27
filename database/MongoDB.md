# MongoDB学习

## 1. 简介

-   MongoDB是一款强大、灵活，且易于扩展的通用
    型NoSQL数据库。它能扩展出非常多的功能，如二级索
    引（secondary index）、范围查询（range
    query）、排序、聚合（aggregation），以及地理
    空间索引（geospatial index）。
-   主要设计特点：
    -   易于使用
    -   易于扩展

## 2. 基本概念

### 1. 文档 Document

-   MongoDB数据库属于文档数据库，可以存放并获取文档。
-   MongoDB中的文档以键值对形式存在，键是字符串，可以使用任意UTF-8字符。但：
    -   键不能含有`\0`(系统用来表键尾)
    -   `.和$`有特殊用法，不能随意使用
-   文档值可以是普通值也可以是文档(嵌套)、集合，值区分类型、大小写。
-   文档键值对有序，键不能重复。
-   下列文档皆不相同：

```json
{"foo": 3}
{"Foo": 3}
{"foo": "3"}
{"x":0, "y":1}
{"y":1, "x":0}
```

### 2. 集合 Collection

-   集合就是一组文档。
-   集合中的文档可以是不同类型的(结构不同)。
-   集合名不能是空字符串`""`、空字符`\0`、不能以`system.`开头、不能包含`$`。
-   子集合：组织集合的一种惯例是使用`.`分隔不同命名空间
    的子集合。

### 3. 数据库 Database

-   数据库由集合组成，每个数据库可以有0个或多个集合。
-   每一个数据库都拥有独立的权限。
-   数据库命名规则
    -   不能是空字符串`""`。
    -   不得含有`/、\、.、"、*、<、>、:、|、?、$（一个空格）、\0（空字符）`。基本上，只能使用ASCII中的字母和数字。
    -   数据库名区分大小写，即便是在不区分大小写的文件系统中也是如此。简单起见，数据
        库名应全部小写。
    -   数据库名最多为64字节。
-   保留的数据库名(不可被使用)：
    -   admin
    -   local
    -   config

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

### 4. Mongo Shell

-   shell是一个功能完备的JavaScript解释器，可运行任意JavaScript程序，可充分利用JavaScript的标准库。

### 5. 基础命令

#### 1. 连接Mongo Shell

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

#### 2. CRUD操作

##### 1. 插入(Create)

>   如果插入数据库、集合不存在，则创建新的数据库、集合。
>
>   多行操作：以`(`、`[`或`{`开头，省略`)`、`[`、`}`结尾就可以换行进行多行操作，最后添加`)`、`[`、`}`
>
>   连续输入3次`Enter`则结束(废弃)当前输入命令进入下一次输入。

```bash
# 插入单条记录
db.collection.insertOne({xx:xx, ...})

#插入多条记录
db.collection.insertMany([{xx:xx, ..}, {...}])
```

##### 2. 查找(Read)

```bash
# 查询
db.collection.find({xx:xx})
```

##### 3. 更新(Update)

```bash
db.collection.updateOne()
db.collection.updateMany()
db.collection.replaceOne()
```

##### 4. 删除(Delete)

```bash
db.collection.deleteOne()
db.collection.deleteMany()
```


#### 3. 用户角色管理

##### 1. 角色管理

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

##### 2. 用户管理

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

### 6. 数据类型

-   null：用于表示空值或者不存在的字段
-   布尔型：有2个值true和false
-   数值：shell默认使用64位浮点型数值。可以使用`NumberInt()、NumberLong()`表示4B和8B带符号整数。
-   字符串：UTF-8字符串都可表示为字符串类型。
-   日期：日期被存储为自新纪元以来经过的毫秒数，不存储时区。
-   正则表达式：可以在 查询时使用正则表达式作为限定条件。
-   数组
-   内嵌文档：文档可嵌套其他文档，被嵌套的文档作为父文档的值。
-   对象id对象id：对象id是一个12字节的ID，是文档的唯一标识。
    -   在一个集合里每一个文档都必须有一个`_id`键，值可以是任何类型，默认是ObjectID对象，在每一个集合中`_id`值唯一，不同集合中可以存在相同的`_id`值。
    -   如果插入文档时没有"_id"键，系统会自动帮你创建一个。
-   二进制数据：二进制数据是一个任意字节的字符串。它不能直接在shell中使用。如果要将非UTF-8字符保存到数据库中，二进制数据是唯一的方式。
-   代码：查询和文档中可以包括任意JavaScript代码。

```js
{"x": null}
{"x": true}
{"x": 3.14}
{"x": NumberInt(3)}
{"x": "hhby"}
{"x": new Date()}
{"x": [1, 2, 3, 4]}
{"x": {"y": xxx}}
{"x": ObjectId()}
{"x": function() { /* ... */ }}
```

