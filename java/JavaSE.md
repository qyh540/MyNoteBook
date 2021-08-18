# JsvaSE

## 第一章	Java入门

##### 1. JDK	JRE	JVM

​	JDK(Java Development Kit) 是Java SE平台所提供的软件工具开发箱.

```java
  /* 
  jdk主要包含的文件夹: 
  bin:最主要的是编译器(javac.exe)
  include:java和JVM交互用的头文件
  lib：类库
  jre:java运行环境
  */
```
​	JRE(Java Runtime Environment)是java运行环境,包含JVM标准实现及Java核心类库.

​	JVM(Java Virtual Machine)是Java虚拟机.

###### 三者联系:

​	JDK>JRE>JVM(JDK包含JRE,JRE包含JVM).

```java
1.三者联系：
JVM不能单独搞定class的执行，解释class的时候JVM需要调用解释所需要的类库lib。在JDK下面的的jre目录里面有两个文件夹bin和lib,在这里可以认为bin里的就是jvm，lib中则是jvm工作所需要的类库，而jvm和 lib和起来就称为jre。JVM+Lib=JRE。总体来说就是，我们利用JDK（调用JAVA API）开发了属于我们自己的JAVA程序后，通过JDK中的编译程序（javac）将我们的文本java文件编译成JAVA字节码，在JRE上运行这些JAVA字节码，JVM解析这些字节码，映射到CPU指令集或OS的系统调用。

2.三者区别：
a.JDK和JRE区别：在bin文件夹下会发现，JDK有javac.exe而JRE里面没有，javac指令是用来将java文件编译成class文件的，这是开发者需要的，而用户（只需要运行的人）是不需要的。JDK还有jar.exe, javadoc.exe等等用于开发的可执行指令文件。这也证实了一个是开发环境，一个是运行环境。
b.JRE和JVM区别：JVM并不代表就可以执行class了，JVM执行.class还需要JRE下的lib类库的支持，尤其是rt.jar。
```

##### 2. javac.exe	javap.exe	java.exe	javaw.exe

- javac.exe是Java的编译器,它可以将.java文件(源文件)编译成.class文件(字节码文件).

- javap.exe是java的反编译器,它可以将.class文件反编译成.java文件.

- java.exe是Java的解释器,它可以启动JVM将.class文件逐行解释成机器指令执行.

- javaw.exe主要用于启动基于GUI(图形用户界面)的应用程序.javaw.exe跟java.exe共同点是都可以执行.class字节码文件，
    但是区别：java.exe是**命令行程序**或**阻塞程序**；javaw.exe是GUI**图形用户界面程序**或**非阻塞程序**。

    ###### 命令行运行Java程序:

    ```c
    ... javac xxx.java
    ... java xxx
    ```

##### 3. 语言特点

- 简单易学
- 面向对象
- 平台无关
- 安全稳定
- 支持多线程
- 提供了大量的库
- java和c++区别:java 是'c++--'
    - 无直接指针操作
    - 自动内存管理(java自动回收内存无需delete)
    - 数据类型长度固定(确保平台无关)
    - 不用头文件(自动检测声明)
    - 不包含结构和联合
    - 不支持宏
    - 不支持多重继承
    - 无类外全局变量
    - 无goto语句

##### 4. 运行机制

- .java文件经过javac编译器编译后变为.class文件(字节码,不是最终指令是虚拟机指令)再经过java运行在JVM上
- JVM规范定义了:
    - 指令集
    - 寄存器集
    - 类文件结构
    - 堆栈
    - 垃圾收集堆
    - 内存区域
- JRE(java运行环境)=JVM + API(Lib) 三项主要功能:
    - 加载代码:由class loader完成
    - 校验代码:由bytecode verifier完成
    - 执行代码:由runtime interpreter完成

- java自动垃圾回收技术(garbage collection,GC)
    - 系统级线程跟踪存储空间分配情况
    - 在JVM空闲时,检查并释放那些可被释放的存储器空间
    - 程序员无需也无法精确控制和干预该回收过程
- JDK(java开发工具包)=JRE + Tools  提供的工具
    - java编译器:javac.exe

    - Java执行器:java.exe

    - 文档生成器:javadoc.exe

        - 形式:/**   */

        - 内容:

            ```java
            /**
             * @author:作者
             * @version:版本
             * @see:说明,主题
             * @param:参数
             * @return:返回说明
             * @exception:异常说明
             */
            ```

    - java打包器:jar.exe

        - 编译:javac xxx.java
        - 打包:jar cvfm xxx.jar xxx.man xxx.class
            - c:create v:verbose(显示详情) f:指定文件名 m:表示清单文件
            - xxx.man:清单文件(manifest)包含Manifest-Version:1.0 , Class-Path:., Main-Class:A.常用名:MANIFEST
        - 运行:java -jar xxx.jar
    
    - java调试器:jdb.exe

##### 5. java内存机制

![](https://img-blog.csdn.net/20170301164516274?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvemhhbmdxaWx1R3J1YmJ5/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

-   JVM运行时数据区分类
    1. JVM栈 (Java Virtual Machine Stacks)
    2. 堆内存 (Heap Memory)
    3. 方法区 (Method Area)
    4. 本地方法栈 (Native Method Stacks)
    5. 程序计数器 (Program Counter (PC) Register)
-   

##### 6. java程序类型

- Application和Applet程序:

    - 结构和运行环境不同
    - 前者是独立程序,需要执行器(调用虚拟机)来运行
    - 后者是嵌在HTML页面中的非独立程序由专门的applerViewer来运行或者由web浏览器(调用java虚拟机)来运行

- Application要点:

    - class是主体
    - public类名与文件同名(一个java文件只能定义一个public class)
    - main()的写法是固定的

- Applet要点:

    - 没有main方法
    - 需要自定义方法
    - 需要在HTML网页中执行实现

    ```注
    Applet技术已经落后,使用得不多了解即可.
    ```

    

## 第二章    基本数据类型与数组

### 2.1 标识符与关键字

#### 2.11 标识符

###### 定义:

- 用来标识类名, 变量名, 方法名, 类型名, 数组名以及文件名的有效字符序列.

###### 命名规则:

- 标识符由字母, 下划线, 美元符号和数字组成,长度不受限制.

- 标识符第一个字符不能是数字字符.
- 标识符不能是关键字.
- 标识符不能是 true, false 和 null.

#### 2.1.2 关键字

###### 定义:

- 具有特定用途或被赋予特定意义的一些单词.

###### 附 Java 关键字:

```java
abstract	assert	boolean	break	byte
case	catch	char	class	const
continue	default	do	double	else
enum	extends	final	finally	float
for	goto	if	implements	import
instanceof	int	interface	long	native
new	package	private	protected	public
return	strictfp	short	static	super
switch	synchronized	this	throw	throws
transient	try	void	volatile	while
```

### 2.2 基本数据类型

基本数据类型也称为简单数据类型(定义即可用).Java 共有8种基本数据类型,可以分为四大类:

- 逻辑类型: boolean.
- 整数类型: byte, short, int, long.
- 字符类型: char.
- 浮点类型: float, double.

#### 2.2.1 逻辑类型

###### 常量: false, true.

#### 2.2.2 整数类型

默认初始值:0

常量:

- 非0数字开头, 如123, 23456为十进制.
- 0开头,如023,077为八进制.
- 0x开头,如0xfff,0x1为16进制.

取值范围:

- int型变量分配4个字节内存,取 -2^31^~2^31^-1.
- byte型变量分配1个字节,取 -2^7^~2^7^-1

- short型变量分配2个字节,取 -2^15^~2^15^-1

- long型变量(通常加后缀L)分配8个字节,取 -2^63^~2^63^-1

#### 2.2.3 字符类型

常量是用半角英文单引号括起的Unicode表中的一个字符,如:

- 'A', '!'.
- '97'(同'a')(char型变量取值范围为:0~65535,为无符号变量且不可以用unsigned修饰).
- 转义字符常量(\)如 '\''表示单引号'\\'表示反斜杠.
- 形如'\uxxxx'的unicode排序位置的十六进制转义,如'\u0041'表示字符A.

#### 2.2.4 浮点类型

##### a. float型 

默认初始值: 0.0 ;

常量(float型常量后必须加f或F后缀):

- 小数表示法: 123.456F, 223.223f
- 指数表示法: 1.3e10f(同1.3 * 10^10^),3e-10f(同3 * 10^10^).

变量:

- float变量在存储float型数据时保留8位有效数字,分配4字节,取值范围为1.4e-45~3.4028235e38 和 -3.4028235e38~-1.4e-45.(注意:不包括0!!!)

##### b. double型

常量(double型可以加后缀d或D,也可省略,其他与float相似)

变量:

- 保留16位有效数字,分配8字节,取值范围为 4.9e-324~1.79...e308 和-1.79...e308~-4.9e-324.

### 2.3 类型转换运算

当把一种基本数据类型变量的值赋给另一种基本类型变量时会涉及到数据转换(不包含逻辑类型).

```java
// Java基本数据类型按精度从低到高排序
byte < short < char < int < long < float < double
```

当把级别低的变量值赋给级别高的变量时,系统自动完成数据类型的转换(自动装箱),如:

```java
float x = 100;
System.out.print(x);
```

输出结果为100.0.

当把高精度类型变量的值赋给级别低的变量时, 必须使用类型转换运算,如:

```java
// 强制转换
int x = (int) 33.123;
long y = (long) 56.999f;
int z = (int) 1235125L;
float q = (float) 33.123;
// 或加上对应后缀
float q = 33.123f;
```

### 2.4 数组

Java中除了基本数据类型还有引用数据类型,其中包括类(class)、接口(interface)和数组。

- 一维数组定义与初始化(分配空间)

    ```java
    // 定义:推荐第一种
    int []a;
    int b[];
    
    // 初始化分为静态和动态初始化,二者不能同时使用
    // 静态初始化:由用户指定数组元素初始值,由系统指定长度
    a = {1, 2, 3,};
    // 动态初始化:由系统指定数组元素初始值,由用户指定长度
    b = new int[3];
    // 可以定义初始化写在一起,Java大括号中可以多一个 ','
    int []c = new int[4];
    int []d = {1,2,3,4,}
    ```

- 数组的引用

    ```java
    // 可以直接用下标
    int []a = {1, 3, 5, 7};
    // 下标从0开始,数组有length属性表示长度
    for (int i = 0; i < a.length; i++) {
    	System.out.print(i); // 输出为:1357
    }
    ```

- 增强for语句(Enhanced for):

    ```java
    int []a = {1, 3, 5, 7};
    // 使用Enhanced for语句遍历数组,只读式遍历(只能访问,不能赋值)
    for (int i : a) {
        System.out.println(i);
    }
    ```

- 数组复制

    - 使用`System.arraycopy()`函数来进行数组复制

    ```java
    // 源数组
    int[] source = {3, 5, 3,};
    // 目的数组
    int[] des = new int[3];
    // 将源数组从下标为0开始的length个元素复制到目标数组下标为0开始的地址
    System.arraycopy(source, 0, des, 0, source.length);
    for (int i : des) {
        System.out.println(i);
    }
    ```

- 多维数组

    ```Java
    // 初始化从高维到低维
    // 和C语言不一样不能int [][3]
    int [][]t = new int[3][]
    ```

    

## 第三章	运算符 表达式和语句

### 3.1 运算符与表达式

#### 3.1.2 自增自减运算符

- ++x:表示先x=x+1再使用x的值
- x++:表示先使用x的值再让x=x+1

#### 3.1.3 算术混合运算的精度

- 如果表达式中有双精度类型(double),则按双精度算.
- 如果表达式中精度最高的类型为单精度浮点数(float),则按单精度算.

- 如果表达式中精度最高的类型是long型整数,则按long精度计算.

- 如果表达式中最高精度低于int整数,则按int精度来计算.

    注:Java允许把不超过byte, short 和 char的取值范围赋给byte, short和char型变量.如果超过了取值范围则会出现损失精度的编译错误.

#### 3.1.5 逻辑运算符和逻辑表达式

- && 逻辑与
- || 逻辑或
- !  逻辑非

#### 3.1.7 位运算符

##### 原码	反码	补码

正数的原码反码补码相同,负数的规则如下:

- 原码: 最高位(符号位)为1,其余位为绝对值的二进制数.
- 反码: 原码的符号位不变,其余位取反.
- 补码: 反码末位+1.

##### &按位与    |按位或    ~按位非    ^按位异或

- &: 双目运算符,c=a&b则对a,b整型数据进行位运算如果a,b的对应位都是1则c的对应位是1,否则是0.
- |: 双目运算符,c=a|b则对a,b整型数据进行位运算如果a,b的对应位都是0则c的对应位是0,否则是1.
- ~: 单目运算符,c=~a则对a的进行位运算,如果a的对应位为1则c的对应位为0,否则为1.
- ^: 双目运算符,c=a^b则对a,b进行位运算,如果a,b对应位数字相同则c的对应位为1,否则为0.

应用:^ 的逆运算 ^, a ^ b ^ b=a, 可以用来加密解密文件

#### 3.1.8 instanceof运算符

对象instanceof类,如果右面的对象是左面的类或子类生成的则返回true,否则返回false

## 面向对象程序设计

- 类和对象概念
    - 类:具有共同属性和行为的对象集合
        - 属性:变量(字段 field)
        - 行为:函数(方法 method)
        - 类和对象的关系:类是对象的抽象(模版),对象是类的实例.
- 三大特性
    - 封装:
        - 模块化:将属性和行为封装在类中,程序中定义很多类
        - 信息隐蔽:将类的细节部分隐藏起来,用户只能通过受保护的接口访问某个类
    - 继承:
        - 父类和子类之间共享数据和方法
        - 好处:
            - 更好地进行抽象与分类
            - 增强代码的重用率
            - 提高可维护性
    - 多态:
        - 不同对象收到同一个消息(调用方法)可以产生完全不同的原则
        - 实现细节由接受对象自行决定
- 思想要点
    - 认为客观世界由各种对象组成
    - 程序的分析与设计都围绕着:
        - 有哪些类
        - 每个类有哪些属性,哪些方法
        - 类之间的调用关系(继承,关联等)
        - 对象之间发送消息(调用方法)

## 第四章	类和对象

### 4.2 类

#### 4.2.1 类声明

类名首字母大写,应当符合大驼峰

#### 4.2.3 字段(field) 成员变量

- 字段在声明时如果没有初始化则会默认赋初值(数值赋0,boolean赋false,引用型赋null),局部变量声明时必须初始化(赋初值).

- 在类的声明变量部分所声明的变量叫做字段或成员变量或域变量.

- 成员变量在类体中有效,且其有效性和它在类体中书写的先后位置无关.
- 变量命名符合小驼峰,且一行只声明一个.

#### 4.2.4 方法

- 方法头由方法的类型,名称和参数构成,没有类型的方法是构造器
- {} 和其中的内容为方法体,方法体中定义的变量为局部变量,只在方法内部有效,且没有默认值.
- 当局部变量和成员变量同名时,成员变量被隐藏,要用的话需要this关键字.

### 4.3 构造方法与对象的创建

#### 4.3.1 构造方法

- 构造方法没有类型名.形如:

    ``` java
    public class Zy{
        // 构造器
        Zy(){
        }
    }
    ```

    

- 构造方法可以有多个,但必须保证参数类型或数量不同.

- 如果类中没有定义构造方法则Java会提供一个无参数且方法体为空的默认构造器,如果已经定义了则不会提供.

#### 4.3.2 创建对象

##### 步骤:

- 对象的声明: 类名	对象名

    ```java
    Zy	zhangYu;
    ```
    
- 为声明的对象分配变量:使用new运算符和类的构造方法为声明的对象分配变量(实体),即创建对象(实例化).

    ```java
    ZangYu = new Zy();
    ```

- 对象内存模型:

#### 4.3.4 对象的引用和实体

- 不能使用未实例化的对象.
- 一个类声明的2个对象如果具有2个相同的引用,二者就具有完全相同的变量(浅拷贝).
- 垃圾收集:Java的垃圾收集机制会周期的检测是否有某个实体已不再被任何对象引用,如果有则释放其占有的内存.

### 4.4 类与程序的基本结构

- Java程序有且只有一个主类(含有main方法的类).
- Java程序可以有若干类放在若干个源文件中.

### 4.5 参数传值

- Java中所有方法参数都是传值的,方法改变参数的值,原值不会变,相当于原件复印件.

- 基本数据类型参数,向该参数传递的值级别(精度)不可以高于该参数的级别,如可以向double类型传递float值但不能向int类型传递float值.

- 引用型数据包括数组,对象,接口.

- 改变引用型数据的实体会导致原变量的实体同样发生变化但改变引用不会.

- 可变参数形如下面代码,其参数类型必须相同.

    ```java
    public void f(int ...x){
        .....
    }
    ```
### 4.6 对象的组合

- 一个类可以把对象作为自己的成员变量,如果用这样的类创建对象那么该对象中就会有其它的对象,也就是说该类的对象将其它对象作为自己的组成部分,这就是人们常说的Has-A.
- 组合与复用:如果一个对象a组合了对象b,那么a就可以委托b调用其方法,即a通过组合复用了b的方法.

### 4.7 实例成员与类成员

- 成员变量可以分为实例变量和类变量,用关键字static声明的变量为类变量,其余为实例变量.

    区别:

    - 同一个类的不同对象实例变量互不相同.
    - 同一个类的所有对象共享类变量.
    - 可以通过类名直接访问类变量.
    - 同一个类中的static方法不能直接利用this调用本类的实例方法或实例变量,必须向实例化一个对象,再用对象调用实例方法或实例变量.

- 方法也可以分为实例方法和类方法.

    区别:

    - 只有该类new的对象才能调用实例方法.
    - 类方法可以通过类名直接调用.
    - 原则:如果一个方法不需要操作类中任何实例变量就可以满足程序需求就可以将其设计为类方法.

### 4.8 方法重载

- 方法可以重载和重写.

- 重载要求方法的签名(signature,`方法名+形参列表`即参数的个数或类型)不同,通过重载可以实现多态(polymorphism).

    ```
    注:方法签名相同但是返回类型不同的方法不是重载
    ```

    

### 4.9 this关键字

- this关键字在类的构造方法中出现时,代表使用该构造方法所创建的对象.

- 实例方法中 this.成员变量    类名.类变量 当局部变量与成员变量同名时this不可省略.

- 构造方法中可以用this调用另一个构造方法,必须放在第一句.如下

    ```java
    class Test {
        private String name;
        private String useWay;
    
        Test(String name) {
            this.name = name;
        }
    
        Test() {
            this("test");
            this.useWay = "I want to try whether this can call" +
                    " other construction methods.";
        }
    
        public void printMes() {
            System.out.println(this.name);
            System.out.println(this.useWay);
        }
    }
    ```

    

### 4.10 访问权限

- 用关键字private修饰的成员变量和方法称为私有变量和私有方法
    - 只有类自己的方法可以访问自己的私有变量和调用私有方法.

- 用public修饰的成员变量和方法被称为共有变量和共有方法.
    - 共有变量和方法可以在所有范围内被类名调用.

- 用protected方法修饰的成员变量和方法被称为受保护的变量和方法.
    - 在同一个包中的类可以通过对象组合访问该类的受保护的变量和方法.

- 没有用以上关键字修饰的变量和方法称为友好变量和方法.
    - 同一个包中的类可以通过类名访问类友好方法和变量.

访问权限排名:

```java
//注:类不可以用protected和private修饰
public > protected > package-private > private
```



```java
1.在顶级
public或package-private（没有显式修饰符即默认权限）。

类可以用修饰符public声明，在这种情况下，类对所有类都可见。如果一个类没有修饰符（默认，也称为package-private），它只在自己的包中可见。


2.在成员级别 
public，private，protected或package-private（没有显式修饰符即默认权限）。

在成员级别，也可以使用public修饰符或无修饰符（package-private），如同顶级类一样，具有相同的含义。

对于成员，除public和默认外有两个附加的访问修饰符：private和protected：

private修饰符指定该成员只能在其自己的类中访问。

protected修饰符指定该成员只能在其自己的包（如package-private）中访问，此外还可以由另一个包中的该类的子类访问。

下表显示了对每个修饰符允许的成员的访问权限。

第一列指示类本身是否有权访问由访问级别定义的成员。正如你可以看到，一个类总是有权访问它自己的成员。

第二列指示与该类（不管其父级）相同的包中的类是否具有对成员的访问权限。

第三列指示在此包外部声明的该类的子类是否有权访问成员。

第四列指示是否所有类都具有对成员的访问权限。
```

![img](https://img-blog.csdn.net/20170106135950985)

## 第五章    子类与继承

- 继承可以提高程序的抽象程度
- 继承可以实现代码的重用,提高开发效率和可维护性

### 5.1 子类和父类

- 在类的声明中通过`extends`关键字来定义一个子类 ,形如

    ```java
    class Child extends Parents{
        ...
    }
    ```

- 如果类声明时没有`extends`字句则默认该类为继承`java.lang.Object`的子类.

- 继承关系在UML图中是`is a`的关系

- 一个类可以有多个或0个子类,但只能有一个父类(只能继承一个类,extends后只能跟一个类).

### 5.2 子类的继承性

- 当子类和父类在同一个包时,子类可以继承父类中不是private修饰的成员变量和方法.
- 当子类和父类不在同一个包时,子类只能继承父类中public和protected修饰的成员变量和方法.

### 5.3 子类和对象

- 当用子类的构造方法创建一个子类对象时,不仅子类中声明的成员变量被分配了内存而且父类成员变量也都分配了内存.但只将子类有访问权限的变量作为分配给子类的变量.
- instanceof运算符:A instanceof B (A是对象,B是类)如果A是B或其子类所创建的对象则表达式的值为true否则为false.

### 5.4 成员变量的隐藏和方法重写

- 如果子类声明的成员变量和继承的变量名字相同则继承的变量会被隐藏.但子类仍然可以通过super关键词调用被隐藏的变量.

    ```注
    子类继承的方法只能调用子类继承和被隐藏的变量,不能调用新声明的变量.
    ```

- 子类可以重写继承的方法,重写的方法类型必须和父类中的方法一样或是其子类型,方法签名(方法的名字,参数个数,参数类型)必须和父类方法完全一致.

- 子类可以通过方法的重写隐藏继承的方法.

- 子类重写后的方法和子类新声明的方法等地位,可以访问子类继承和新声明的变量和方法但不能访问被隐藏的变量.

- 重写父类方法不允许降低方法的访问权限但可以提高访问权限.

    - 选择题7

### 5.5 super 关键字

- 可以用super关键字调用被隐藏的父类方法和变量.
  
- 当super调用被隐藏的方法时,该方法的成员变量是被隐藏或继承的成员变量.
  
- 当用子类的构造方法创建一个子类对象时,子类的构造方法总是先调用父类的构造方法,当未指定时优先调用不带参数的构造方法.

- 由于子类不继承父类的构造方法,因此,子类在其构造方法中需要使用super关键字来调用父类构造方法,且super语句必须在子类构造方法的第一句.当子类构造方法中没有super语句时默认的有

    ```java
    super();
    // 如果父类中没有不带参数的构造方法则会报错
    There is no default constructor available in 'c5.A'
    ```

### 5.6 final 关键字

- `final`可以修饰类,成员变量和方法中的局部变量.
- `final`类不能被继承,即不能有子类.
- `final`方法不允许子类重写即不会被隐藏.
    - `static`方法也一样(表面上可以重写但实际上没有卵用)
- `final`修饰的成员变量和局部变量为常量.
    - 常量在运行期间不允许发生修改.
    - 常量没有默认值,在声明常量时必须指定常量的值.

### 5.7 对象的上转型对象

- 假设Parents 类是Child类的父类,当用Child类创建一个对象b,并把对象b的引用放到父类所创建的对象a中时,称对象a是对象b的上转型对象.

    ```java
    // a 是 b 的上转型对象
    Child b = new Child();
    Parent a = b;
    ```

- 上转型对象是子类负责创建的,但上转型对象会失去原对象的一些属性功能.
    - 上转型对象不能操作子类新增的成员变量(失掉了这部分属性），上转型对象不能调用子类新增的方法（失掉了这部分行为）。
    - 上转型对象可以访向于类维承和隐藏的成员变量，也可以调用子类继承的方法或子类重写的方法。
    - 上转型对象操作类继承的方法或子类重写的实例方法，其作用等价于子类对象去调用这些方法。因此，如果子类重写了父类的某个实例方法后，对象的上转型调用这个实例方法时定是调用 了子类重写的实例方法。

- 上转型对象的引用被重新放到子类对象中称为下转型对象.
    - 下转型不是将一个父类对象强转成子类对象,这样会直接报错
        ```java.lang.ClassCastException```

### 5.9 abstract 类和 abstract 方法

- 用关键词abstract修饰的类和方法称为abstract类(抽象类)和abstract方法(抽象)方法.
    - abstract方法只允许声明,不允许实现(无方法体).
    - 不允许用final修饰abstract方法和abstract类.
    - 不允许用static修饰abstract方法.
- abstract类中可以有(也可以没有)abstract方法和非abstract方法,非abstract类中不可以有abstract方法.
- abstract类不能用new创建对象.
    - abstract类的非abstract子类才能new一个对象,且子类必须重写父类中的全部abstract方法,这就是不能用final修饰的原因.
    - abstract类的abstract子类可以重写或继承父类的abstract方法.

- 可以使用abstract类声明对象,尽管不能使用new创建该对象,但该对象可以成为其子类的上转型对象,那么该对象可以调用子类重写的方法.

### 5.10 面向抽象编程

- 使用多态进行程序设计的核心技术之一就是使用上转型对象,即将abstract类声明的对象作为其子类对象的上转型对象.

### 5.11 开闭原则(***很重要***)

- 设计的系统对扩展开放,对修改关闭.(**用抽象构建框架，用实现扩展细节**)

- Java设计模式六大原则:
  
    - 单一职责:一个类只负责一项职责。
    - 里氏替换原则:子类可以扩展父类的功能，但不能改变父类原有的功能。
    - 依赖倒置原则:高层模块不应该依赖低层模块，二者都应该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象。
    - 接口隔离原则:将臃肿的接口I拆分为独立的几个接口，类A和类C分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则。
    - 迪米特法则:一个类对自己依赖的类知道的越少越好。也就是说，对于被依赖的类来说，无论逻辑多么复杂，都尽量地的将逻辑封装在类的内部，对外除了提供的public方法，不对外泄漏任何信息。
    - 开闭原则:对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。所以一句话概括就是：为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，需要面向接口编程。
    
      > [原文链接](https://blog.csdn.net/qq_34182649/article/details/107881628?ops_request_misc=&request_id=&biz_id=102&utm_term=java%25E8%25AE%25BE%25E8%25AE%25A1%25E6%25A8%25A1%25E5%25BC%258F%25E5%2585%25AD%25E5%25A4%25A7%25E5%258E%259F%25E5%2588%2599&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-107881628.first_rank_v2_pc_rank_v29)

## 第六章    接口与实现

### 6.1 接口

```java
// 接口声明
interface InterfaceName{
    // 接口体
    ...
}
```

- 接口体中只能声明常量和抽象方法
- 接口体中的常量必须是` public static `(可省略)修饰的.
- 接口体中的抽象方法必须是` public abstract `(可省略)修饰的.

### 6.2 实现接口

```java
//用implements关键字在声明类时实现接口
class Hh extends He implements Interface1,Interface2{
    ...
}
```

- 类可以在声明时用implements关键字声明实现那些接口,多个接口用' , '分隔.
- 非抽象类实现接口必须要重新接口中所有方法,且重写后的方法必须用public修饰.
- 一个类可以用接口名访问接口中的常量,但一个类如果实现了接口可以直接在类体中使用常量.
- 接口和类一样也可用public修饰.
- 如果父类实现了某个接口,则子类也自然实现了该接口.
- 接口也可以被继承.

### 6.3 接口回调

- 接口回调类似与上转型对象,将实现了接口的类所创建的对象的引用赋给一个接口变量,该接口就可以调用被实现的方法.

### 6.4 接口参数

如果一个方法的参数类型是接口,那么该参数可以是实现了该接口的类的对象.

## 第七章   内部类与异常类 

### 7.1 内部类

- 内部类的外嵌类的成员变量在内部类中仍然有效,内部类的方法也可以调用外嵌类的方法.
- 内部类类体中不可以声明类变量和类方法,外嵌类的类体可以用内部类创建的对象作为成员.
- 内部类仅供它的外嵌类使用.
- 内部类可以用static修饰(静态内部类).
    - 静态内部类可供非外嵌类使用.
    
    - 静态内部类不可以使用外嵌类的成员变量.
    
    - 非内部类不能用static修饰.
    
        ```java
        public class BlackCowForm {
            public static void main(String[] args) {
                // 外嵌类.静态内部类 来调用静态内部类
                RedCowForm.RedCow red = new RedCowForm.RedCow();
                red.speak();
            }
        }
        class RedCowForm{
            static class RedCow{
                public void speak(){
                    System.out.println("I am a RedCow!");
                }
            }
        }
        ```
    
        

### 7.2    匿名类

#### 7.2.1 子类匿名类

```java
//匿名类是父类的子类 
new Parent () {
    ...
}
```

- 匿名类可以继承也可以重写父类中的方法.
- 使用匿名类时,必然是在某个类中直接用匿名类创建对象,因此匿名类一定是内部类.
- 由于匿名类是一个子类但没有类名因此匿名类可以直接使用父类的构造方法.

#### 7.2.2 接口匿名类

```java
//实现接口的匿名类
new Interface (){
    ...
}
```

- java允许直接用接口名和类体组合创建一个匿名对象传递给方法作为参数,类体必须重写方法中的全部参数.

### 7.3 异常类

- 异常就是程序运行时可能会出现的一些错误,比如试图打开一个根本不存在的文件等.
  
- java 使用throw关键字抛出一个Exception子类的实例表示异常发生.
  
- java用try-catch语句来处理异常,将可能出现的异常放在try部分,一旦try部分抛出异常对象(实例),或调用某个可能抛出异常对象的方法并且该方法抛出了异常对象,那么try部分将立即结束执行,转向执行catch部分.try-catch语句可以有多个catch部分.

    ```java
    try{
        包含可能发生异常的语句
    }
    // 各个catch函数的参数为Exception的子类,这些子类之间不能含有父子关系,否则保留一个父类即可.
    catch(ExceptionSubClass1){
        ...
    }
    catch(ExceptionSubclass2){
        ...
    }
    ```

- 在编写程序时可以扩展Exception类定义自己的异常类,然后根据程序的需要来规定那些方法会产生这样的异常.一个方法在声明时可以使用throws关键字声明要产生的若干个异常,并在该方法的方法体中具体给出产生异常的操作,即用相应的异常类创建对象,并使用throw关键抛出异常.

### 7.4 断言

断言语句一般用于程序不准备通过捕获异常来处理的错误,例如,当发生某个错误时,要求程序必须立即停止执行.在调试代码阶段让断言语句发挥作用这样就可以发现一些重要错误,当程序正式运行时就可以关闭断言语句.

```java
// 如果booleanExpression值为true则继续执行否则程序立刻结束执行.
assert booleanExpression;
// 如果booleanExpression值为true则继续执行否则程序立刻结束执行并输出messageException的值提示用户出现了什么错误.
assert booleanExpression:messageException;
// java解释器默认关闭断言语句可以使用 -ea命令启用断言
java -ea mainClass
```

finally语句:在执行try-catch语句后执行finally子语句,也就是说无论try部分是否发生异常finally语句都会被执行.

- 如果try-catch部分执行了return语句,那么finally语句仍然会执行.
- 如果try-catch部分执行了System.exit(0);(退出代码)那么finally语句不执行.

## 第八章    常用实用类

### 8.1 String类

- String 常量也是对象,是用双引号括起的字符串.

- String 对象可以用String类new也可以直接引用String常量.

    ```java
    // 用new运算符创建对象
    String s = new String("zyssb");
    String t = new String("zyssb");
    // 引用常量
    String s1 = "zyssb";
    String s2 = "zyssb";
    //常用的2个构造方法
    char a[] = {'z','y','s','s','b'};
    String s_1 = new String(a);
    // 数组名,起始位置,截取字符数
    String t_1 = new String(a,0,5);
    ```

    ```
    注:s,t,s_1,t_1都是对象变量,他们本身的值是引用所以即使他们引用的变量值相等他们本身也不相等即s==t的值为false(使用new运算符会为变量新开辟一个内存空间).
    但s1和s2引用的是同一个常量池中的同一个常量,所以s1==s2的值为真.
    ```

- String对象可以用"+"运算符进行并置运算,即首尾相接得到一个新的String对象.

    - 如果是两个常量进行并置则结果仍然是常量,常量池中如果2个都有则合一,如果没有则新的会被加入常量池.

    - 如果2个中有一个是变量,则就会生成新的实体和引用.

        ```java
        //s4和s3的引用相同都是指向常量池中的"helloworld",和ss不同;
        String s1 = "hello";
        String s2 = "world";
        String s3 = s1 + s2;
        String s4 = "helloworld";
        String ss = new String("world");
        ss = s1 + ss;
        ```

        

- 常用方法:

    ```java
    // 求长 length函数
    int len = str.length();
    // 判断 equals函数
    // 值为真
    s.equals(t);
    // 判断前缀后缀 startsWith,endsWith
    "hhby".startsWith("hh");
    "hhby".endsWith("by");
    // 比较 compareTo
    s.compareTo(t)=0;
    ```

- 数据转换 
    - String 到基本数据类型:int = Integer.parseInt(str);(其他类似)
    - 基本数据类型到String: str = valueOf(123455);

- 正则表达式

    [参考](https://blog.csdn.net/qq_18298439/article/details/88974940?ops_request_misc=%25257B%252522request%25255Fid%252522%25253A%252522160812422416780265396509%252522%25252C%252522scm%252522%25253A%25252220140713.130102334..%252522%25257D&request_id=160812422416780265396509&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-88974940.first_rank_v2_pc_rank_v29&utm_term=java%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)

- 字符分割
    - String 提供的split(String)方法.
    - StringTokenizer类. 
    - Scanner类.
    
- 注:阅读程序题1.由于String对象的实体不能修改加上方法参数的引用不会被改变所以任何方法不可能改变String对象作为参数的实体和引用.

### 8.2 StringBuffer类

- String对象的字符序列不可修改.即String的实体不能修改.
- 三个构造方法:
    - StringBuffer();无参数默认长度16个字符如果实体长度大于16则会自动增加长度.
    - StringBuffer(int size);指定长度如果实体长度大于16则会自动增加长度.
    - StringBuffer(String s)指定实体的初始容量为s的长度加16.

## 第九章    组件及事件处理

### 9.1 Java Swing 概述

- Component 的子类或间接子类创建的对象称为一个组件.
- Container 的子类或间接子类创建的对象称为一个容器.
- 可以利用Container提供的add()方法向容器添加组件.
- 容器可以调用removeAll()方法移除容器中所有组件,可以调用remove(Component c)方法移除指定的参数:c组件.
- 容器本身也是一个组件,可以把一个容器添加到另一个容器中实现容器的嵌套.
- 每当容器添加或移除组件时应当让容器调用validate()方法,以保证容器的组件能够正确显示出来.
- <img src=".\..\markdownRes\java\05.png" alt="image-20201217164025284" style="zoom:20%;" />

### 9.2 窗口

- java窗口类:JFrame

    - JFrame():创建无标题窗口.
    - JFrame(String s):创建标题为s的窗口.
    - setBonds(x,y,w,h):设置窗口4个属性分别为,距离屏幕左面x像素,距离屏幕上方y像素,长h像素,宽w像素.
    - setLocation(x,y):设置窗口位置默认0,0(左上角).
    - setSize(w,h):设置窗口大小.(以上三个方法的参数全文int类型)
    - setVisible(boolean b):设置窗口是否可见,默认不可见.
    - setResizeable(boolean b):设置窗口是否可调整大小,默认可调整.
    - dispose():撤销当前窗口,并释放当前窗口所使用的资源.
    - setExtendedState(int state):设置窗口扩展状态,其中参数state取JFrame类以下常量:
        - MAXIMIZED_HORIZ:水平方向最大化.
        - MAXIMIZED_VERT:垂直方向最大化.
        - MAXIMIZED_BOTH:都最大化.

    - setDefaultCloseOperation(int operation):设置点击窗口右上角关闭图标后的操作,参数operation取JFrame类以下常量:
        - DO_NOTHING_ON_CLOSE:什么也不做.
        - HIDE_ON_CLOSE:隐藏当前窗口.
        - DISPODE_ON_CLOSE:隐藏当前窗口并释放窗口使用的资源.
        - EXIT_ON_CLOSE:结束窗口所在的应用程序.

- 菜单条,菜单,菜单项是窗口的常用组件,菜单放在菜单条里,菜单项放在菜单里.

    - JComponent类的子类JMenuBar负责创建菜单条.
    
- setJMenuBar(JMenuBar bar):将bar菜单条放在窗口里.
  
- JComponent类的子类JMenu负责创建菜单.
  
- JComponent类的子类JMenuItem负责创建菜单项.
  
- 可以用Icon类声明一个图标然后用其子类ImageIcon创建一个图标,再调用setIcon方法将图标设置为icon:
  
    ```java
    Icon icon = new ImageIcon("xxx.jpg");
    JMenuItem jmi = new JMenuItem();
    jmi.setIcon(icon);   
    ```

### 9.3 常见组件及布局

- 常用组件:
    - JTextField类:文本框,允许用户在文本框输入单行文本.
    - JTextArea类:文本区,允许用户在文本区输入多行文本.
    - JButton类:按钮,允许用户单击按钮.
    - JLabel类:标签.
    - JCheckBox类:复选框.
    - JRadioButton类:单选按钮.
    - JComboBox类:下拉菜单.
    - JPasswordField类:密码框.

- 常见容器(本节所提到的均为中间容器需要被添加到底层容器才能生效):

    - JPanel类:面板,经常使用JPanel类创建一个面板,再向这个面板添加组件,然后把这个面板添加到其它容器中.面板默认布局为FlowLayout布局.

    - JTabbedPane类:选项卡窗格,可以向其中添加组件,一个组件对应一个选项.

        ```java
        JTabbedPane jtp = new JTabbdePane();
        // str为字符串文本提示,c为要添加的组件.
        jtp.add(str, c);
        ```

    - JScrollPane类:滚动窗格,只能添加一个组件,可以把一个组件放在其中通过滚动条来看.

    - JSplitPane类:拆分窗格,分水平拆分和垂直拆分,拆分线可以移动.

    - JLayeredPane类:分层窗格,需要处理重叠问题时可用,可分为五层.

- 容器可以使用setLayout()方法设置自己的布局,常用布局:

    - FlowLayout布局:居中对齐,从左到右排列,排满换行.
    - BorderLayout布局:分东西南北中五个区域中间最大,每个区域只显示一个组件.
    - CardLayout布局:层叠布局,最先放进去的组件显示在最上层.
    - GridLayout布局:分成若干行若干列的网格布局.
    - null布局:空布局,空布局容器可以准确定位组件在容器中的大小和位置.
    - BoxLayout布局:盒式容器.

### 9.4 处理事件

- 事件处理模式:
    - 事件源:能够产生事件的对象.
    - 监视器:一个对象对事件源对象进行监视.
    - 处理事件的接口:监视器检测到了事件源产生事件需要调用方法去处理事件.

- ActionEvent事件
    - ActionEvent事件源:文本框,按钮等都可以触发ActionEvent事件,都可以成为ActionEvent事件源.
    - 注册监视器:ActionEvent事件源都可以用addActionListener(ActionListener listener)方法将实现了ActionListener接口的子类的实例注册为事件源的监视器.
    - ActionListener接口:该接口只有一个方法:actionPerformed(ActionEvent event).
- ItemEvent事件
    - 事件源:选择框,下拉列表.
    - 监听器:addItemListener(ItemListener listener).
    - 接口:
- DocumentEvent事件
    - 事件源:文本区.
    - 监听器:addDocumentListener(DoucmentListener listener).
    - 接口:

- MouseEvent事件

    - 事件源:所有组件.

    - 5种事件:

        - 在事件源上按下鼠标键
        - 在事件源上释放鼠标键
        - 在事件源上单击鼠标
        - 在事件源上进入事件源
        - 在事件源上退出事件源(离开)

    - 重要方法:

        - getX(),getY()获取鼠标坐标.

        - getModifiers()获取鼠标左键或右键.

        - getCountClick()获取鼠标被单击次数.

        - getSource()获取发生鼠标事件的事件源.

            (书p245)......

- 焦点事件
- 键盘事件
- 窗口事件

## 第十章    输入输出流

### 10.1 File类

- 构造方法:

    ```java
    //filename 文件名
    File(String filename);
    //directoryPath 文件路径
    File(String directoryPatn, String filename);
    //dir 目录
    File(File dir, String filename);
    ```

- 获取文件属性的方法.
    - getName() 文件名
    - canRead() 是否可读
    - canWrite() 是否可写
    - exists() 是否存在
    - length() 长度
    - getAbsolutePath() 绝对路径
    - getParent() 父目录
    - isFile() 是否是普通文件而不是目录
    - isDirectory() 是否是目录
    - isHidden() 是否是隐藏文件
    - lastModified() 最后一次修改时间

- 目录
    - mkdir()创建目录
    - list(),listFiles()列出目录下文件

- 文件创建与删除
    - createNewFile()创建
    - delete()删除

- 运行可执行文件
  
- 用Runtime类声明一个对象,然后用类方法getRuntime()创建对象.
  
- 文件字节输入流 FileInputStream

    - 基本步骤:
        - 设定输入流的源.
        - 创建指向源的输入流.
        - 让输入流读取源中的数据.
        - 关闭输入流.

    - 构造方法:
        - FileInputStream(String name);指定文件名.
        - FileInputStream(File file);指定文件对象.

    - 使用输入流读取字节:
        - int read();读取单个字节,返回字节值0~255,未读取到返回-1.
        - int read(byte b[]);读取b.length个字节到字节数组b中,返回实际读取字节数量,如果达到文件尾返回-1.
        - int read(byte b[], int off, int len);读取len个字节从b中off位置开始存储,如果达到文件尾返回-1.

    - 关闭流:
        - close();

    注:FileInputStream流顺序地读取文件,只要不关闭流,每次调用read方法就顺序地读取源中其余内容,直至末尾或被关闭.

- 文件字节输出流 FileOutputStream

    - 基本步骤:
        - 设定输出流的目的地.
        - 创建指向目的地的输出流.
        - 让输出流把数据写入到目的地.
        - 关闭输出流.

    - 构造方法:
        - FileOutputStream(String name);
        - FileOutputStream(File file);
        - FileOutputStream(xxx, boolean append);可选择是否刷新文件(true在文件尾部写,false在头部)

    - 使用输出流写字节:
        - write(int n);
        - write(byte b[]);
        - write(byte b[], int off, int len);

    - 关闭流:
        - close();

- 文件字符输入输出流
    - 以字符形式输入输出(一个汉字占2个字节).
    - FileReader;
    - FileWriter;

- 缓冲流

    - 输入:BuffererReader

        - BuffererReader(Reader reader);构造方法
        - readLine();读取一行文本.

    - 输出:BufferedWriter

        - BufferedWriter(Writer writer);构造方法

        - newLine();输出一行

- 随机流 RandomAccessFile
    - 即可以读取也可以写入
    - 构造方法:
        - RandomAccessFile(String name, String mode);
        - RandomAccessFile(File file, String mode);
        - 指向文件时不刷新文件.

- 数组流

    - 字节数组流
        - ByteArrayInputStream
        - ByteArrayOutputStream

    - 字符数组流
        - CharArrayReader
        - CharArrayWriter

- 数据流
    - DataInputStream
    - DataOutputStream

- 对象流
    - ObjectInputStream
    - ObjectOutputStream
    - 对象要序列化.
    - 可以用对象流先写入在读取的方式克隆对象.

### 10.2 流及分类

1. **流:不同类型的输入输出都抽象为流,按方向可分为输入流和输出流.**

![](.\..\markdownRes\java\01.jpg)

2. **字节流和字符流**

    > 字节流每次读取一个字节,字符流每次读取一个字符,一个字符在不同编码下可以是一个或多个字节.
    
    |      |    字节流    | 字符流 |
    | :--: | :----------: | :----: |
    | 输入 | InputStream  | Reader |
    | 输出 | OutputStream | Writer |

3. 节点流和处理流

- 节点流(Node Stream)

    - 可以从或向一个特定的地方(节点)读写数据.

    - 如文件流FileInputStream,内存流ByteArrayInputStream.

    - 常用节点流

        <img src=".\..\markdownRes\java\02.jpg" style="zoom:90%;" />

- 处理流(Processing Stream)

    - 是对一个已存在的流的连接和封装,处理流又称为过滤流(Filter).

    - 如缓冲处理流BufferedReader.

        <img src=".\..\markdownRes\java\04.png" style="zoom:80%;" />

    - 处理流的构造方法总是要带一个其他的流对象作参数.

        ```java
        //常用处理流构造方法
        BufferedReader in = new BufferedReader(
                            	new InputStreamReader(
                                    new FileInputStream(filename), StandardCharsets.UTF_8));
        String s1 = in.readLine();
        System.out.println("s1 = " + s1);
        ```

### 10.3 常见内容的读写

1. 二进制(图片等)

    ```java
    //示例
    public static void dump(InputStream src, OutputStream dest) throws IOException {
            InputStream input = new BufferedInputStream(src);
            OutputStream output = new BufferedOutputStream(dest);
            byte[] data = new byte[1000];
            int length = -1;
            while ((length = input.read(data)) != -1) {
                output.write(data, 0, length);
            }
            input.close();
            output.close();
        }
    ```

2. 文本(字符)

    - 不同编码字符不同.

3. 对象

    - 对象和基本数据在写的时候都是用二进制流.

    - 对象读写:ObjectInputStream,ObjiectOutputStream
    - 基本数据读写:DataInputStream,DataOutputStream
    - 将对象或基本数据写入文件的过程称为序列化(Serialize),从文件读取对象或数据的过程称为反序列化(deserialize)
    - 序列化对象要求对象实现Serializable接口(该接口无方法,只是一个标记)

### 10.4 网络流



## 第十二章    Java多线程机制

### 12.1 进程与线程

- 程序是一段静态代码,是应用软件执行的蓝本.
- 进程是程序的一次动态执行过程.
- 线程是比进程更小的执行单位,一个进程在其执行过程中可以产生多个线程,形成多条执行线索.

### 12.2 Java中的线程

- Java语言内置对多线程的支持.多线程是指一个应用程序中同时存在几个执行体,按几条不同的执行线索共同工作的情况.

- Java应用程序总是从主类的main方法开始运行,当JVM加载代码发现main方法时会启动一个线程,称为主线程(main线程),该线程执行main方法.如果main方法执行中再创建线程就称为程序中的其他线程.如果没有其他线程那么main方法返回时JVM就会结束执行.
- 线程的状态与生命周期:
    - 状态:
        - 新建:线程程被创建时.
        - 运行:轮到线程来享用CPU资源时.
        - 中断:
        - 死亡:

- 线程调度与优先级:
    - 线程优先级影响线程调度的先后顺序,优先级越高越先调度.
    - 初始优先级为5,可以用setPriority(int grade)方法修改.

### 12.3 Thread类与线程的创建

- 使用Thread子类创建线程
    - 在用Thread子类创建线程时必须重写父类run()方法因为父类run()方法中没有语句.
- 使用Thread类创建线程
    - 构造方法:Thread(Runnable target);其中target为实现了Runnable接口的类创建的对象称作所创建线程的目标对象,当线程调用start()方法后,一旦轮到它来享用CPU资源后目标对象就会自动调用接口中的run()方法,这一方法是自动实现的只需要让线程调用start()方法就行了.

- 线程间可以共享相同的内存单元,并利用这些共享单元来进行数据交换,实时通信与必要的同步操作.
- 使用Runable接口比Thread子类更加灵活.

- 目标对象与线程直间的关系.
    - 完全解耦:目标对象不包含对线程对象的引用.
    - 弱耦合:目标对象可以组合线程,即将线程作为自己的成员.

### 12.4 线程的常用方法

- start():启动线程使之从新建状态到就绪状态,不可反复调用.
- run():Thread类的run方法和Runnable的run方法效果相同,都用来定义线程对象被调度之后所执行的操作,都是系统自动调用而用户程序不得引用的方法.
- sleep():休眠,可以通过让高优先级线程休眠来使低优先级的线程先被调用.
- isAlive():在线程run方法执行时返回true否则返回false.
- currentThread():类方法返回当前正在使用CPU资源的线程.
- interrupt():唤醒休眠的线程.

### 12.5 线程同步

- 线程同步即是若干个线程都需要使用一个方法,而这个方法用synchronize修饰.
- 机制:一个线程使用synchronize方法时其他线程想要使用都必须等待.

### 12.6 协调同步的线程

- 使用wait()方法中断线程的执行,使本线程等待暂时让出CPU使用权让后面的线程使用同步方法.

### 12.7 线程联合

- 一个线程A在占有CPU资源期间可以让其他线程调用join()方法和本线程联合,如:

    ```java
    B.join();
    ```

    我们称A在运行期间联合了B.如果A在占有CPU资源期间一旦联合了B线程那么A线程将立即中断执行一直等到B执行完毕,如果A准备联合的B已经结束,那么B.join()不会生效.

### 12.8 GUI线程

- 当Java程序包含GUI时,JVM在启动程序时会自动启动更多的线程,其中2个最重要的:
    - AWT-EventQueue:负责处理GUI事件.
    - AWT-Windows:负责将窗体或组件绘制到桌面.

### 12.9 计时器线程

- 当某些操作需要周期性执行可以使用计时器.

### 12.10 守护线程

- 线程默认是非守护线程.
- 非守护线程也称user线程(用户线程).
- 一个线程可以调用setDaemon(boolean on)方法将自己设置成一个守护线程.
- 当所有用户线程都结束时即使守护线程仍有run方法在执行也会立即结束运行.

## 第十五章    泛型与集合框架

### 15.1 泛型

- ```java
    //泛型类声明
    class People<E>{
        ...
    }
    ```

    people是类名,E是泛型即未指定类型的数据,它可以是任何对象和接口但不能是基本类型.

- ```java
    //使用泛型类声明对象
    People<Dog> zy = new People<Dog>(new Dog());
    ```

### 15.2 链表

- LinkedList<E>泛型类可以创建链表对象.

- 常用方法:

    - add()
    - clear()
    - remove()
    - get()
    - indexOf()
    - lastIndexOf()
    - set()
    - size()
    - contains()

    - addFirst()
    - addLast()
    - getFirst()
    - getLast()
    - removeFirst()
    - removeLast()
    - clone()

- 遍历链表
    - 使用iterator()方法获取一个Iterator(迭代器)对象.

- 排序与查找
    - sort()
    - binarySearch()
- 洗牌与旋转
    - shuffle()将链表中数据按洗牌算法随机排序.
    - rotate()旋转链表中的数据正值右转.
    - reverse()倒置数据.

### 15.4 散列映射

- HashMap<K,V>类

### 15.5 树集

- TreeSet<E>泛型类
    - add()添加节点
- 常用方法:
    - clear
    - 