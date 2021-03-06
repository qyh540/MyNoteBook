# linux服务器配置

##  一、基础配置

#### 1. 用户配置

1. 创建用户

```bash
adduser zhu521
```

2. 设置密码

```bash
passwd zhu521
```

3. 授权

    1. 查看 sudoers 位置

        ```bash
        whereis sudoers
        ```

    2. 增减写权限

        ```bash
        chmod -v u+w /etc/sudoers
        ```

    3. 添加用户

        ```
        zhu521	ALL=(ALL)	ALL
        ```

    4. 收回权限

        ```bash
        chmod -v u-w /etc/sudoers
        ```

4. 切换为创建的用户

    ```bash
    su zhu521
    # 第一次切换会有提示
    ```

#### 2. 免密登录

1. WSL本地生成公私钥

```bash
ssh-keygen
```

2. 将公钥发送到远程服务器

```bash
ssh-copy-id  -i ~/.ssh/id_rsa.pub <user>@<ip>
```

3. 配置别名

```bash
vim ~/.ssh/config
```

添加以下内容

```tex
Host <name>
	HostName <ip>
    User <user>
    Port <port>
	IdentityFile ~/.ssh/id_rsa
```

然后就可以使用 <code>ssh <name></code> 登录远程服务器。

4.  补充

    -   设置长时间未操作不断连

    ```bash
    #编辑sshd配置
    sudo vim /etc/ssh/sshd_config
    
    #取消ClientAliveInterval和ClientAliveCountMax的注释，修改其值为:
    ClientAliveInterval 90    #每过多少秒给SSH客户端发送消息90s
    ClientAliveCountMax 86400  #超过多少秒无操作后断开连接24h
    
    #保存退出，重启sshd服务
    sudo systemctl restart sshd
    
    #编辑本地配置
    vim ~/.ssh/config
    
    #添加
    ServerAliveInterval 90
    
    #退出保存，重启服务(wsl)
    sudo /etc/init.d/ssh restart
    ```
    
    -   参考：[(35 阿里云ECS服务器ssh一会儿就自动断开连接解决方案_liutao43的博客-CSDN博客](https://blog.csdn.net/liutao43/article/details/111060281)

## 二、SHELL配置

#### 1. 安装git

```
sudo yum -y install git
```

#### 2. 安装zsh

1. 安装

```bash
sudo yum update && sudo yum -y install zsh
```

2. 切换默认shell

```bash
# 查看所有shell路径
sudo chsh -l
#切换root shell
# sudo chsh -s /bin/zsh
切换 用户 shell
chsh -s /bin/zsh

# 启动zsh
zsh
```

> 安装完成后第一次启动zsh会有提示，选择 0，只创建.zshrc

#### 3. 安装ohmyzsh

1. 克隆项目

```bash
git clone https://gitee.com/mirrors/oh-my-zsh.git
```

2. 安装

```bash
cd ~/oh-my-zsh/tools
./install.sh
```

> 安装后会在~/生成.ohmyzsh,可以将下载的删除了
>
> 安装完成后会提示切换默认shell，确认后选择只创建默认配置.zshrc，根据需要修改，不懂不要改

在之后说明

#### 4. 安装zsh插件

- **zsh-autosuggestions**
    1. 下载

```bash
git clone https://gitee.com/yantaozhao/zsh-autosuggestions.git
```

   2. 移动到指定目录

```bash
mv ~/zsh-autosuggestions ~/.oh-my-zsh/plugins/
```

- **zsh-syntax-highlighting**
    1. 下载

```bash
git clone https://gitee.com/zhongyuehui/zsh-syntax-highlighting.git
```

   2. 移动

```bash
mv ~/zsh-syntax-highlighting ~/.oh-my-zsh/plugins/
```

- **autojump**
    1. 下载

```bash
git clone git://github.com/wting/autojump.git
```

   2. 安装

```bash
cd autojump
./install.py
```

​	3. 根据安装完成提示，将最后的几行添加到 .zshrc 末尾。

- **tmux**

```bash
sudo yum -y install tmux
```

- **添加 .zshrc 配置**
    1. 安装完上述三个插件后都要添加配置，否则不起作用。找到 .zshrc 中的 plugins添加以下内容

```txt
plugin = (
	zsh-autosuggestions
	zsh-syntax-highlighting
	autojump
	# 根据需要添加以下插件
	# 这些是自带的，无需下载
	tmux
	python
	brew
)
```

#### 5. 安装vim插件

1. Vundle

下载Vundle包

```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

把以下内容写到在 ~/.vimrc 开头

```vimrc
filetype off                  " required

" set the runtime path to include Vundle and initialize
" 需要修改 Vundle 的路径"
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" 在这里添加其他插件

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
func SetTitle()
call setline(1, "\#!/usr/bin/python")
call setline(2, "\# -*- coding=utf8 -*-")
call setline(3, "\"\"\"")
call setline(4, "\# @Author : Wlq")
call setline(5, "\# @Created Time : ".strftime("%Y-%m-%d %H:%M:%S"))
call setline(6, "\# @Description : ")
call setline(7, "\"\"\"")
normal G
normal o
normal o
endfunc
autocmd bufnewfile *.py call SetTitle()
```

2.  使用其他配置

```bash
git clone https://github.com/youngyangyang04/PowerVim.git
cd PowerVim
sh install.sh
```



## 三、环境配置

#### 1. 安装jdk

1. 下载jdk

> https://www.oracle.com/java/technologies/javase-downloads.html

2. 解压到指定文件夹

```bash
sudo tar -zxvf /software/jdk... -C /opt/java
```

3. 配置环境变量

```bash
sudo vim /etc/profile
```

```tex
# JAVA_HOME
export JAVA_HOME=/opt/java/jdk1.8
export JRE_HOME=$JAVA_HOME/jre
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
```

4. 刷新

```bash
. /etc/profile
# 验证
java -version
javac -version
```

#### 2. 升级python

1. 官网下载python3.8安装包：[Python Release Python 3.8.11 | Python.org](https://www.python.org/downloads/release/python-3811/)

2. 上传到服务器软件目录，解压

    ```bash
    sudo tar -zxvf Python-3.8.11.tgz
    ```

3. 创建文件夹并授权

    ```bash
    sudo mkdir /usr/local/python38
    sudo chmod 777 /usr/local/python38
    ```

4. 安装必要依赖

    ```bash
    #安装C/C++环境
    sudo yum install gcc-c++
    #安装必要库
    sudo yum -y install zlib zlib-devel
    sudo yum libffi-devel -y
    ```

5. 进入解压目录，编译安装

    ```bash
    cd ./Python-3.8.11
    ./configure --enable-optimizations --prefix=/usr/local/python38 && make && make install
    ```

6. 将之前的备份后解除链接

    ```bash
    # 也可以选择链接python3即
    # sudo cp /usr/bin/python3 /usr/bin/python3.bak
    # sudo unlink /usr/bin/python3
    sudo cp /usr/bin/python /usr/bin/python2.bak
    sudo unlink /usr/bin/python
    ```

7. 将python38链接到python

    ```bash
    # 如果链接python3的话就是
    # sudo ln -s /usr/local/python38/bin/python3.8 /usr/bin/python3
    sudo ln -s /usr/local/python38/bin/python3.8 /usr/bin/python
    ```

8. 测试

    ```bash
    # 输入python 回车
    python 
    # 输出以下内容则成功
    Python 3.8.11 (default, Jul 22 2021, 17:48:09)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>>
    ```

9.其他

- 由于yum使用的是系统自带的python解释器(我的是python2.7)如果将python版本变为3.8可能会在使用yum的时候报错，所以可以选择链接python3或是修改yum配置文件。

    ```bash
    # 修改下列文件首行 #!/usr/bin/python 为 #!/usr/bin/python2.7
    sudo vim /usr/bin/yum
    sudo vim /usr/libexec/urlgrabber-ext-down
    ```

- 参考：[linux 更新python3.8_氷泠-CSDN博客_linux python3.8](https://blog.csdn.net/qq_27525611/article/details/104627328)

## 四、常用软件

#### 1. 安装tomcat

1. 下载

> https://tomcat.apache.org/download-80.cgi

选择 core 中的.tar.gz文件

2. 解压并改名

```bash
sudo tar -zxvf /software/apache-... -C /opt/tomcat/
sudo mv /opt/tomcat/apache-tomcat-8.5.69 /opt/tomcat/tomcat8
```

3. 配置环境

```bash
sudo vim /etc/profile
```

```tex
# TOMCAT_HOME
export TOMCAT_HOME=/opt/tomcat/tomcat
```

4. 创建启动tomcat的用户

> root 启动tomcat 会有危险

```bash
sudo useradd -M -s /sbin/nologin tomcat
# -M 不创建home dir
# -s 用户使用的shell
# /sbin/nologin 不允许登录
```

5. 修改权限

```bash
sudo chown -R tomcat:tomcat /opt/tomcat/
```

6. 设置service

```bash
sudo vim /etc/systemd/system/tomcat.service
```

```tex
# Systemd unit file for tomcat
[Unit]
Description=Apache Tomcat Web Application Container
After=syslog.target network.target

[Service]
Type=forking

Environment=JAVA_HOME=/opt/java/java
Environment=CATALINA_PID=/opt/tomcat/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat/tomcat
Environment=CATALINA_BASE=/opt/tomcat/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djdk.tls.client.protocols="TLSv1.2" -Dsun.security.ssl.allowUnsafeRenegotiation=false -Dhttps.protocols="TLSv1.2"'
ExecStart=/opt/tomcat/tomcat/bin/startup.sh
ExecStop=/bin/kill -15 $MAINPID

User=tomcat
Group=tomcat

[Install]
WantedBy=multi-user.target
```

> 重要 修改各环境的路径

7. 建立 tomcat java 连接

```bash
cd /opt/java
sudo ln -s jdk1.8 java

cd /opt/tomcat
sudo ln -s tomcat8 tomcat
```

> 如果想取消连接
>
> sudo unlink tomcat
>
> sudo unlink java

8. 修改 logs 存放位置

```bash
sudo mkdir /var/log/tomcat8
sudo rm -rf /opt/tomcat/tomcat8/logs
cd /opt/tomcat/tomcat8
sudo ln -s /var/log/tomcat8 logs
```

> 需要修改logs的权限，否则程序没有权限创建写入文件
>
> sudo chmod a+rwx -R logs

9. 启动tomcat

```bash
# 因为添加了 tomcat8.service, 所以重新加载
sudo systemctl daemon-reload
# 启动
sudo systemctl start tomcat

# 停止
sudo systemctl stop tomcat
# 重启
sudo systemctl restart tomcat
# 查看状态信息
sudo systemctl status tomcat -l
# 设置开机启动
sudo systemctl enable tomcat
```

10. 其他
    - 后续更新：将tomcat8与tomcat的链接断开链接新的目录然后重新做第八步第九步。
    - 参考：[Linux 笔记 #04# Installing Tomcat 8 on Debian - xkfx - 博客园 (cnblogs.com)](https://www.cnblogs.com/xkxf/p/8460019.html)

> 如果输入 ip:8080 没有看到tomcat欢迎页，可能是安全组没有打开8080端口或者防火墙没有开放8080端口。
>
> 如果启动失败，可能是8080端口被占用
>
> netstat -tunp | grep 8080 # 查看 8080 端口的程序
>
> kill -9 pid # 杀死程序

#### 2. 安装MySQL

CentOS-7默认没有mysql的yum源，需要添加mysql源到yum

```bash
# 查看是否有mysql源
sudo yum --disablerepo=\* --enablerepo='mysql*-community*' list available
```

> 按照官方文档添加的源非常慢，这里使用清华的镜像

```bash
# 创建文件，添加镜像连接
sudo vim /etc/yum.repos.d/mysql-community.repo
```

> 根据版本选择 下面是centos7.8的
>
> https://mirrors.cnnic.cn/help/mysql/

```bash
[mysql-connectors-community]
name=MySQL Connectors Community
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql-connectors-community-el7-$basearch/
enabled=1
gpgcheck=1
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql

[mysql-tools-community]
name=MySQL Tools Community
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql-tools-community-el7-$basearch/
enabled=1
gpgcheck=1
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql

[mysql-5.6-community]
name=MySQL 5.6 Community Server
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql-5.6-community-el7-$basearch/
enabled=0
gpgcheck=1
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql

[mysql-5.7-community]
name=MySQL 5.7 Community Server
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql-5.7-community-el7-$basearch/
enabled=1#1为启用
gpgcheck=1
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql

[mysql-8.0-community]
name=MySQL 8.0 Community Server
baseurl=https://mirrors.tuna.tsinghua.edu.cn/mysql/yum/mysql-8.0-community-el7-$basearch/
enabled=0#若安装5.7，将此改为0
gpgcheck=1
gpgkey=https://repo.mysql.com/RPM-GPG-KEY-mysql
```

```bash
# 安装
sudo yum -y install mysql-community-server

# 修改配置文件
sudo vim /etc/my.cnf

# 在[mysqld]下加上：
character-set-server = utf8
explicit_defaults_for_timestamp=true

# 重启服务
sudo systemctl restart mysqld

# 查看密码
sudo grep "temporary password" /var/log/mysqld.log

# 使用此密码进入mysql
mysql -uroot -p
# 远程登录
mysql -hhost -uroot -p

# 修改密码
set password = password('xxx');

# 授权远程连接
# 法一
 GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY 'xxx' WITH GRANT OPTION;
 
# 法二
use mysql;
update user set host='%' where user='root' and host='localhost';

# 刷新权限
flush privileges;
```

#### 3. 安装PostgreSQL

1. 下载仓库

    ```bash
    yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    ```

2. 下载软件

    ```shell
    yum install -y postgresql12-server
    ```

3. 初始化

    ```shell
    /usr/pgsql-12/bin/postgresql-12-setup initdb
    ```

4. 开机自启

    ```shell
    systemctl enable postgresql-12
    ```

5. 启动

    ```shell
    systemctl start postgresql-12
    ```

> PostgreSQL版本可选,链接在[官网](https://www.postgresql.org/download/).
>
> [systemctl命令教程](https://linux.cn/article-5926-1.html)

#### 4. 安装MongoDB

- 下载至任意目录(/software)

```shell
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.2.9.tgz
```

- 解压

```shell
tar -zxvf mongodb-linux-x86_64-3.2.9.tgz
```

- 移动

```shell
mv mongodb-linux-x86_64-3.2.9.tgz /opt/mongodb/mongodb-3.2.9
```

- 创建数据文件夹、日志文件、配置文件

```shell
mkdir -p /opt/mongodb/mongodb-3.2.9/data
touch /opt/mongodb/mongodb-3.2.9/mongodb.log
touch /opt/mongodb/mongodb-3.2.9/mongodb.conf
```

- 修改配置文件

```shell
vim /opt/mongodb/mongodb-3.2.9/mongodb.conf
#添加以下内容
dbpath=/opt/mongodb/mongodb-3.2.9/data
logpath=/opt/mongodb/mongodb-3.2.9/mongodb.log
logappend = true 
port = 27017 
fork = true 
auth = true
```

- 进入安装目录下bin，启动mongodb

```shell
cd /opt/mongodb/mongodb-3.2.9/bin
#启动
./mongod --config /opt/mongodb/mongodb-3.2.9/mongodb.conf
#关闭
./mongod -shutdown -dbpath=/opt/mongodb/mongodb-3.2.9/data
```

- 开放端口,授权远程连接

```shell
#修改配置文件
vim ~/.bashrc
#最后一行添加
export PATH=$PATH:/opt/mongodb/mongodb-3.2.9/bin
#运行
source ~/.bashrc
#授权远程连接
/sbin/iptables -I INPUT -p tcp --dport 27017 -j ACCEPT
```

2.创建管理员用户

```sql
# 切换数据库
use admin
# 创建管理员用户
db.createUser({ user: "admin", pwd: "xxxxxx", roles: [{ role: "userAdminAnyDatabase", db: "admin" }] })
# 登录授权验证成功返回1
db.auth('admim', 'xxxxxx')
```

> [参考](https://www.cnblogs.com/hanyinglong/p/5704320.html)
>
> mongodb的管理员权限由roles赋予,roles有以下几类:
>
> 1 Database User Roles(数据库用户角色)：read、readWrite
>
> 2 Database Administration Roles(数据库管理角色)：dbAdmin、dbOwner、userAdmin
>
> 3 Culster Administration Roles(管理员组，针对整个系统进行管理)：clusterAdmin、clusterManager、clusterMonitor、hostManager
>
> 4 Backup and Restoration Roles(备份还原角色组)：backup、restore
>
> 5 All-Database Roles(所有数据库角色)：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase
>
> 6 Superuser Roles(超级管理员)：root、(dbOwner、userAdmin、userAdminAnyDatabase这几个角色角色提供了任何数据任何用户的任何权限的能力，拥有这个角色的用户可以在任何数据库上定义它们自己的权限)

#### 5. 安装redis

1.  官网下载[Redis](https://redis.io/)

下载最新的稳定版

![image-20210910134913459](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210910134913459.png)

2.  上传至软件目录
3.  解压

```bash
tar -zxvf redis-6.2.5.tar.gz
```

4.  进入解压后的目录编译(服务器要有gcc环境)

```bash
cd /opt/redis/redis-6.2.5
make
```

5.  安装

```bash
make PREFIX=/opt/redis/redis6.2.5 install
```

6.  创建配置文件目录，并复制配置文件

```bash
sudo mkdir /opt/redis/redis6.2.5/etc/
sudo cp /opt/redis/redis-6.2.5/redis.conf /opt/redis/redis6.2.5/etc/
```

7.  修改配置文件

```bash
sudo vim /opt/redis/redis6.2.5/etc/redis.conf

#修改以下内容
# bind 127.0.0.1 
bind 0.0.0.0 -::1
#修改为0.0.0.0，允许所有ip地址访问，也可以自定义特定IP或网段访问

protected-mode  
#是否开启保护模式，默认开启。要是配置里没有指定bind和密码。开启该参数后，redis只会允许本地进行访问，拒绝外部访问。要是开启了密码 和bind，可以开启。否则最好关闭，设置为no。
port 6379
#redis监听的端口，默认6379

# daemonize no
 daemonize yes
#redis采用的是单进程多线程的模式。当daemonize设置成yes时，代表开启守护进程模式，也就是允许后台运行。在守护进程模式下，redis启动后后台运行，并将进程pid号写入redis.conf选项pidfile配置的文件中。

pidfile /var/run/redis_6379.pid
#守护进程模式下，pid文件的保存位置，保持默认即可。

loglevel notice
#日志级别，默认为notice，保持默认即可

#logfile ""
 logfile /opt/redis/logs/redis.log
#设置redis日志文件，默认没有。自定义位置，注意要手动创建。

databases 16
# 默认值为16，默认数据库为0，数据库范围在0-（database-1）之间


rdbcompression yes
# 存储至本地数据库时（持久化到rdb文件）是否压缩数据，默认为yes

dbfilename dump.rdb
# 本地持久化数据库文件名，默认值为dump.rdb

# dir ./
 dir /opt/redis/redis/data/
#可以理解数据库持久化数据存储的目录，必须指定目录而不是文件，如果自定义需要手动创建该目录。就是存放上面dump.rdp文件的位置，累加文件也放在这里。

# requirepass foobared
 requirepass redis
#要求客户端在处理任何命令时都要验证身份和密码，即redis的密码。默认是没有的，需要开启并设置。
```

7.  创建日志目录和数据目录

```bash
sudo mkdir /opt/redis/redis/data/
sudo mkdir /opt/redis/redis/logs/
sudo touch /opt/redis/redis/logs/redis.log
```

8.  启动

```bash
sudo ./bin/redis-server ./etc/redis.conf 
```

9.  查看运行状态

```bash
#查看端口是否处于监听状态。
# ss -tnl | grep 6379
#查看进程
# ps -ef | grep redis
```

10.  关闭

```bash
redis-cli shutdown
```

11.  配置环境变量

```bash
sudo vim /etc/profile.d/redis_bin.sh

#添加
export PATH=$PATH:/opt/redis/redis/bin\

#运行
source /etc/profile.d/redis_bin.sh
```

12.  配置开机自启

```bash
sudo vim /etc/systemd/system/redis.service
#添加
[Unit]
Description=redis-server
After=network.target
 
[Service]
Type=forking
ExecStart=/opt/redis/redis/bin/redis-server /opt/redis/redis/etc/redis.conf
PrivateTmp=true
 
[Install]
WantedBy=multi-user.target
```

参考：

>   [Centos7编译安装redis - 刘晨](https://www.cnblogs.com/lcxhk/p/15141343.html)

## 五、常用命令

#### 1. 文件互串

-   从linux上下载到本地(win10)

    ```bash
    #使用git bash 执行此命令 
    #win10 路径写作 /c/Users...
    #文件夹 用-r 文件不用
    scp [-r] user_name@ip_address:linux_path local_paht
    ```

-   从linux上下载到本地(wsl)

    ```bash
    scp [-r] user_name@ip_address:linux_path local_paht
    ```

-   从wsl上传到linux

    ```bash
    scp local_path user_name@ip_address:linux_path
    ```

#### 2. 链接操作

-   命令格式：`ln -[参数] [源文件] [链接名]`
-   参数形式：`[-bdfinsvF] [-S backup-suffix] [-V {numbered,existing,simple}]`

-   必要参数：

    -   -b 删除，覆盖以前建立的链接
    -   -d 允许超级用户制作目录的硬链接
    -   -f 强制执行
    -   -i 交互模式，文件存在则提示用户是否覆盖
    -   -n 把符号链接视为一般目录
    -   -s 软链接(符号链接)
    -   -v 显示详细的处理过程

-   选择参数：

    -   -S "-S<字尾备份字符串> "或 "--suffix=<字尾备份字符串>"
    -   -V "-V<备份方式>"或"--version-control=<备份方式>"
    -   --help 显示帮助信息
    -   --version 显示版本信息

-   软链接：

    1.  软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式

    2.  软链接可以 跨文件系统 ，硬链接不可以

    3.  软链接可以对一个不存在的文件名进行链接

    4.  软链接可以对目录进行链接

-   硬链接：

    1.  硬链接，以文件副本的形式存在。但不占用实际空间。

    2.  不允许给目录创建硬链接

    3. 硬链接只有在同一个文件系统中才能创建

-  解除链接：`unlink [链接名]`

#### 3. tar 压缩、解压

-   命令格式：`tar [-ABcdgGhiklmMoOpPrRsStuUvwWxzZ][-b <区块数目>][-C <目的目录>][-f <备份文件>][-F <Script文件>][-K <文件>][-L <媒体容量>][-N <日期时间>][-T <范本文件>][-V <卷册名称>][-X <范本文件>][-<设备编号><存储密度>][--after-date=<日期时间>][--atime-preserve][--backuup=<备份方式>][--checkpoint][--concatenate][--confirmation][--delete][--exclude=<范本样式>][--force-local][--group=<群组名称>][--help][--ignore-failed-read][--new-volume-script=<Script文件>][--newer-mtime][--no-recursion][--null][--numeric-owner][--owner=<用户名称>][--posix][--erve][--preserve-order][--preserve-permissions][--record-size=<区块数目>][--recursive-unlink][--remove-files][--rsh-command=<执行指令>][--same-owner][--suffix=<备份字尾字符串>][--totals][--use-compress-program=<执行指令>][--version][--volno-file=<编号文件>][文件或目录...]`
-   主要用法：

```bash
# 解压
tar -zxvf [filename]
# 压缩
tar -zcvf [filename] 待压缩文件
# 排除目录中的某些文件，然后进行压缩。
tar --exclude=目录名/* 或者 文件名 -zcvf 备份文件名.tgz 目录名
```

-   其他：[Linux tar 命令 | 菜鸟教程](https://www.runoob.com/linux/linux-comm-tar.html)

#### 4. systemctl系统控制

[Systemd 入门教程：命令篇 - 阮一峰的网络日志 - http://www.ruanyifeng.com/](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)

