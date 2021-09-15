# CSS学习

## 一、CSS简介

-   CSS 是一种描述 HTML 文档样式的语言。

-   CSS指的是层叠样式表 (Cascading Style Sheets)
-   CSS 描述了如何在屏幕、纸张或其他媒体上显示 HTML 元素
-   CSS 节省了大量工作。它可以同时控制多张网页的布局
-   外部样式表存储在 CSS 文件中

-   CSS发展史：

    -   CSS1.0
    -   CSS2.0：DIV（块）+CSS，HTML与CSS结构分离的思想，网页变得简单，SEO
    -   CSS2.1：浮动，定位
    -   CSS3.0：圆角、阴影、动画…浏览器兼容性~

-   优势：

    1、内容和表现分离；
    2、网页结构表现统一，可以实现复用
    3、样式十分的丰富
    4、建议使用独立于html的css文件
    5、利用SEO(搜索引擎优化)，容易被搜索引擎收录！

## 二、CSS导入方式

### 1. 外部样式

1.  使用`<link>`元素导入

```html
<!--外部样式-->
<link rel="stylesheet" href="xxx/xxx.css">
```

2.  使用`@import`导入(CSS2.1特有，不推荐使用)

```html
<!--导入式-->
<style>
    @import url("xxx/xxx.css");
</style>
```

### 2. 内部样式

-   使用`<style>`标签，直接在内部写如CSS样式

```html
<!-- 内部样式 -->
<style>
    p {
        ...
    }
</style>
```

### 3. 行内样式

-   在标签内添加`style`属性写入CSS样式

```html
<p style="color: red">hhby</p>
```

### 4. 优先级

-   在相同样式的情况下，根据导入方式不同，样式的优先级如下所示(不包含`! important`的情况)：
    -   **==行内样式的优先级最高，内部样式和外部样式的优先级相同，谁在后面谁优先==**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css简介</title>
    <!--外部样式-->
    <link href="static/css/01.css" rel="stylesheet">
    <!--内部样式-->
    <style>
        p {
            background-color: black;
        }
    </style>
</head>
<body>
<!--内部样式在后面，所以背景是黑色的-->
<p>hhby</p>
<!--行内样式-->
<p style="color: red">hhby</p>
</body>
</html>
```

## 三、CSS语法

-   CSS 规则集（rule-set）由选择器和声明块组成：

![image-20210915094939561](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210915094939561.png)

-   选择器指向您需要设置样式的 HTML 元素。

- 声明块包含一条或多条用分号分隔的声明。

-   每条声明都包含一个 CSS 属性名称和一个值，以冒号分隔。

-   多条 CSS 声明用分号分隔，声明块用花括号括起来。
-   CSS注释由`/* */`组成

## 四、==CSS选择器==

>   CSS 选择器用于“查找”（或选取）要设置样式的 HTML 元素。
>
>   我们可以将 CSS 选择器分为五类：
>
>   简单选择器（根据名称、id、类来选取元素）
>   组合器选择器（根据它们之间的特定关系来选取元素）
>   伪类选择器（根据特定状态选取元素）
>   伪元素选择器（选取元素的一部分并设置其样式）
>   属性选择器（根据属性或属性值来选取元素）

### 1. 简单选择器

-   元素选择器：根据元素名称进行选择
    -   语法：`元素名称 {...}`
-   类(class)选择器：根据元素`class`属性进行选择
    -   语法：`.classname {...}`
-   多类选择器：可以选择包含多个类的元素
    -   语法：`.class1.class2 {...}`
-   id选择器：根据元素`id`属性进行选择，选择唯一元素
    -   语法：`#idName {...}`
-   通用选择器：选择所有元素的选择器
    -   语法：`* {...}`
-   分组选择器：将样式相同的**元素组合器**结合起来
    -   语法：`元素1, 元素2, ...{...}`

### 2. 组合器选择器

>   组合器是解释选择器之间关系的某种机制。
>
>   CSS 选择器可以包含多个简单选择器。在简单选择器之间，我们可以包含一个组合器。
>
>   CSS 中有四种不同的组合器：
>
>   后代选择器 (空格)
>   子选择器 (>)
>   相邻兄弟选择器 (+)
>   通用兄弟选择器 (~)

-   后代选择器：后代选择器匹配属于指定元素后代的所有元素。
    -   语法：` div p {...}`(div下所有p元素)
-   子选择器：匹配属于指定元素子元素的所有元素。
    -   语法：`div > p {...}`(div的子元素p)
-   相邻兄弟选择器：匹配所有作为指定元素的相邻同级的元素。兄弟（同级）元素必须具有相同的父元素，“相邻”的意思是“紧随其后”。
    -   语法：`div + p {...}`(具有相同父元素的相邻的div和p元素)
-   通用兄弟选择器：匹配属于指定元素的同级元素的所有元素。
    -   语法：`div ~ p {...}`(与div同级的所有p元素)

### 3. 伪类选择器

>   伪类用于定义元素的特殊状态。

1.  常用伪类

    -   `:hover`：悬浮伪类，选择鼠标悬浮在上的元素
        -   语法：`element:hover{...}`

    -   锚伪类：

    ```css
    /* 未访问的链接 */
    a:link {
      color: #FF0000;
    }
    
    /* 已访问的链接 */
    a:visited {
      color: #00FF00;
    }
    
    /* 鼠标悬停链接 */
    a:hover {
      color: #FF00FF;
    }
    
    /* 已选择的链接 */
    a:active {
      color: #0000FF;
    }
    /*
    注意：a:hover 必须在 CSS 定义中的 a:link 和 a:visited 之后，才能生效！a:active 必须在 CSS 定义中的 a:hover 之后才能生效！伪类名称对大小写不敏感。
    */
    ```

    -   `:first-child`:与指定的元素匹配：该元素是另一个元素的第一个子元素。

        -   语法：

        ```css
        a:first-child /* 是第一个子元素且是a元素的元素 */
        div:first-child a /* 是第一个子元素且是div元素的元素的所有后代a元素 */
        ```

2.  伪类列表

| 伪类                                                         | 例子                  | 意义                                                         |
| ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| [:active](https://www.w3school.com.cn/cssref/selector_active.asp) | a:active              | 选择活动的链接。                                             |
| [:checked](https://www.w3school.com.cn/cssref/selector_checked.asp) | input:checked         | 选择每个被选中的 <input> 元素。                              |
| [:disabled](https://www.w3school.com.cn/cssref/selector_disabled.asp) | input:disabled        | 选择每个被禁用的 <input> 元素。                              |
| [:empty](https://www.w3school.com.cn/cssref/selector_empty.asp) | p:empty               | 选择没有子元素的每个 <p> 元素。                              |
| [:enabled](https://www.w3school.com.cn/cssref/selector_enabled.asp) | input:enabled         | 选择每个已启用的 <input> 元素。                              |
| [:first-child](https://www.w3school.com.cn/cssref/selector_first-child.asp) | p:first-child         | 选择作为其父的首个子元素的每个 <p> 元素。                    |
| [:first-of-type](https://www.w3school.com.cn/cssref/selector_first-of-type.asp) | p:first-of-type       | 选择作为其父的首个 <p> 元素的每个 <p> 元素。                 |
| [:focus](https://www.w3school.com.cn/cssref/selector_focus.asp) | input:focus           | 选择获得焦点的 <input> 元素。                                |
| [:hover](https://www.w3school.com.cn/cssref/selector_hover.asp) | a:hover               | 选择鼠标悬停其上的链接。                                     |
| [:in-range](https://www.w3school.com.cn/cssref/selector_in-range.asp) | input:in-range        | 选择具有指定范围内的值的 <input> 元素。                      |
| [:invalid](https://www.w3school.com.cn/cssref/selector_invalid.asp) | input:invalid         | 选择所有具有无效值的 <input> 元素。                          |
| [:lang(*language*)](https://www.w3school.com.cn/cssref/selector_lang.asp) | p:lang(it)            | 选择每个 lang 属性值以 "it" 开头的 <p> 元素。                |
| [:last-child](https://www.w3school.com.cn/cssref/selector_last-child.asp) | p:last-child          | 选择作为其父的最后一个子元素的每个 <p> 元素。                |
| [:last-of-type](https://www.w3school.com.cn/cssref/selector_last-of-type.asp) | p:last-of-type        | 选择作为其父的最后一个 <p> 元素的每个 <p> 元素。             |
| [:link](https://www.w3school.com.cn/cssref/selector_link.asp) | a:link                | 选择所有未被访问的链接。                                     |
| [:not(*selector*)](https://www.w3school.com.cn/cssref/selector_not.asp) | :not(p)               | 选择每个非 <p> 元素的元素。                                  |
| [:nth-child(*n*)](https://www.w3school.com.cn/cssref/selector_nth-child.asp) | p:nth-child(2)        | 选择作为其父的第二个子元素的每个 <p> 元素。                  |
| [:nth-last-child(*n*)](https://www.w3school.com.cn/cssref/selector_nth-last-child.asp) | p:nth-last-child(2)   | 选择作为父的第二个子元素的每个<p>元素，从最后一个子元素计数。 |
| [:nth-last-of-type(*n*)](https://www.w3school.com.cn/cssref/selector_nth-last-of-type.asp) | p:nth-last-of-type(2) | 选择作为父的第二个<p>元素的每个<p>元素，从最后一个子元素计数 |
| [:nth-of-type(*n*)](https://www.w3school.com.cn/cssref/selector_nth-of-type.asp) | p:nth-of-type(2)      | 选择作为其父的第二个 <p> 元素的每个 <p> 元素。               |
| [:only-of-type](https://www.w3school.com.cn/cssref/selector_only-of-type.asp) | p:only-of-type        | 选择作为其父的唯一 <p> 元素的每个 <p> 元素。                 |
| [:only-child](https://www.w3school.com.cn/cssref/selector_only-child.asp) | p:only-child          | 选择作为其父的唯一子元素的 <p> 元素。                        |
| [:optional](https://www.w3school.com.cn/cssref/selector_optional.asp) | input:optional        | 选择不带 "required" 属性的 <input> 元素。                    |
| [:out-of-range](https://www.w3school.com.cn/cssref/selector_out-of-range.asp) | input:out-of-range    | 选择值在指定范围之外的 <input> 元素。                        |
| [:read-only](https://www.w3school.com.cn/cssref/selector_read-only.asp) | input:read-only       | 选择指定了 "readonly" 属性的 <input> 元素。                  |
| [:read-write](https://www.w3school.com.cn/cssref/selector_read-write.asp) | input:read-write      | 选择不带 "readonly" 属性的 <input> 元素。                    |
| [:required](https://www.w3school.com.cn/cssref/selector_required.asp) | input:required        | 选择指定了 "required" 属性的 <input> 元素。                  |
| [:root](https://www.w3school.com.cn/cssref/selector_root.asp) | root                  | 选择元素的根元素。                                           |
| [:target](https://www.w3school.com.cn/cssref/selector_target.asp) | #news:target          | 选择当前活动的 #news 元素（单击包含该锚名称的 URL）。        |
| [:valid](https://www.w3school.com.cn/cssref/selector_valid.asp) | input:valid           | 选择所有具有有效值的 <input> 元素。                          |
| [:visited](https://www.w3school.com.cn/cssref/selector_visited.asp) | a:visited             | 选择所有已访问的链接。                                       |

### 4. 伪元素选择器

>   CSS 伪元素用于设置元素指定部分的样式。

-   `::first-line`：选择文本的首行，只能应用于块级元素。
-   `::first-letter`：选择文本首字母。
-   `::after`：在元素之后插入东西。
-   `::before`：在元素之后插入东西
-   `::selection`：选择选中的元素

### 5. 属性选择器

>   设置带有特定属性或属性值的 HTML 元素的样式。

-   `元素[属性]{}`

```css
/* 选择有class属性的a标签 */
a[class] {
}

/* 选择class属性完全等于"hhby"的a标签 */
a[class="hhby"] {
}

/* 选择class属性的值包含"hhby"这个单词的a标签 */
a[class~="hhby"] {
}

/* 选择class属性以"hh"开头的a标签 */
a[class^="hh"] {
}

/* 选择class属性以"by"结尾的a标签 */
a[class$="by"] {
}

/* 选择class属性包含"by"部分的a标签 */
a[class*="hb"] {
}
```

### 6. 选择器优先级

-   **==!important >> 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性==**

-   同一级别中后写的会覆盖先写的样式

-   组合在一起时可以用权值计算

>   行内样式的权值为 1000
>   ID 选择器的权值为 100
>   Class 类选择器的权值为 10
>   HTML 标签选择器的权值为 1
>   我们可以把选择器中规则对应做加法，比较权值，如果权值相同那就后面的覆盖前面的了

## 五、CSS美化网页

### 1. 字体相关

### 2. 文本相关

### 3. 链接相关

### 4. 列表相关

### 5. 边框相关

### 6. 边距相关

### 7. 图片相关

### 8. 颜色相关

1.  CSS中共支持140种标准颜色名。
2.  颜色使用类型大致分为3种：
    -   背景颜色：使用`background-color`定义
    -   文本颜色：使用`color`定义
    -   边框颜色：使用`border-color`定义
3.  颜色格式：
    -   RGB型：
        -   格式：`rgb(red, green, blue)`
        -   每个参数 (*red*、*green* 以及 *blue*) 定义了 0 到 255 之间的颜色强度。
    -   RGBA型：
        -   格式：`rgba(red, green, blue, alpha)`
        -   alpha 参数是介于 0.0（完全透明）和 1.0（完全不透明）之间的数字。
    -   HEX型：
        -   格式：`#rrggbb`
        -   rr（红色）、gg（绿色）和 bb（蓝色）是介于 00 和 ff 之间的十六进制值（与十进制 0-255 相同）。
    -   HSL型
        -   格式：`hsla(hue, saturation, lightness)`
        -   色相（hue）是色轮上从 0 到 360 的度数。0 是红色，120 是绿色，240 是蓝色。饱和度（saturation）是一个百分比值，0％ 表示灰色阴影，而 100％ 是全色。亮度（lightness）也是百分比，0％ 是黑色，50％ 是既不明也不暗，100％是白色。
    -   HSLA型(和HSL的关系类似于RGBA与RGB的，多一个`alpha`调整透明度)
4.  示例

```css
body {
    /* 背景颜色 */
    /* 使用标准颜色名取色 */
    background-color: aqua;
}

div {
    border-width: 3px;
    /* 使用rgb选取边框颜色*/
    border-color: rgb(22, 22, 22);
}

div > p:first-child {
    /* hsl取文本颜色 */
    color: hsl(0, 50%, 50%);
}

a {
    border: 2px solid red;
    background-color: rgba(0, 0, 0, 1);
    color: #fff;
}

p::selection {
    font-size: 100px;
    color: hsla(120, 50%, 50%, 0.5);
}
```



