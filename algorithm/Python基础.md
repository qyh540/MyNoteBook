### 1.字符串格式化 format()函数

- 通过关键字

    ```python
    print('{name}喜欢{sports}'.format(name='hhby', sports='慢走'))
    ```

- 通过位置

    - 默认位置

        ```python
        print('1:{}, 2:{}, 3:{}'.format(1, 2, 3))
        ```

    - 指定位置

        ```python
        print('2:{1}, 1:{0}, 3:{2}'.format(1, 2, 3))
        ```

- 填充,居中,对齐

    - ^ 居中对齐

        ```python
        print('{:^30}'.format('hhby'))
        ```

    - < 左对齐; > 右对齐

        ```python
        print('{:<30}'.format('hhby'))
        print('{:>30}'.format('hhby'))
        ```

- 精度控制

    - .nf 保留n位小数

        ```python
        print('{:.3f}'.format(6.6666666))
        ```

    - +给负数加-,正数加+; -给负数加-
    - .%化为百分数形式 .e科学计数法
    - b二进制 d十进制 o八进制 x十六进制 

- Python3.6 新版f-string

    - 样式和format函数一样但可以直接在大括号中写变量

        ```python
        print(f'{1.01*3.77:+.3f}')
        输出:+3.808
        ```

        

### 2.文件

- 文件打开

    - With open()

    ```python
    # 使用with open()不用关闭文件python会自动关闭更加方便安全
    With open('1.txt', 'w') as f:
        content = f.read()
    ```

    - 文件打开模式

        - 'r':只读模式。如果文件不存在，返回异常FileNotFoundError,默认值；
        - 'w':覆盖写模式，文件不存在则创建，存在则完全覆盖；
        - 'x':创建写模式，文件不存在则创建，存在则返回异常FileExistError；
        - 'a':追加写模式，文件不存在则创建，存在则在文件最后追加内容；
        - 'b':二进制文件模式；
        - 't':文本文件模式，默认值；
        - '+':与r/w/x/a一同使用，在原功能的基础上增加同时读写的功能
        
    - 文件读取

        ```python
        with open('1.txt', 'r') as f:
            for lien in f:
                print(line)
        	lines = f.readlines()
        ```

    - 文件写入
    
        ```python
        # 要想写入多行要在每行结尾加上'\n'
        with open(filename, "w") as f:
            f.write("zyssb\n")
            f.write("zyzdssb\n")
        
        with open(filename, 'a') as f:
            f.write(f'{"qyh":*^60s}')
        ```
    
        

### 3.异常

