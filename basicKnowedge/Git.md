# Git学习

## 1.版本控制

**版本控制**（Revision Control）是一种在开发过程中用于管理我们对文件、目录或工程内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。

- 实现跨区域多人协同开发
- 追踪和记载一个或多个文件的历史记录
- 组织和保护你的源代码和文档
- 统计工作量
- 并行开发、提高开发效率
- 跟踪记录整个软件的开发过程
- 减轻开发人员的负担，节省时间同时降低人为错误

> 多人开发必须使用版本控制！

主流的版本控制器有如下这些：

- **Git**
- **SVN**（Subversion）
- **CVS**（Conrcurrent Versions System）
- **VSS**（Microsoft Visual SourceSafe)
- **Visual Studio Online**

版本控制分类：

1. 本地版本控制：记录文件每次更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人使用，如RCS。
2. 集中版本控制：所有版本数据都保存在服务器上，协同开发者从服务器上同步更新或上传自己的修改。用户本地只有自己以前所同步的版本，如果不联网的话用户就看不到历史版本，也无法切换版本，或在不同分支工作。但所有数据都保存在单一服务器上，有很大风险这个服务器会损坏，这样就会丢失所有的数据，当然可以定期备份。代表产品有SVN、CVS、VSS。
3. 分布式版本控制：所有版本信息仓库全部同步到本地的每个用户，这样就可以在本地查看所有版本历史，可以离线在本地提交，只需要联网时push到相应的服务器或其他用户即可。由于每一个用户保存的都是所有的版本数据，只要一个用户的设备没有问题就可以恢复到所有的数据，但这增加了本地存储空间的占用。不会因为服务器损坏或者网络问题，造成不能工作的情况！代表产品：Git。

> **Git和SVN最主要的区别：**
>
> SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而工作时使用的都是自己的电脑，所以要首先从中央服务器上得到最新的版本，然后工作，完成工作后，再将自己完成的代码推送到中央服务器。集中式版本控制系统是必须联网才能工作，对网络带宽要求较高。
>
> Git是分布式版本控制系统，没有中央服务器，每个人的电脑就是一个完整的版本库，工作的时候无需联网，因为版本都在自己的电脑上。协同的方法是这样的：一个人在自己的电脑上修改了文件A，另一个人也修改了文件A，这时2个人只需要把自己的修改推送给对方就可以互相看到自己的修改了。Git可以直接看到更新了哪些代码。
>
> Git是目前世界上最先进的分布式版本控制系统。

## 2.安装配置

官网下载一路next

![liunx基本命令](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/01.jpg)

- 相关配置文件本地路径

    ```path
    D:\DevTools\Git\etc\gitconfig
    C:\Users\王林清\.gitconfig
    ```

- 设置邮箱和用户名(必要)

    ```bash
    git config --global user.name "xxx"
    git config --global user.email xxx
    ```
    
- 配置其他

    ```bash
    # 直接写在配置文件里面
    [color]
    	ui = auto
    [core]
    	editor = vim
    [alias]
    	co = checkout
    	ci = commit
    	st = status
    	br = branch
    	unstage = reset HEAD --
    	last = log -1 HEAD
    ```

    

## 3.Git基本原理(重点)

- 工作区域划分：

    - Git有三个工作区域：工作目录(Working Directory)、暂存区(Stage/Index)、资源库(Repository或Git Directory)，如果在算上远程Git仓库(Remote Directory)就可以划分为4个工作区域，文件在这四个区域之间转换关系如下图所示。

        <img src="https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/02.jpg" style="zoom:50%;" />

    - Working Directory/Workspace：工作区，就是你平时存放代码的地方。

    - Stage/Index：暂存区，用于临时存放你的改动，事实上只是一个文件，保存即将提交到文件列表信息

    - History/Repository：仓库区，安全存放数据的位置，这里面有提交到所有版本的数据。其中HEAD指向最新放入仓库的版本。

    - Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

- 工作流程：

    ![](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/04.jpg)

    1. 在工作目录中添加、修改文件。
    2. 将需要进行版本管理的文件放入暂存区域。
    3. 将暂存区域的文件提交到git仓库。

    因此，git管理的文件有三种状态：已修改(modified)、已暂存(staged)、已提交(committed)。

## 4.Git项目创建

- 创建工作目录和常用指令

    工作目录(Workspace)一般就是你希望Git帮你管理的文件夹，可以是你项目的目录，也可以是一个空目录，最好不要有中文。

    ![04](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/03.png)

- 本地仓库搭建：

    1. 创建全新仓库：

        ```bash
        # 在要管理的目录打开Git Bash执行以下命令
        git init
        ```

    2. 克隆远程仓库：

        ```bash
        git clone url
        ```

## 5.Git文件操作

- 文件的4种状态：

    - **Untracked**：未跟踪，此文件在文件夹中，单并没有加入到Git库不参与版本控制，通过`git add`状态变为`staged`。

    - **Unmodified**：文件已入库未修改，即版本库中文件快照内容与文件夹中完全一致，如果被修改状态变为`Modified`，如果使用`git rm`移出版本库则状态变为`Untracked`。

    - **Modified**：文件已修改，没有进行其他操作，可以通过`git add .`进入`staged`状态，也可以使用`git checkout`回退到`Unmodified`状态。

    - **Staged**：暂存状态，执行`git commit`则将修改同步到库中，文件变为`Unmodified`状态；执行`git reset HEAD filename`取消暂存，文件状态变为`Modified`。

        ```bash
        #查看指定文件状态
        git status [filename]
        
        #查看所有文件状态
        git status
        
        #将文件添加到暂存区
        git add [filename]
        
        #将文件添加到本地仓库 -m是commit message
        git commit -m "xxx" [filename]
        
        #将文件上传到远端服务器
        git push [filename]
        ```

- 忽略文件：有时候我们不想要把某些文件纳入版本控制中，比如数据库文件、临时文件、设计文件等，就可以在主目录下建立`.gitignore`文件，此文件如下规则：
    1. 空行或以`#`开头的行将被忽略。
    2. 可以使用Linux通配符。例如：`*`代表任意多个字符，`?`代表一个字符，`[abc]`代表可选字符范围，`{s1,s2}`代表可选字符串。
    3. 如果名称最前面有`!`，表示例外规则，将不被忽略。
    4. 如果名称的最前面是一个`/`，表示要忽略的文件在此目录下，而子目录的文件不忽略。
    5. 如果名称的最后面是一个`/`，表示要忽略的是此目录下该名称的子目录，而非文件。

## 6.Git命令

```bash
# 初始化文件夹
git init <file>

# 查看工作区和仓库文件状况
git status
# 缩减
git status -s

# 将工作区文件添加到暂存区
git add --all  # 或者 git add .
git add <file>

# 提交到本地仓库
git commit -m "msg" <file>
# 或者详细信息
git commit <file>
#第一行：用一行文字简述提交的更改内容
#第二行：空
#第三行以后：记述更改的原因和详细内容

# 查看提交日志
git log
# 缩短版
git log --oneline
git log --stat #统计
git log --pretty=oneline/short/full/fuller
# 查看提交差异
git log -p -限制条数 -- <file>
# 以图的形式展示日志
git log --graph

# 查看工作区和最新提交间的差别
git diff

# 列出分支(有*的是当前分支)
git branch [--list]

# 创建并切换分支
git checkout -b <branch>
#等价于
git branch <branch>
git checkout <branch>

# 切换分支
git checkout <branch>
# 切换回上一个分支
git checkout -

# 合并分支
git merge --no-ff <branch>

# 回溯版本
git reset --hard <hash>

# 查看历史操作
git reflog

# 修改提交信息
git commit --amend

# 回滚工作区修改
git restore <file>

# 添加+提交(对工作区新创建的文件必须要用git add来添加)
git commit -am "msg"

# 修改分支名
git branch -m 旧分支名 新分支名
# 删除本地分支
git branch --delete <branch>

# 删除远程分支
git push --delete origin 旧分支名

# 将新分支名推上去 
git push origin 新分支名

#将新本地分支和远程相连 
git branch --set-upstream-to origin/新分支名

# 查看工作区文件和暂存区文件区别
git diff
# 查看暂存区文件和最后一次提交文件区别
git diff --staged #或者--cached

# 删除文件
git rm <file>
# 只删除暂存区
git rm --cached <file>

# 改名
git mv

# 取消提交
git commit --amend

# 取消暂存
git reset HEAD <file>
#等价于
git unstage <file>

# 将工作区文件回滚到第一次提交时
git co -- <file>

# 连接远程仓库    origin    url简称
git remote add <remote> <shortname> <url>
# 查看连接
git remote -v
# 抓取
git fetch <remote>
# 推送
git push <remote> <branch>
# 初始化推送(第一次)
git push -u <romote> <branch>


```



```bash
# 查看、添加、提交、删除、找回，重置修改文件

git help <command> # 显示command的help

git show # 显示某次提交的内容 git show $id

git co -- <file> # 抛弃工作区修改

git co . # 抛弃工作区修改

git add <file> # 将工作文件修改提交到本地暂存区

git add . # 将所有修改过的工作文件提交暂存区
git add --all #将所有工作区文件提交到暂存区

git rm <file> # 从版本库中删除文件

git rm <file> --cached # 从版本库中删除文件，但不删除文件

git reset <file> # 从暂存区恢复到工作文件

git reset -- . # 从暂存区恢复到工作文件

git reset --hard # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改

git ci <file> git ci . git ci -a # 将git add, git rm和git ci等操作都合并在一起做　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　git ci -am "some comments"

git ci --amend # 修改最后一次提交记录

git revert <$id> # 恢复某次提交的状态，恢复动作本身也创建次提交对象

git revert HEAD # 恢复最后一次提交的状态

# 查看文件diff



#查看提交记录

git log

git log <file> # 查看该文件每次提交记录
git log --oneline # 缩短的历史记录
git log -p <file> # 查看每次详细修改内容的diff

git log -p -2 # 查看最近两次详细修改内容的diff

git log --stat #查看提交统计信息
tig

#Mac上可以使用tig代替diff和log，brew install tig

# Git 本地分支管理
# 查看、切换、创建和删除分支


git br -r # 查看远程分支

git br <new_branch> # 创建新的分支

git br -v # 查看各个分支最后提交信息

git br --merged # 查看已经被合并到当前分支的分支

git br --no-merged # 查看尚未被合并到当前分支的分支

git co <branch> # 切换到某个分支

git co -b <new_branch> # 创建新的分支，并且切换过去

git co -b <new_branch> <branch> # 基于branch创建新的new_branch

git co $id # 把某次历史提交记录checkout出来，但无分支信息，切换到其他分支会自动删除

git co $id -b <new_branch> # 把某次历史提交记录checkout出来，创建成一个分支

git br -d <branch> # 删除某个分支

git br -D <branch> # 强制删除某个分支 (未被合并的分支被删除的时候需要强制)分支合并和reba
git merge <branch> # 将branch分支合并到当前分支

git merge origin/master --no-ff # 不要Fast-Foward合并，这样可以生成merge提交

git rebase master <branch> # 将master rebase到branch，相当于： git co <branch> && git rebase master && git co master && git merge <branch>

# Git补丁管理(方便在多台机器上开发同步时用)
 
git merge <branch> # 将branch分支合并到当前分支
 
git merge origin/master --no-ff # 不要Fast-Foward合并，这样可以生成merge提交

git rebase master <branch> # 将master rebase到branch，相当于： git co <branch> && git rebase master && git co master && git merge <branch>

# Git暂存管理

git stash # 暂存

git stash list # 列所有stash

git stash apply # 恢复暂存的内容

git stash drop # 删除暂存区

# Git远程分支管理

git pull # 抓取远程仓库所有分支更新并合并到本地

git pull --no-ff # 抓取远程仓库所有分支更新并合并到本地，不要快进合并

git fetch origin # 抓取远程仓库更新

git merge origin/master # 将远程主分支合并到本地当前分支

git co --track origin/branch # 跟踪某个远程分支创建相应的本地分支

git co -b <local_branch> origin/<remote_branch> # 基于远程分支创建本地分支，功能同上

git push # push所有分支

git push origin master # 将本地主分支推到远程主分支

git push -u origin master # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)

git push origin <local_branch> # 创建远程分支， origin是远程仓库名

git push origin <local_branch>:<remote_branch> # 创建远程分支

git push origin :<remote_branch> #先删除本地分支(git br -d <branch>)，然后再push删除远程分支

# Git远程仓库管

git remote -v # 查看远程服务器地址和仓库名称

git remote show origin # 查看远程服务器仓库状态

git remote add origin git@ github:robbin/robbin_site.git # 添加远程仓库地址

git remote set-url origin git@ github.com:robbin/robbin_site.git # 设置远程仓库地址(用于修改远程仓库地址) 
git remote rm <repository> # 删除远程仓库

# 创建远程仓库

git clone --bare robbin_site robbin_site.git # 用带版本的项目创建纯版本仓库

scp -r my_project.git git@ git.csdn.net:~ # 将纯仓库上传到服务器上

mkdir robbin_site.git && cd robbin_site.git && git --bare init # 在服务器创建纯仓库

git remote add origin git@ github.com:robbin/robbin_site.git # 设置远程仓库地址

git push -u origin master # 客户端首次提交

git push -u origin develop # 首次将本地develop分支提交到远程develop分支，并且track

git remote set-head origin master # 设置远程仓库的HEAD指向master分支也可以命令设置跟踪远程库和本地库

git branch --set-upstream master origin/master

git branch --set-upstream develop origin/develop
```

## 7.Git常见错误

1. 代理问题：

    ```bash
    fatal: unable to access 'https://github.com/.../.git': Could not resolve host: github.com
    
    # 解决方法：在工程目录下执行以下语句
    git config --global http.proxy
    git config --global --unset http.proxy
    ```

2. http缓存问题：

    ```bash
    git error: RPC failed； result=35, HTTP code = 0 fatal: The remote end hung up unexpectedly
    
    # 解决方法：在工程目录下执行以下语句
    git config --global http.postBuffer 20M
    ```

    

