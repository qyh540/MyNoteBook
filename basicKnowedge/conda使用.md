# Conda使用

### 简介

-   conda默认随miniconda或anaconda发行，因此要安装conda，只需要安装miniconda或anconda即可。

-   一个conda环境就是一个目录包含所有的安装包和依赖，不同环境之间独立且不相互影响。跟python的虚拟环境`virtualenv`一样

-   通常我们可以使用conda来下载和卸载安装包。conda是一种通用包管理系统，可以构建和管理任何语言的任何类型的软件，因此，它也使用于Python包。

    注意：Anaconda中base环境中已经集成安装好了conda和pip，所以可以使用两种方式来安装我们想要的python软件包，安装好了软件包在Scripts目录下可以找到。

-   Anaconda下载的包一般在`Anaconda安装位置\Lib\site-packages`下

-   Anaconda创建的虚拟环境一般在`Anaconda安装位置\envs`下

### 查看信息

```bash
# 查看当前环境安装的包
conda list
conda list -n EnvName  # 查看指定环境安装的包

# 查看有哪些环境
conda info -e
conda env list

# 查看版本
conda --version

# 查看命令
conda -h
```

### 虚拟环境管理

#### 1. 创建与删除

```bash
# 创建虚拟环境
conda create --name EnvName python=x.x
# 创建 anaconda环境(自带绝大部份包)
conda create --name EnvName python=x.x anaconda

# 移除虚拟环境
conda remove --name EnvName --all
```

#### 2. 激活与切换

```bash
# windows上
# 激活
conda activate EnvName
# 切换回基础环境或关闭当前环境
conda deactivate

# Linux、Mac上
# 激活
source activate EnvName
# 切换回基础环境或关闭当前环境
source deactivate EnvName
```

#### 3. 备份与导出

```bash
# 克隆环境
conda create --name newEnv --clone EnvName
 
# 使用Spec List
# 导出配置文件
conda list --explicit > spec-list.txt
# 导入配置文件重现环境
conda create  --name python-course --file spec-list.txt

# 或者使用Environment.yml
# 导出
conda env export > environment.yml
# 导入
conda env create -f environment.yml
```

### 包管理

#### 1. 安装与卸载

```bash
# 安装(默认安装到当前激活环境)
conda install packageName
# -c 指定channel安装
conda install -c conda-forge packageName
# -n 指定安装到哪个环境
conda install -n EnvName packageName

# 卸载
conda uninstall -n envName packageName
conda remove -n envName packageName
```

#### 2. 更新

```bash
# 更新包
conda update -n envNmae packageName

# 更新conda，保持conda最新
conda update conda

# 更新anaconda
conda update anaconda

# 更新Python，更新到当前python最新版本如3.7.XX会更新到python3.7的最新版本
conda update python
```

### 镜像源管理

```bash
# 查看镜像源
conda config --show-sources

# 添加镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

# 设置镜像源
conda config --set show_channel_urls yes
```

### 垃圾清理

```bash
conda clean -p      	#删除没有用的包
conda clean -t      	#tar打包
conda clean -y --all 	#删除所有的安装包及cache
```



