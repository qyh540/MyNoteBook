# C++

## 第一章

## 第二章 开始学习C++

**名称空间**:为了避免不同库中同名函数间的冲突使用名称空间指定函数.

```cpp
//using编译指令 使用头文件iostream中的内容
using namespace std;
//为了不冲突可以指定想要的函数
using std::cout;
using std::cin;
using std::endl;
```

换行符:endl or "\n"

赋值: c和cpp可以连续赋值,如 `int b, c, a = b= c = 88;`,顺序从右到左.

#### CLion创建子项目教程:

1. 在父项目中创建子项目文件夹并 `make directory as` 为 `project source and header`

2. 在子项目文件夹下新建`CMakeList.txt`文件并添加:

    ```cmake
    # 反馈给父项目文件夹内容
    include_directories(.)
    ```

3. 在父项目中的`CMakeList.txt`添加:

    ```cmake
    ADD_SUBDIRECTORY('子项目文件名')
    ```

[教程链接](https://blog.csdn.net/weixin_40040107/article/details/108167589)



#### CLion项目使用多个main函数教程

##### 法一:重定义main (不推荐)

- 要用的时候使用`#define xxx main`,不用之后改成`#define xxx xxx`

- 优点：不需要修改配置文件

- 缺点：会让源码文件中多出一些奇奇怪怪的代码，降低代码可阅读性！

##### 法二:手动添加路径 (main函数少时可用)

- 在`CMakeLists.txt`文件中手动添加:

    ```cmake
    add_executable(文件名 路径)
    ```

- 优点：只修改配置文件，不会影响源码的可读性

- 缺点：每新建一个文件，就得修改配置文件，较为繁琐！

##### 法三:自动遍历 (推荐)

- 基础版:遍历文件根目录下的main函数

    ```cmake
    # 遍历项目根目录下所有的 .cpp 文件
    file (GLOB files *.cpp)
    foreach (file ${files})
    string(REGEX REPLACE ".+/(.+)\\..*" "\\1" exe ${file})
    add_executable (${exe} ${file})
    message (\ \ \ \ --\ src/${exe}.cpp\ will\ be\ compiled\ to\ bin/${exe})
    endforeach ()
    ```

- 进阶版:遍历项目根目录及二级目录下的main函数

    ```cmake
    # 遍历项目根目录及二级目录下所有的 .cpp 文件
    file (GLOB files *.cpp */*cpp)
    foreach (file ${files})
    string(REGEX REPLACE ".+/(.+)\\..*" "\\1" exe ${file})
    add_executable (${exe} ${file})
    message (\ \ \ \ --\ src/${exe}.cpp\ will\ be\ compiled\ to\ bin/${exe})
    endforeach ()
    ```

- 最优版:遍历工程文件根目录下的所有文件目录的main函数

    ```cmake
    # 遍历项目根目录下所有的 .cpp 文件
    file (GLOB_RECURSE files *.cpp)
    foreach (file ${files})
    string(REGEX REPLACE ".+/(.+)\\..*" "\\1" exe ${file})
    add_executable (${exe} ${file})
    message (\ \ \ \ --\ src/${exe}.cpp\ will\ be\ compiled\ to\ bin/${exe})
    endforeach ()
    ```

- 优点：方便省时

- 缺点：这种方法要求所有cpp文件命名不重复，不能含有中文，不能含有‘/’等字符！因为它就是直接Copy你的源码文件名的。

参考链接:[使用CLion 刷题解决多个main函数问题的终极方法_Kim修炼日记-CSDN博客](https://blog.csdn.net/weixin_43316691/article/details/106932999?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_title-0&spm=1001.2101.3001.4242)

## 第三章 处理数据

### 3.2 const限定符

- 通过const限定符声明常量,比通过`#define`声明常量更好.

- 常量一旦赋值就不可更改.

- 常量变量名首字母应该大写.

- 创建常量通用格式:

    ```c++
    const type name = value;
    ```

    

### 3.3 浮点数

- 输出浮点数: 

```c++
// 通常cout会截断float/double结尾的0,通过setf属性覆盖此行为.
cout.setf(ios_base::fixed, ios_base::floatfield);
```

### 3.4 C++算术运算符

- 类型转换
    - C++自动执行类型转换的情况:
    
        - 将一种算术类型的值赋给另一种算术类型的变量时.
        - 表达式中包含不同类型时.
        - 将参数传递给函数时.
    
    - 具体规则:
        1. 初始化和赋值进行的转化
        
        2. 以`{}`方式初始化时进行的转换:c++ 11 将使用大括号的初始化称为列表初始化,因为这种初始化常用于给复杂的数据类型提供值列表,对类型转换的要求更严格.列表初始化不允许缩窄.
        
        3. 表达式中的转换:短数据在表达式运算时会进行整型提升,如short, bool, char会被转换为int进行运算.
        
        4. 传递参数时的转换:
        
        5. 强制类型转换：
        
            ```c++
            (typeName) value;	// c风格
            typeName (value);	// c++风格
            static_cast<typeName> (value);	//强制类型转换符
            ```

## 第四章 复合类型

### 4.1 数组

- 数组初始化规则：
    - 只有在定义数组时才能初始化数组。
    - 不能将一个数组赋给另一个数组。
    - 初始化数组时提供的值可以少于数组的元素数目。
    - 如果只对数组的一部分进行初始化，则编译器将把其他部份置为0。

- 数组初始化方法
    - 初始化数组时可以省略等号。
    - 可不再大括号内包含任何东西，相当于将所用元素置0。
    - 列表初始化禁制缩窄转换。

## 4.2 字符串

- C-style string:以`\0`空符结尾的char型数组。
    - C++ 11 不允许 `char*`给数组初始化。

### 4.4 结构体

- 再利用结构体声明变量时无需使用struct关键词。

- 可以在成员变量后添加字位符来限制空间。

- 可以使用匿名结构体，必须在定义末位声明变量。

    ```c++
    //
    // fileName: test in Ch04
    // C++ 11 with CLion
    // created by 王林清 on 2021/7/18 17:32
    //
    #include <bits/stdc++.h>
    
    using namespace std;
    
    const int Size = 20;
    struct Stu {
        bool sex: 1; // true为男，false为女
        long long id;
        char name[Size];
    } s[Size];
    
    int main() {
        for (int i = 0; i < Size; ++i) {
            s[i].sex = i % 2;
            s[i].id = i * 1000 + i;
            cin >> s[i].name;
        }
        for (Stu j : s) {
            cout << "name = " << j.name << endl;
            cout << "sex = " << j.sex << endl;
            cout << "id = " << j.id << endl;
        }
        return 0;
    }
    ```

### 4.5 共用体

```cpp
//
// fileName: union in Ch04
// C++ 11 with CLion
// created by 王林清 on 2021/7/17 21:29
//
#include <bits/stdc++.h>

using namespace std;

const int Size = 20;

struct stu {
    union he{
        int id;
        string s1;
//        char id_str[Size];
    };
    char name[Size];
    bool sex: 1;
} s[Size];

int main() {
    for (int i = 0; i < Size; ++i) {
        s[i].sex = i % 2;
        if (s[i].sex) {
            s[i].id = i * 1000 + i;
        } else {
            cout << "please input the id: " << endl;
            cin >> s[i].id_str;
        }
        cout << "please input the name: " << endl;
        cin >> s[i].name;
    }

    for (stu j : s) {
        cout << "j.name = " << j.name << endl;
        if (j.sex) {
            cout << "j.id = " << j.id << endl;
        } else {
            cout << "j.id_str = " << j.id_str << endl;
        }
    }
}
```

### 4.6 枚举





