# CSS学习

## 一、CSS简介

-   CSS 是一种描述 HTML 文档样式的语言。

-   CSS指的是层叠样式表 (Cascading Style Sheets)
-   CSS 描述了如何在屏幕、纸张或其他媒体上显示 HTML 元素
-   CSS 节省了大量工作。它可以同时控制多张网页的布局
-   外部样式表存储在 CSS 文件中

-   CSS发展史: 

    -   CSS1.0
    -   CSS2.0: DIV(块)+CSS，HTML与CSS结构分离的思想，网页变得简单，SEO
    -   CSS2.1: 浮动，定位
    -   CSS3.0: 圆角、阴影、动画…浏览器兼容性~

-   优势: 

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

-   在相同样式的情况下，根据导入方式不同，样式的优先级如下所示(不包含`! important`的情况): 
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

-   CSS 规则集(rule-set)由选择器和声明块组成: 

![image-20210915094939561](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210915094939561.png)

-   选择器指向您需要设置样式的 HTML 元素。

- 声明块包含一条或多条用分号分隔的声明。

-   每条声明都包含一个 CSS 属性名称和一个值，以冒号分隔。

-   多条 CSS 声明用分号分隔，声明块用花括号括起来。
-   CSS注释由`/* */`组成

## 四、==CSS选择器==

>   CSS 选择器用于“查找”(或选取)要设置样式的 HTML 元素。
>
>   我们可以将 CSS 选择器分为五类: 
>
>   简单选择器(根据名称、id、类来选取元素)
>   组合器选择器(根据它们之间的特定关系来选取元素)
>   伪类选择器(根据特定状态选取元素)
>   伪元素选择器(选取元素的一部分并设置其样式)
>   属性选择器(根据属性或属性值来选取元素)

### 1. 简单选择器

-   元素选择器: 根据元素名称进行选择
    -   语法: `元素名称 {...}`
-   类(class)选择器: 根据元素`class`属性进行选择
    -   语法: `.classname {...}`
-   多类选择器: 可以选择包含多个类的元素
    -   语法: `.class1.class2 {...}`
-   id选择器: 根据元素`id`属性进行选择，选择唯一元素
    -   语法: `#idName {...}`
-   通用选择器: 选择所有元素的选择器
    -   语法: `* {...}`
-   分组选择器: 将样式相同的**元素组合器**结合起来
    -   语法: `元素1, 元素2, ...{...}`

### 2. 组合器选择器

>   组合器是解释选择器之间关系的某种机制。
>
>   CSS 选择器可以包含多个简单选择器。在简单选择器之间，我们可以包含一个组合器。
>
>   CSS 中有四种不同的组合器: 
>
>   后代选择器 (空格)
>   子选择器 (>)
>   相邻兄弟选择器 (+)
>   通用兄弟选择器 (~)

-   后代选择器: 后代选择器匹配属于指定元素后代的所有元素。
    -   语法: ` div p {...}`(div下所有p元素)
-   子选择器: 匹配属于指定元素子元素的所有元素。
    -   语法: `div > p {...}`(div的子元素p)
-   相邻兄弟选择器: 匹配所有作为指定元素的相邻同级的元素。兄弟(同级)元素必须具有相同的父元素，“相邻”的意思是“紧随其后”。
    -   语法: `div + p {...}`(具有相同父元素的相邻的div和p元素)
-   通用兄弟选择器: 匹配属于指定元素的同级元素的所有元素。
    -   语法: `div ~ p {...}`(与div同级的所有p元素)

### 3. 伪类选择器

>   伪类用于定义元素的特殊状态。

1.  常用伪类

    -   `:hover`: 悬浮伪类，选择鼠标悬浮在上的元素
        -   语法: `element:hover{...}`

    -   锚伪类: 

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
    注意: a:hover 必须在 CSS 定义中的 a:link 和 a:visited 之后，才能生效！a:active 必须在 CSS 定义中的 a:hover 之后才能生效！伪类名称对大小写不敏感。
    */
    ```

    -   `:first-child`:与指定的元素匹配: 该元素是另一个元素的第一个子元素。

        -   语法: 

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

-   `::first-line`: 选择文本的首行，只能应用于块级元素。
-   `::first-letter`: 选择文本首字母。
-   `::after`: 在元素之后插入东西。
-   `::before`: 在元素之后插入东西
-   `::selection`: 选择选中的元素

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

>   在 CSS 中，有五个通用字体族: 
>
>   -   衬线字体(Serif)- 在每个字母的边缘都有一个小的笔触。它们营造出一种形式感和优雅感。(在计算机屏幕上，无衬线字体被认为比衬线字体更易于阅读。)
>   -   无衬线字体(Sans-serif)- 字体线条简洁(没有小笔画)。它们营造出现代而简约的外观。
>   -   等宽字体(Monospace)- 这里所有字母都有相同的固定宽度。它们创造出机械式的外观。
>   -   草书字体(Cursive)- 模仿了人类的笔迹。
>   -   幻想字体(Fantasy)- 是装饰性/俏皮的字体。
>
>   所有不同的字体名称都属于这五个通用字体系列之一。

-   `font-family`: 应包含多个字体名称作为“后备”系统，以确保浏览器/操作系统之间的最大兼容性。请以您需要的字体开始，==并以通用系列结束==(如果没有其他可用字体，则让浏览器选择通用系列中的相似字体)。字体名称应以逗号分隔。
    -   语法: `[ <family-name> | <generic-family> ]#  <family-name> = <string> | <custom-ident>+ <generic-family> = serif | sans-serif | cursive | fantasy | monospace`

-   `font-style`: 字体样式，常用来选择斜体`italic`

    -   语法: `normal | italic | oblique <angle>?`

-   `font-weight`: 指定字体的粗细(1~1000)也可以是`bold`、`ligher`、`bolder`等值。

-   `font-variant`: 字体变体，指定是否以 `small-caps` 字体(小型大写字母)显示文本。在 small-caps 字体中，所有小写字母都将转换为大写字母。但是，转换后的大写字母的字体大小小于文本中原始大写字母的字体大小。

-   `font-size`: 设置文本的大小。

    >   在网页设计中，能够管理文本大小很重要。但是，不应使用调整字体大小来使段落看起来像标题，或是使标题看起来像段落。
    >
    >   font-size 值可以是绝对或相对大小。
    >
    >   绝对尺寸(长度): 
    >
    >   -   将文本设置为指定大小
    >   -   不允许用户在所有浏览器中更改文本大小(可访问性不佳)
    >   -   当输出的物理尺寸已知时，绝对尺寸很有用
    >
    >   相对尺寸(百分比): 
    >
    >   -   设置相对于周围元素的大小
    >   -   允许用户在浏览器中更改文本大小
    >
    >   **注释: **如果您没有指定字体大小，则普通文本(如段落)的默认大小为 16px(16px = 1em)

-   `font`属性是以下属性的简写属性(顺序可变): 

    -   font-style
    -   font-variant
    -   font-weight
    -   font-size/line-height
    -   font-family

    >   **font-size** 和 **font-family** 的值是必需的。如果缺少其他值之一，则会使用其默认值。

### 2. 文本相关

-   `color`: 文本颜色

-   `text-align`: 文本水平对齐，可选`left`、`right`、`center`、`justify`(两端对齐)等。

-   `vertical-align`: 文本垂直对齐，可选`top`、`middle`、`bottom`等。

-   `direction` : 文本方向，可选`ltr`(left to right)、`rtl`(right to light)

-   `unicodebini`: 与direction属性一起确定文档中双向文本的处理方式，配合`direction`使用`bidi-override`

-   `text-decoration`: 文本装饰，常使用`text-decoration: none`来去除链接下划线，是缩写。可选属性: 

    -   语法: <`text-decoration-line`> || <`text-decoration-style`> || <`text-decoration-color`> || <`text-decoration-thickness`>
    -   顺序可变，其中`text-decoration-line`有`overline`(上划线)、`underline`、`line-through`(中划线)。
    -   其他3个属性和[`border`](#6. 边距相关)类似。

-   `text-transform`: 文本转换，可选`uppercase`(全部大写)、`lowercase`(全部小写)、`capitalize`(首字母大写)

-   `text-indent`: 文本缩进，指定第一行缩进。值可以直接是长度

    -   语法: `<length-percentage> && hanging(悬浮)? && each-line(每一行)?`
          		`<length-percentage> = <length> | <percentage>`

-   `letter-spacing`: 字母间距，可以直接是长度或是`normal`

    -   语法: `normal | <length>`

-   `word-sapcing`: 字间距，同上

-   `line-height`: 行高，数字代表行高为字号*数字

    -   语法: `normal | <number> | <length> | <percentage>`

-   `white-space`: 属性指定元素内部空白的处理方式。

    -   语法: `normal | pre | nowrap | pre-wrap | pre-line | break-spaces`

    >   normal - 空白序列被折叠。 源中的换行符的处理方式与其他空格相同。 必要时断行以填充行框。  
    >
    >   nowrap – 像normal一样折叠空白，但抑制源中的换行符(文本换行)。  
    >
    >   pre – 保留空白序列。 仅在源和元素中的换行符处换行。  
    >
    >   pre-wrap – 保留空白序列。 在换行符、以及根据需要填充行框时将换行。  
    >
    >   pre-line – 空白序列被折叠。 在换行符、 以及根据需要填充行框时将换行。  
    >
    >   break-spaces – 行为与pre-wrap相同，除了: 
    >   任何保留的空白序列总是占用空间，包括在行尾。
    >   每个保留的空白字符之后都存在换行机会，包括空白字符之间。
    >   这种保留的空间占用空间并且不会挂起，从而影响盒子的内在大小(最小内容大小和最大内容大小)。

-   `text-shadow`: 为文本添加阴影。
    -   语法: `none | <shadow-t>#<shadow-t> = [ <length>{2,3} && <color>? ] <color> = <rgb()> | <rgba()> | <hsl()> | <hsla()> |  <hex-color> | <named-color> | currentcolor | <deprecated-system-color>`(2个长度+阴影颜色)

### 3. 链接相关

-   链接可以使用任何 CSS 属性(例如 color、font-family、background 等)来设置样式。
-   可以根据链接处于什么状态来设置链接的不同样式。四种链接状态(顺序必须相同)分别是: 
    -   a:link - 正常的，未访问的链接
    -   a:visited - 用户访问过的链接
    -   a:hover - 用户将鼠标悬停在链接上时
    -   a:active - 链接被点击时

### 4. 列表相关

-   `list-style-type`: 属性指定列表项标记的类型。

    >   <custom-ident> – 与@counter-style或预定义样式之一的值匹配的标识符:   
    >   symbols() – 定义列表的匿名样式。  
    >   <string> – 指定的字符串将用作项目的标记。  
    >   none – 不显示项目标记。  
    >   disc – 一个实心圆(默认值)。  
    >   circle - 空心圆。  
    >   square – 填充的正方形。  
    >   decimal - 十进制数，从 1 开始。  
    >   cjk-decimal – cjk-decimal十进制数。  
    >   decimal-leading-zero - 十进制数，由初始零填充。  
    >   lower-roman – 小写罗马数字。  
    >   upper-roman – 大写罗马数字。  
    >   lower-greek – 小写古典希腊语。  
    >   lower-alpha, lower-latin – 小写 ASCII 字母。  
    >   upper-alpha, upper-latin – 大写 ASCII 字母。  
    >   arabic-indic, -moz-arabic-indic – 阿拉伯-印度数字。  
    >   armenian -传统的亚美尼亚编号。  
    >   孟加拉语bengali, -moz-bengali – 孟加拉语编号。  
    >   cambodian/khmer -柬埔寨/高棉编号。  
    >   cjk-earthly-branch, -moz-cjk-earthly-branch – 汉族“地支”序数。  
    >   cjk-heavenly-stem, -moz-cjk-heavenly-stem – 汉族“天干”序数。  
    >   cjk-ideographic – 与trad-chinese-informal相同。
    >
    >   devanagari, -moz-devanagari – 梵文编号。  
    >   ethiopic-numeric – 埃塞俄比亚编号。  
    >   georgian – 传统的格鲁吉亚编号。  
    >   gujarati, -moz-gujarati – 古吉拉特语编号。  
    >   gurmukhi, -moz-gurmukhi – Gurmukhi 编号。  
    >   hebrew -传统希伯来语编号  
    >   hiragana - 字典顺序平假名字母。  
    >   hiragana-iroha – Iroha 阶 平假名刻字  
    >   japanese-formal – 用于法律或财务文件的日本正式编号。 汉字的设计使得它们不能被修改为看起来像另一个正确的。  
    >   japanese-informal – 日本非正式编号。  
    >   kannada, -moz-kannada – 卡纳达语编号。  
    >   katakana – 字典顺序片假名字母  
    >   katakana-iroha – Iroha 顺序 片假名刻字  
    >   korean-hangul-formal – 韩文编号。  
    >   korean-hanja-formal – 正式的韩文编号。  
    >   korean-hanja-informal – 韩文汉字编号。  
    >   lao, -moz-lao – 老挝语编号。  
    >   lower-armenian亚美尼亚语 - 小写亚美尼亚语编号。  
    >   malayalam, -moz-malayalam语malayalam, -moz-malayalam – 马拉雅拉姆语编号。  
    >   mongolian – 蒙古文编号。  
    >   myanmar, -moz-myanmar – 缅甸(缅甸)编号。  
    >   oriya, -moz-oriya – 奥里亚语编号。  
    >   persian - 波斯语编号  
    >   simp-chinese-formal – 简体中文正式编号。  
    >   simp-chinese-informal – 简体中文非正式编号。  
    >   tamil语——泰米尔语编号。  
    >   telugu, -moz-telugu固语telugu, -moz-telugu – 泰卢固语编号。  
    >   thai, -moz-thai – 泰语编号。
    >
    >   tibetan ——藏语编号。  
    >   trad-chinese-formal – 繁体中文正式编号。  
    >   trad-chinese-informal – 繁体中文非正式编号。  
    >   upper-armenian Armenian – 传统的大写亚美尼亚语编号。  
    >   disclosure-open - 表示disclosure-open诸如<details>类的披露小部件的符号。  
    >   disclosure-closed - 表示公开小部件(例如<details>已关闭的符号。

-   `list-style-position`: 属性指定列表项标记(项目符号)的位置。

    -   `outside`表示项目符号点将在列表项之外。`inside`表示项目符号将在列表项内。由于它是列表项的一部分，因此它将成为文本的一部分，并在开头推开文本。

-   `list-style` 属性是一种简写属性。它用于在一条声明中设置所有列表属性。

    -   list-style-type(如果指定了 list-style-image，那么在由于某种原因而无法显示图像时，会显示这个属性的值)
    -   list-style-position(指定列表项标记应显示在内容流的内部还是外部)
    -   list-style-image(将图像指定为列表项标记)

### 5. 边框相关

1.  常见属性

-   `border-style`: 指定要显示的边框类型。可以设置一到四个值(用于上边框、右边框、下边框和左边框)，允许以下类型。(上右下左，下同上，左同右)

    >   **注意: **除非设置了 **`border-style`** 属性，否则其他 CSS 边框属性都不会有任何作用！

    -   `dotted`:  定义点线边框
    -   `dashed`: 定义虚线边框
    -   `solid`: 定义实线边框
    -   `double`: 定义双边框
    -   `groove`: 定义 3D 坡口边框。效果取决于 border-color 值
    -   `ridge`: 定义 3D 脊线边框。效果取决于 border-color 值
    -   `inset`: 定义 3D inset 边框。效果取决于 border-color 值
    -   `outset`: 定义 3D outset 边框。效果取决于 border-color 值
    -   `none`: 定义无边框
    -   `hidden`:  定义隐藏边框

-   `border-width`: 指定边框宽度，可以设置一到四个值(效果同上)

-   `border-color`: 指定边框颜色，可以设置一到四个值(效果同上)，如果未设置将继承元素颜色。

-   `border-radius`: 指定边框圆角半径，可以设置一到四个值(效果同上)

2.  简写属性

-   `border`: 将`style、width、color`，`style`不可少，简写中每个属性只能写一个值。

3.  示例

```css
/* 测试边框样式 */
/*
 * style: a       上右下左=a
 * style: a b     上下=a 左右=b
 * style: a b c   上=a 左右=b 下=c
 * style: a b c d 上=a 右=b 下=c 左=d
 */
h1 {
    border-style: solid dotted double inset;
    border-width: 10px 20px 30px 40px;
    border-radius: 5px 8px;
    color: skyblue;
    font-size: 30px;
}

h2 {
    /* 简写 */
    border: solid 5px red;
}
```

4.  边框属性表

| 属性                                                         | 描述                                                  |
| :----------------------------------------------------------- | :---------------------------------------------------- |
| [border](https://www.w3school.com.cn/cssref/pr_border.asp)   | 简写属性，在一条声明中设置所有边框属性。              |
| [border-color](https://www.w3school.com.cn/cssref/pr_border-color.asp) | 简写属性，设置四条边框的颜色。                        |
| [border-radius](https://www.w3school.com.cn/cssref/pr_border-radius.asp) | 简写属性，可设置圆角的所有四个 border-*-radius 属性。 |
| [border-style](https://www.w3school.com.cn/cssref/pr_border-style.asp) | 简写属性，设置四条边框的样式。                        |
| [border-width](https://www.w3school.com.cn/cssref/pr_border-width.asp) | 简写属性，设置四条边框的宽度。                        |
| [border-bottom](https://www.w3school.com.cn/cssref/pr_border-bottom.asp) | 简写属性，在一条声明中设置所有下边框属性。            |
| [border-bottom-color](https://www.w3school.com.cn/cssref/pr_border-bottom-color.asp) | 设置下边框的颜色。                                    |
| [border-bottom-style](https://www.w3school.com.cn/cssref/pr_border-bottom-style.asp) | 设置下边框的样式。                                    |
| [border-bottom-width](https://www.w3school.com.cn/cssref/pr_border-bottom-width.asp) | 设置下边框的宽度。                                    |
| [border-left](https://www.w3school.com.cn/cssref/pr_border-left.asp) | 简写属性，在一条声明中设置所有左边框属性。            |
| [border-left-color](https://www.w3school.com.cn/cssref/pr_border-left-color.asp) | 设置左边框的颜色。                                    |
| [border-left-style](https://www.w3school.com.cn/cssref/pr_border-left-style.asp) | 设置左边框的样式。                                    |
| [border-left-width](https://www.w3school.com.cn/cssref/pr_border-left-width.asp) | 设置左边框的宽度。                                    |
| [border-right](https://www.w3school.com.cn/cssref/pr_border-right.asp) | 简写属性，在一条声明中设置所有右边框属性。            |
| [border-right-color](https://www.w3school.com.cn/cssref/pr_border-right-color.asp) | 设置右边框的颜色。                                    |
| [border-right-style](https://www.w3school.com.cn/cssref/pr_border-right-style.asp) | 设置右边框的样式。                                    |
| [border-right-width](https://www.w3school.com.cn/cssref/pr_border-right-width.asp) | 设置右边框的宽度。                                    |
| [border-top](https://www.w3school.com.cn/cssref/pr_border-top.asp) | 简写属性，在一条声明中设置所有上边框属性。            |
| [border-top-color](https://www.w3school.com.cn/cssref/pr_border-top-color.asp) | 设置上边框的颜色。                                    |
| [border-top-style](https://www.w3school.com.cn/cssref/pr_border-top-style.asp) | 设置上边框的样式。                                    |
| [border-top-width](https://www.w3school.com.cn/cssref/pr_border-top-width.asp) | 设置上边框的宽度。                                    |

### 6. 边距相关

1.  外边距

-   通过`margin`来定义外边距的4个值(上右下左)。

-   也可以通过`margin-top/right/bottom/left`来分别定义4个值。

-   值分为4种类型: 

    -   `length`: 以`px、pt、cm`等单位指定外边距长度。
    -   `auto`: 浏览器自动计算边距，使元素在其容器中水平居中。
    -   `inherit`: 继承父元素。
    -   `%`: 包含元素宽度的百分比计的外边距。

-   外边距合并: 当2个平行的外边距(上上、下下、左左、右右、上下、左右)相遇时会进行合并，合并后的外边距值等同于合并前较大的那个值。

    ![image-20210916101627740](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210916101627740.png)

2.  内边距

-   使用`padding`定义，其他同上(无合并)。

3.  元素宽度(`width`)和边距的关系

-   `width`属性指定元素内容区域的宽度。内容区域是元素(盒模型)的内边距、边框和外边距内的部分。因此，如果元素拥有指定的宽度，则添加到该元素的内边距会添加到元素的总宽度中。这通常是不希望的结果(定义的`width`与实际的元素宽度不等)。
-   可以使用`box-sizing`属性定义尺寸，可以保证边距不影响元素宽度，但会影响内容宽度。

### 7. 表格相关

-   `border-collapse`: 设置表格边框折叠为单一边框，可选属性`collapse`(折叠)、`separate`(分开)
-   如需控制边框和表格内容之间的间距，请在 `<td>` 和 `<th>` 元素上使用 padding 属性

| 属性                                                         | 描述                                           |
| :----------------------------------------------------------- | :--------------------------------------------- |
| [border](https://www.w3school.com.cn/cssref/pr_border.asp)   | 简写属性。在一条声明中设置所有边框属性。       |
| [border-collapse](https://www.w3school.com.cn/cssref/pr_border-collapse.asp) | 规定是否应折叠表格边框。                       |
| [border-spacing](https://www.w3school.com.cn/cssref/pr_border-spacing.asp) | 规定相邻单元格之间的边框的距离。               |
| [caption-side](https://www.w3school.com.cn/cssref/pr_tab_caption-side.asp) | 规定表格标题的位置。                           |
| [empty-cells](https://www.w3school.com.cn/cssref/pr_tab_empty-cells.asp) | 规定是否在表格中的空白单元格上显示边框和背景。 |
| [table-layout](https://www.w3school.com.cn/cssref/pr_tab_table-layout.asp) | 设置用于表格的布局算法。                       |

### 8. 颜色相关

1.  CSS中共支持140种标准颜色名。
2.  颜色使用类型大致分为3种: 
    -   背景颜色: 使用`background-color`定义
    -   文本颜色: 使用`color`定义
    -   边框颜色: 使用`border-color`定义
3.  颜色格式: 
    -   RGB型: 
        -   格式: `rgb(red, green, blue)`
        -   每个参数 (*red*、*green* 以及 *blue*) 定义了 0 到 255 之间的颜色强度。
    -   RGBA型: 
        -   格式: `rgba(red, green, blue, alpha)`
        -   alpha 参数是介于 0.0(完全透明)和 1.0(完全不透明)之间的数字。
    -   HEX型: 
        -   格式: `#rrggbb`
        -   rr(红色)、gg(绿色)和 bb(蓝色)是介于 00 和 ff 之间的十六进制值(与十进制 0-255 相同)。
    -   HSL型
        -   格式: `hsla(hue, saturation, lightness)`
        -   色相(hue)是色轮上从 0 到 360 的度数。0 是红色，120 是绿色，240 是蓝色。饱和度(saturation)是一个百分比值，0％ 表示灰色阴影，而 100％ 是全色。亮度(lightness)也是百分比，0％ 是黑色，50％ 是既不明也不暗，100％是白色。
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

### 9. 背景相关

1.  常见属性

-   `background-color`: 指定背景颜色，可以为任何 HTML 元素设置背景颜色。
-   `background-image`: 指定背景图像，默认情况下，图像会重复，以覆盖整个元素。
    -   格式: `background-image: url(xxx)`
-   `background-repeat`: 指定背景图像重复，可设置`no-repeat`(不重复)、`repeat-x`(水平重复)、`repeat-y`(垂直重复)3种值。
-   `background-attachment`: 指定图片是否固定，可设置`fixed`(固定)，`scroll`(随页面滚动)2种值。
-   `background-position`: 指定背景图像开始的位置。
    -   格式: `background-position: [left/right/center] [top/bottom/center]`

-   `opacity`: 透明度，为元素的背景添加透明度时，其所有子元素都继承相同的透明度。

2.  简写属性

-   `background`: 按以下顺序填写，可以缺少，顺序不能乱。
    -   `background-color`
    -   `background-image`
    -   `background-repeat`
    -   `background-attachment`
    -   `background-position`

3.  背景属性表

| 属性                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| [background](https://www.w3school.com.cn/cssref/pr_background.asp) | 在一条声明中设置所有背景属性的简写属性。           |
| [background-attachment](https://www.w3school.com.cn/cssref/pr_background-attachment.asp) | 设置背景图像是固定的还是与页面的其余部分一起滚动。 |
| [background-clip](https://www.w3school.com.cn/cssref/pr_background-clip.asp) | 规定背景的绘制区域。                               |
| [background-color](https://www.w3school.com.cn/cssref/pr_background-color.asp) | 设置元素的背景色。                                 |
| [background-image](https://www.w3school.com.cn/cssref/pr_background-image.asp) | 设置元素的背景图像。                               |
| [background-origin](https://www.w3school.com.cn/cssref/pr_background-origin.asp) | 规定在何处放置背景图像。                           |
| [background-position](https://www.w3school.com.cn/cssref/pr_background-position.asp) | 设置背景图像的开始位置。                           |
| [background-repeat](https://www.w3school.com.cn/cssref/pr_background-repeat.asp) | 设置背景图像是否及如何重复。                       |
| [background-size](https://www.w3school.com.cn/cssref/pr_background-size.asp) | 规定背景图像的尺寸。                               |

### 10. 轮廓相关

-   使用`outline`定义轮廓
-   与`border`属性用法大致相同，没有`radius`但多了`outline-offset`(轮廓偏移)，并且`outline`不能分别设置四边。
-   `outline-offset`属性在元素的轮廓与边框之间添加空间。元素及其轮廓之间的空间是透明的。

-   与`border`最大的不同在于: 轮廓是在元素边框之外绘制的，并且可能与其他内容重叠。同样，轮廓也不是元素尺寸的一部分；元素的总宽度和高度不受轮廓线宽度的影响。
-   示例

```css
h5 {
    border: dotted 5px aqua;
    outline: 10px dashed aquamarine;
}

h6 {
    border: solid 1px black;
    outline: skyblue outset 20px;
    outline-offset: 10px;
}

p {
    border: solid 1px black;
    outline: skyblue solid 20px;
    outline-offset: 33px;
}
```

### 11. CSS盒模型以及高度/宽度设置

#### 1. 高度/宽度

-   `height`和`width`属性用于设置元素的高度和宽度。
-   `height`和`width`属性不包括内边距、边框或外边距。它设置的是元素内边距、边框以及外边距内的区域的高度或宽度。
-   `height`和`width`属性可设置如下值: 
    -   `auto`: 默认。浏览器计算高度和宽度。
    -   `length`: 以 px、cm 等定义高度/宽度。
    -   `%`: 以包含块的百分比定义高度/宽度。
    -   `initial`: 将高度/宽度设置为默认值。
    -   `inherit`: 从其父值继承高度/宽度。
-   `max-width`属性用于设置元素的最大宽度。可以用长度值(例如 px、cm 等)或包含块的百分比(％)来指定`max-width`(最大宽度)，也可以将其设置为 none(默认值。意味着没有最大宽度)。当浏览器窗口小于元素的最大宽度时，使用`max-width`能够改善浏览器对小窗口的处理。`max-width`会覆盖`width`。

-   属性表

| 属性                                                         | 描述                 |
| :----------------------------------------------------------- | :------------------- |
| [height](https://www.w3school.com.cn/cssref/pr_dim_height.asp) | 设置元素的高度。     |
| [max-height](https://www.w3school.com.cn/cssref/pr_dim_max-height.asp) | 设置元素的最大高度。 |
| [max-width](https://www.w3school.com.cn/cssref/pr_dim_max-width.asp) | 设置元素的最大宽度。 |
| [min-height](https://www.w3school.com.cn/cssref/pr_dim_min-height.asp) | 设置元素的最小高度。 |
| [min-width](https://www.w3school.com.cn/cssref/pr_dim_min-width.asp) | 设置元素的最小宽度。 |
| [width](https://www.w3school.com.cn/cssref/pr_dim_width.asp) | 设置元素的宽度。     |

#### 2. 盒模型

-   所有 HTML 元素都可以视为方框。在 CSS 中，在谈论设计和布局时，会使用术语“盒模型”或“框模型”。CSS 盒模型实质上是一个包围每个 HTML 元素的框。它包括: 外边距、边框、内边距以及实际的内容。下图展示了框模型: 

![image-20210916142558082](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210916142558082.png)

-   内容: 框的内容，其中显示文本和图像。
-   内边距: 清除内容周围的区域。内边距是透明的。
-   边框: 围绕内边距和内容的边框。
-   外边距: 清除边界外的区域。外边距是透明的。
-   元素框的最内部分是实际的内容，直接包围内容的是内边距。内边距呈现了元素的背景。内边距的边缘是边框。边框以外是外边距，外边距默认是透明的，因此不会遮挡其后的任何元素。
-   背景应用于由内容和内边距、边框组成的区域。
-   内边距、边框和外边距都是可选的，默认值是零。但是，许多元素将由用户代理样式表设置外边距和内边距。可以通过将元素的 margin 和 padding 设置为零来覆盖这些浏览器样式。这可以分别进行，也可以使用通用选择器对所有元素进行设置
-   元素总宽度 = 宽度 + 左内边距 + 右内边距 + 左边框 + 右边框 + 左外边距 + 右外边距
-   元素总高度 = 高度 + 上内边距 + 下内边距 + 上边框 + 下边框 + 上外边距 + 下外边距

## 六、CSS高级

### 1. ==`display`属性具体==

#### 1. 块级元素

-   块级元素总是从新行开始，并占据可用的全部宽度(尽可能向左和向右伸展)
-   例子: 
    -   `<div>`
    -   `<h1> - <h6>`
    -   `<p>`
    -   `<form>`
    -   `<header>`
    -   `<footer>`
    -   `<section>`

#### 2. 行内元素(内联元素)

-   内联元素不从新行开始，仅占用所需的宽度。
-   例子: 
    -   `<span>`
    -   `<a>`
    -   `<img>`

#### 3. `display`属性取值

>   设置元素的`display`属性仅会更改*元素的显示方式*，而不会更改元素的种类。因此，带有`display: block;` 的行内元素仍然不允许在其中包含其他块元素。

1.  常用

-   `none`: 通常与 JavaScript 一起使用，以隐藏和显示元素，而无需删除和重新创建它们。

>   元素的隐藏也可以使用`visibility: hidden;`来实现，区别是: 通过将`display`属性设置为`none`可以隐藏元素。该元素将被隐藏，并且页面将显示为好像该元素不在其中。通过`visibility`隐藏，则该元素仍将占用与之前相同的空间。元素将被隐藏，但仍会影响布局。

-   `block`: 块级元素
-   `inline`: 行内元素
-   `inline-block`: 行内块级元素

2.  表格

| 值                 | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| none               | 此元素不会被显示。                                           |
| block              | 此元素将显示为块级元素，此元素前后会带有换行符。             |
| inline             | 默认。此元素会被显示为内联元素，元素前后没有换行符。         |
| inline-block       | 行内块元素。（CSS2.1 新增的值）                              |
| list-item          | 此元素会作为列表显示。                                       |
| run-in             | 此元素会根据上下文作为块级元素或内联元素显示。               |
| compact            | CSS 中有值 compact，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| marker             | CSS 中有值 marker，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| table              | 此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。 |
| inline-table       | 此元素会作为内联表格来显示（类似 <table>），表格前后没有换行符。 |
| table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 <tbody>）。       |
| table-header-group | 此元素会作为一个或多个行的分组来显示（类似 <thead>）。       |
| table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 <tfoot>）。       |
| table-row          | 此元素会作为一个表格行显示（类似 <tr>）。                    |
| table-column-group | 此元素会作为一个或多个列的分组来显示（类似 <colgroup>）。    |
| table-column       | 此元素会作为一个单元格列显示（类似 <col>）                   |
| table-cell         | 此元素会作为一个表格单元格显示（类似 <td> 和 <th>）          |
| table-caption      | 此元素会作为一个表格标题显示（类似 <caption>）               |
| inherit            | 规定应该从父元素继承 display 属性的值。                      |

### 2. 溢出相关

-   `overflow`属性指定在元素的内容太大而无法放入指定区域时是剪裁内容还是添加滚动条。可设置以下值: 
    -   `visible`: 默认。溢出没有被剪裁。内容在元素框外渲染
    -   `hidden`: 溢出被剪裁，其余内容将不可见
    -   `scroll`: 溢出被剪裁，同时添加滚动条以查看其余内容
    -   `auto`: 与 scroll 类似，但仅在必要时添加滚动条
-   `overflow`属性仅适用于具有指定高度的块元素。
-   `overflow-x`和`overflow-y`属性规定是仅水平还是垂直地(或同时)更改内容的溢出: 
    -   overflow-x 指定如何处理内容的左/右边缘。
    -   overflow-y 指定如何处理内容的上/下边缘。

### 3. 浮动相关

>   CSS `float`属性规定元素如何浮动。
>
>   CSS `clear`属性规定哪些元素可以在清除的元素旁边以及在哪一侧浮动。

-   `float`属性用于定位和格式化内容，例如让图像向左浮动到容器中的文本那里。可以设置以下值之一: 

    -   `left`: 元素浮动到其容器的左侧
    -   `right `: 元素浮动在其容器的右侧
    -   `none`: 元素不会浮动(将显示在文本中刚出现的位置)。默认值。
    -   `inherit`: 元素继承其父级的 float 值

-   `clear`属性指定哪些元素可以浮动于被清除元素的旁边以及哪一侧。可设置以下值之一: 

    >   使用`clear`属性的最常见用法是在元素上使用了`float`属性之后。
    >
    >   在清除浮动时，应该对清除与浮动进行匹配: 如果某个元素浮动到左侧，则应清除左侧。您的浮动元素会继续浮动，但是被清除的元素将显示在其下方。

    -   `none`: 允许两侧都有浮动元素。默认值
    -   `left`: 左侧不允许浮动元素
    -   `right`: 右侧不允许浮动元素
    -   `both`: 左侧或右侧均不允许浮动元素
    -   `inherit`: 元素继承其父级的 clear 值

-   父级边框塌陷问题解决方案

    -   法一: 增加父元素高度。
    -   法二: 添加一个空`<div>`，清除浮动。
    -   法三: 在父级元素中添加`overflow`属性。
    -   法四: 使用`:after`伪类。

### 4. 定位相关

-   `position`属性规定应用于元素的定位方法的类型。有五个不同的位置值: 

    -   `static`: 静态定位，HTML 元素默认情况下的定位方式为`static`(静态)。静态定位的元素不受 top、bottom、left 和 right 属性的影响。

    -   `relative`: 相对定位，设置相对定位的元素的 top、right、bottom 和 left 属性将导致其偏离其正常位置进行调整。不会对其余内容进行调整来适应元素留下的任何空间。

    -   `fixed`: 固定定位，是相对于视口定位的，这意味着即使滚动页面，它也始终位于同一位置。 top、right、bottom 和 left 属性用于定位此元素。

    -   `absolute`: 绝对定位，对于最近的定位祖先元素进行定位(而不是相对于视口定位，如 fixed。

        然而，如果绝对定位的元素没有祖先，它将使用文档主体(body)，并随页面滚动一起移动。

    -   `sticky`: 粘性定位，根据滚动位置在相对(relative)和固定(fixed)之间切换。起先它会被相对定位，直到在视口中遇到给定的偏移位置为止然后将其“粘贴”在适当的位置(比如 position:fixed)。

-   元素其实是使用 top、bottom、left 和 right 属性定位的。但是，除非首先设置了 position 属性，否则这些属性将不起作用。根据不同的 position 值，它们的工作方式也不同。

-   在对元素进行定位时，它们可以与其他元素重叠。`z-index`属性指定元素的堆栈顺序(哪个元素应放置在其他元素的前面或后面)。元素可以设置正或负的堆叠顺序。