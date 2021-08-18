# 搭建cloudmanager

## 创建云服务器（三台）

按量付费 同一地区 计算型c6/ecs.c6 专有网络 按固定带宽1Mbps

### node01

4核8GB

### node02

2核4GB

### node03

2核4GB

## 创建安全组

![image-20210414213532923](image-20210414213532923.png)

## 实例绑定安全组

![image-20210414213601017](image-20210414213601017.png)

## ssh 远程连接服务器

### 基础配置

#### 修改yum源

1. 修改文件

```
vim /etc/yum.repos.d/CentOS-Base.repo 
```

只修改专有网络 删除原有 base update extras vim快捷键 ==22dd== 删除1 - 22 行

```
[base]
name=CentOS-6.10
enabled=1
failovermethod=priority
baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/os/$basearch/
gpgcheck=1
gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6

[updates]
name=CentOS-6.10
enabled=1
failovermethod=priority
baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/updates/$basearch/
gpgcheck=1
gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6

[extras]
name=CentOS-6.10
enabled=1
failovermethod=priority
baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/extras/$basearch/
gpgcheck=1
gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
```

2. 修改文件 vim快捷键 ==7dd== 删除 1 - 7行 

```
vim /etc/yum.repos.d/epel.repo
```

```
[epel]
name=Extra Packages for Enterprise Linux 6 - $basearch
enabled=1
failovermethod=priority
baseurl=http://mirrors.cloud.aliyuncs.com/epel-archive/6/$basearch
gpgcheck=0
gpgkey=http://mirrors.cloud.aliyuncs.com/epel-archive/RPM-GPG-KEY-EPEL-6
```

#### 修改网络配置

1. 配置内网ip和主机名（另外两台的ip）

```
vim /etc/hosts
```

```
内网ip	主机名
```

#### 关闭防火墙（可省略）

```
service iptables stop

chkconfig iptables off
```

或

```
systemctl stop firewalld
systemctl disable firewalld
```

#### 验证

```
ping 主机名
```

#### 免密登录

1. 都执行命令

```
ssh localhost

# 检查（可省）
cd ~ | ls -a
```

2. 生成公钥和私钥（都执行）

```
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
```

3. 发送公钥到另外两台

```
# 三台所有语句都要执行
ssh-copy-id cdh-node01
ssh-copy-id cdh-node02
ssh-copy-id cdh-node03
```

4. 验证

```
# 用ssh连接另外两台
ssh 主机名
```

### 安装软件

#### 安装jdk

1. 在三台机器新建software文件夹

```
mkdir /software
```

2. 将文件传输到另外两台

```
# 只修改节点名即可
scp jdk-7u67-linux-x64.rpm cdh-node02:`pwd`
```

3. 解压

```
rpm -i /soft*/jdk*
```

4. 配置环境变量

```
vim /etc/profile
```

```
# 追加
export JAVA_HOME=/usr/java/jdk1.7.0_67
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

5. 加载配置

```
. /etc/profile
# 或
source /etc/profile
```

6. 验证

```
java -version
```

#### 时间配置

1. 检查时间是否一致，若一致，下一步省略

```
# 检查时间
date
```

2. 设置开机启动

```
chkconfig ntpd on
# 设置时间同步
ntpdate node01内网ip
```

#### 安装mysql （node01）

1. 安装

```
yum -y install mysql-server
```

2. 开启服务

```
service mysqld start
# 或
systemctl restart mysqld.service
```

3. 重置密码

```
# 默认无密码，直接回车
/usr/bin/mysql_secure_installation
# 输入密码后 分别是 n n n y
```

4. 进入mysql

```
mysql -uroot -p
```

5. 删除 user

```
user mysql;
delete from user;
# 重新授权 密码自定义
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123' WITH GRANT OPTION;
```

6. 刷新权限

```
flush privileges
```

#### 下载第三方依赖包（三个）

```
yum install -y chkconfig python bind-utils psmisc libxslt zlib sqlite cyrus-sasl-plain cyrus-sasl-gssapi fuse fuse-libs redhat-lsb
```

#### 安装Cloudera Manager Server、Agent

1. 创建文件夹

```
mkdir /opt/cloudera-manager
```

2. 上传文件到node01的/software （已完成）

3. 解压cloudre

```
tar xvzf cloudera-manager*.tar.gz -C /opt/cloudera-manager
```

4. 配置CM Agent

```
vim /opt/cloudera-manager/cm-5.4.3/etc/cloudera-scm-agent/config.ini
```

```
# 修改为
server_host=cdh-node01
```

5. 三节点创建用户(三个)

```
useradd --system --no-create-home --shell=/bin/false --comment "Cloudera SCM User" cloudera-scm
```

6. 创建Parcel目录

```
# node01
mkdir -p /opt/cloudera/parcel-repo
chown cloudera-scm:cloudera-scm /opt/cloudera/parcel-repo

# 都要做
mkdir -p /opt/cloudera/parcels
chown cloudera-scm:cloudera-scm /opt/cloudera/parcels
```

7. 配置CM Server数据库

```
# 复制文件
cd /usr/share/java/
mv /software/mysql-connector-java-5.1.26-bin.jar ./

# 修改文件名
mv mysql-connector-java-5.1.26-bin.jar mysql-connector-java.jar
```

8. 进入mysql

```
# 密码123
grant all on *.* to 'temp'@'%' identified by 'temp' with grant option;
```

