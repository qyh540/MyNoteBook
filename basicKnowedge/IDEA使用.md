# IDEA使用

## 一、下载安装

>   [官网下载](https://www.jetbrains.com/idea/)

-   选择旗舰版下载exe文件，学生可以凭借学生邮箱免费用。

>   下载toolbox后用toolbox下载(推荐)
>
>   [JetBrains Toolbox App：轻松管理您的工具](https://www.jetbrains.com/zh-cn/toolbox-app/)

-   toolbox可以管理所有jetbrains旗下的所有ide工具及使用这些ide所创建的项目。

-   安装后推荐改一下配置：

    ![image-20210818161720006](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210818161720006.png)

    ![image-20210818161621021](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210818161621021.png)

如果用户名是中文建议使用以上安装目录，并更改安装目录下的`.vmoptions`文件，添加`-Duser.home=xxx`

## 二、初级设置

1.  字体设置

    >   系统字体：
    >
    >   File | Settings | Appearance & Behavior | Appearance > use custom font
    >
    >   
    >
    >   代码字体：
    >
    >   File | Settings | Editor | Font > font
    >
    >   
    >
    >
    >   鼠标滚轮缩放字体：
    >
    >   File | Settings | Editor | General > change font size with ctrl + mouse wheel

2.  外观设置

    >面包屑：推荐开启
    >
    >File | Settings | Editor | General | Breadcrumbs
    >
    >
    >
    >
    >多行文件标签栏：推荐开启
    >
    >File | Settings | Editor | General | Editor Tabs > show tabs in one row (取消勾)
    >
    >
    >
    >背景图片设置：
    >
    >File | Settings | Appearance & Behavior | Appearance > Background image
    >
    >
    >
    >代码每行长度限制：java推荐120
    >
    >File | Settings | Editor | Code Style > hard wrap at
    >
    >
    >
    >显示空格：
    >
    >File | Settings | Editor | General | Appearance > show whitespaces(选择leading：行首)
    >
    >
    >
    >方法分割线：
    >
    >File | Settings | Editor | General | Appearance > Show method separators

3.  编码设置

    >   File | Settings | Editor | File Encodings 全部改为UTF-8
    >
    >
    >   File | Settings | Editor | General | Console > default encoding 改为utf-8

4.  其他设置

    >   项目目录：
    >
    >   File | Settings | Appearance & Behavior | System Settings > default project directory

## 三、常用插件

1.  `One dark theme`：主题插件
2.  `translation`：翻译插件
3.  `statistic`：代码统计插件
4.  `Key Promoter X`：快捷键提示
5.  `Ace Jump`：代码跳转，使用`ctrl + ;`进行跳转
6.  `Grep Console`：控制台过滤
7.  `CamelCase`：命名转换(`shift + alt + u`大小驼峰，)
8.  `CodeGlance`：代码概览
9.  `Markdown Editor`：md文件编辑器
10.  `Quick file preview`：单击预览文件
11.  `Save Action`：自动修改代码

>   java专用
>
>   1.  codota：智能补全
>   2.  JunitGenerator：junit单元测试
>   3.  easycode：自动生成实体类
>   4.  Alibaba Java Coding Guidelines：阿里巴巴java开发手册，规范代码
>   5.  JRebel and XRebel for IntelliJ：热布署(团队url：https://jrebel.qekang.com/c09763aa-c43f-448c-9ce7-29460b05fffb)

## 四、高级设置

1.  **==live templates(代码模板)==**
2.  ==**file and code templates(文件模板)**==
3.  

## 五、常用快捷键

>   **1. 常用**
>
>   1.Ctrl＋E，可以显示最近编辑的文件列表
>
>   2.Shift＋Click可以关闭文件
>
>   3.Ctrl＋[或]可以跳到大括号的开头结尾
>
>   4.Ctrl＋Shift＋Backspace可以跳转到上次编辑的地方
>
>   5.Ctrl＋F12，可以显示当前文件的结构
>
>   6.Ctrl＋F7可以查询当前元素在当前文件中的引用，然后按F3可以选择
>
>   7.Ctrl＋N，可以快速打开类
>
>   8.Ctrl＋Shift＋N，可以快速打开文件
>
>   9.Alt＋Q可以看到当前方法的声明
>
>   10.Ctrl＋W可以选择单词继而语句继而行继而函数
>
>   11.Alt＋F1可以将正在编辑的元素在各个面板中定位
>
>   12.Ctrl＋P，可以显示参数信息
>
>   13.Ctrl＋Shift＋Insert可以选择剪贴板内容并插入
>
>   14.Alt＋Insert可以生成构造器/Getter/Setter等
>
>   15.Ctrl＋Alt＋V 可以引入变量。例如把括号内的SQL赋成一个变量
>
>   16.Ctrl＋Alt＋T可以把代码包在一块内，例如try/catch
>
>   17.Alt＋Up and Alt＋Down可在方法间快速移动
>
>   **2. 查找**
>
>   CTRL+N  查找类 
>   CTRL+SHIFT+N 查找文件 
>   CTRL+SHIFT+ALT+N 查找类中的方法或变量 
>   CIRL+B  找变量的来源 
>   CTRL+ALT+B 找所有的子类 
>   CTRL+SHIFT+B 找变量的类 
>   CTRL+G  定位行 
>   CTRL+F  在当前窗口查找文本 
>   CTRL+SHIFT+F 在指定窗口查找文本 
>   CTRL+R  在 当前窗口替换文本 
>   CTRL+SHIFT+R 在指定窗口替换文本 
>   ALT+SHIFT+C 查找修改的文件 
>   CTRL+E  最近打开的文件 
>   F3  向下查找关键字出现位置 
>   SHIFT+F3 向上一个关键字出现位置 
>   F4  查找变量来源 
>   CTRL+ALT+F7 选中的字符查找工程出现的地方 
>   CTRL+SHIFT+O 弹出显示查找内容
>
>   **3. 自动代码**
>
>   ALT+回车 导入包,自动修正 
>   CTRL+ALT+L 格式化代码 
>   CTRL+ALT+I 自动缩进 
>   CTRL+ALT+O 优化导入的类和包 
>   ALT+INSERT 生成代码(如GET,SET方法,构造函数等) 
>   CTRL+E 最近更改的代码 
>   CTRL+SHIFT+SPACE 自动补全代码 
>   CTRL+空格 代码提示 
>   CTRL+ALT+SPACE 类名或接口名提示 
>   CTRL+P  方法参数提示 
>   CTRL+J  自动代码 
>   CTRL+ALT+T 把选中的代码放在 TRY{} IF{} ELSE{} 里
>
>   **4. 复制快捷方式**
>
>   CTRL+D  复制行 
>   CTRL+X  剪切,删除行  
>
>   **5. 其他快捷方式**
>
>   CIRL+U  大小写切换 
>   CTRL+Z  倒退 
>   CTRL+SHIFT+Z 向前 
>   CTRL+ALT+F12 资源管理器打开文件夹 
>   ALT+F1  查找文件所在目录位置 
>   SHIFT+ALT+INSERT 竖编辑模式 
>   CTRL+/  注释//  
>   CTRL+SHIFT+/ 注释/*...*/ 
>   CTRL+W  选中代码，连续按会有其他效果 
>   CTRL+B  快速打开光标处的类或方法 
>   ALT+ ←/→ 切换代码视图 
>   CTRL+ALT ←/→ 返回上次编辑的位置 
>   ALT+ ↑/↓ 在方法间快速移动定位 
>   SHIFT+F6 重构-重命名 
>   CTRL+H  显示类结构图 
>   CTRL+Q  显示注释文档 
>   ALT+1  快速打开或隐藏工程面板 
>   CTRL+SHIFT+UP/DOWN 代码向上/下移动。 
>   CTRL+UP/DOWN 光标跳转到第一行或最后一行下 
>   ESC  光标返回编辑框 
>   SHIFT+ESC 光标返回编辑框,关闭无用的窗口 
>   F1  帮助千万别按,很卡! 
>   CTRL+F4  非常重要下班都用

![](https://img.jbzj.com/file_images/article/201412/2014121711113294_jb51.png)

