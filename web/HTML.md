# HTML学习

## 一、HTML简介

### 1. 什么是HTML

-   **HTML(Hyper Text Markup Language)**：超文本标记语言
-   HTML不是一种编程语言而是一种标记语言(Markup Language)
-   标记语言是一套标记标签
-   HTML使用标记标签来描述网页

### 2. HTML标签 

-   HTML 标记标签通常被称为 HTML 标签 (HTML tag)。

-   HTML 标签是由*尖括号*包围的关键词，比如 `<html>`
-   HTML 标签通常是*成对出现*的，比如 `<b>` 和 `</b>`
-   标签对中的第一个标签是*开始标签*，第二个标签是*结束标签*
-   开始和结束标签也被称为*开放标签*和*闭合标签*
-   也有单独出现的标签如**换行标签**`<br>`称为自闭合标签
-   HTML5下的自闭合标签不加`/`(乱加可能出错)

### 3. HTML 文档(网页)

-   HTML 文档*描述网页*
-   HTML 文档*包含 HTML 标签*和纯文本
-   HTML 文档也被称为*网页*

-   web浏览器的作用就是读取HTML文档并以网页的形式显示出来

-   浏览器不会显示 HTML 标签，而是使用标签来解释页面的内容



## 二、HTML基础

### 1. 常用标签

-   结构：

    -   文档(html)：使用`<html> </html>`定义整个HTML文档，包含`<head>`、`<body>`等元素
    -   头部(head)：使用`<head> </head>`定义文档头部信息，包含`<meta>`(描述信息)和`<title>`(标题)等元素
    -   主体(body)：使用`<body> </body>`定义文档主体包含很多其他元素

    ```html
    <!-- 文章结构示例 -->
    <!--DOCTYPE：告诉浏览器使用什么规范（默认是html）-->
    <!DOCTYPE html>
    <!--语言 zh中文 en英文-->
    <html lang="zh">
    <!--head标签代表网页头部-->
    <head>
        <!--meta 描述性标签，表示用来描述网站的一些信息-->
        <!--一般用来做SEO-->
        <meta charset="UTF-8">
        <!--网站标题(浏览器标签页内容)-->
        <title>Title</title>
        <!--图标-->
        <link rel="icon" href="static/img/icon.png">
    </head>
    <!--body代表主体-->
    <body>
    <h1>标题</h1>
    <p>paragraph1</p>
    <!--水平分割线-->
    <hr>
    <p>paragraph2</p>
    hh
    <!--换行-->
    <br>
    hh
    <hr>
    <!--不换行-->
    hh
    hh
    <img src="https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/04.jpg" alt="无法加载">
    </body>
    </html>
    ```

    ![效果](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210821171730252.png)

-   标题：使用`<h1> </h1>`到`<h6> </h6>`定义
-   断落：使用`<p> </p>`定义
-   链接：使用`<a> </a>`定义
-   图像：使用`<img>`

### 2. HTML元素

-   HTML元素是指包含**开放标签和闭合标签及其中代码**在内的所有代码
-   HTML 元素以*开始标签*起始
-   HTML 元素以*结束标签*终止
-   *元素的内容*是开始标签与结束标签之间的内容
-   某些 HTML 元素具有*空内容（empty content）*
-   空元素*在开始标签中进行关闭*（以开始标签的结束而结束）
-   大多数 HTML 元素可拥有***属性***
-   HTML元素分为：**==块级元素、行内元素、行内块级元素==**

>   ​	根据CSS规范的规定，每一个网页元素都有一个display属性，用于确定该元素的类型，每一个元素都有默认的display属性值，比如div元素，它的默认display属性值为“block”，成为“块级”元素(block-level)；而span元素的默认display属性值为“inline”，称为“行内”元素。div这样的块级元素，就会自动占据一定矩形空间，可以通过设置高度、宽度、内外边距等属性，来调整的这个矩形的样子；与之相反，像“span”“a”这样的行内元素，则没有自己的独立空间，它是依附于其他块级元素存在的，因此，对行内元素设置高度、宽度、内外边距等属性，都是无效的。
>
>   **行内、块状元素区别：**
>
>   (1).块级元素会独占一行，其宽度自动填满其父元素宽度；行内元素不会独占一行，相邻的行内元素会排列在同一行里，知道一行排不下，才会换行，其宽度随元素的内容而变化
>
>   (2). 一般情况下，块级元素可以设置 width, height属性，行内元素设置width,  height无效(注意：块级元素即使设置了宽度，仍然是独占一行的)
>
>   (3).块级元素可以设置margin 和 padding.  行内元素的水平方向的padding-left,padding-right,margin-left,margin-right 都产生边距效果，但是竖直方向的padding-top,padding-bottom,margin-top,margin-bottom都不会产生边距效果。（水平方向有效，竖直方向无效）

### 3. HTML属性

-   HTML 标签可以拥有*属性*。属性提供了有关 HTML 元素的*更多的信息*。

-   属性总是以名称/值对的形式出现，比如：*name="value"*。

-   属性总是在 HTML 元素的*开始标签*中规定。

## 三、页面结构

### 1. 头部元素

-   `<head>` 元素是所有头部元素的容器。`<head>` 内的元素可包含脚本，指示浏览器在何处可以找到样式表，提供元信息，等等。
-   以下标签都可以添加到 head 部分：`<title>、<base>、<link>、<meta>、<script> 以及 <style>`。

1.  `<title>`元素：

    title 元素用来定义HTML标题在所有 HTML/XHTML 文档中都是必需的。

    title 元素能够：

    -   定义浏览器工具栏中的标题
    -   提供页面被添加到收藏夹时显示的标题
    -   显示在搜索引擎结果中的页面标题

2.  `<base>`元素：

     base标签为页面上的所有链接规定默认地址或默认目标（target）

3.  `<link>`元素：

    `<link> `标签定义文档与外部资源之间的关系。

    `<link>` 标签最常用于连接样式表：`<link rel="stylesheet" type="text/css" href="mystyle.css">`

4.  `<style>`元素

    `<style>` 标签用于为 HTML 文档定义样式信息。

5.  `<meta>`元素

    元数据（metadata）是关于数据的信息。

    `<meta>` 标签提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。

    典型的情况是，meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。

    `<meta>` 标签始终位于 head 元素中。

    元数据可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），编码，或其他 web 服务。

6.  `<script>`元素

    `<script>` 标签用于定义客户端脚本，比如 JavaScript。

### 2. 主体元素

-   使用`<body>`元素定义HTML文档主体，常常包含`<header> <footer> <seciton> <article> <aside> <nav>`等元素。

| 元素名  | 描述                                               |
| ------- | -------------------------------------------------- |
| header  | 标题头部区域的内容（用于页面或者页面中的一块区域） |
| footer  | 标记脚部区域的内容（用于整个页面或页面的一块区域） |
| section | Web页面中的一块独立区域                            |
| article | 独立的文章内容                                     |
| aside   | 相关内容或应用                                     |
| nav     | 导航类辅助内容                                     |

## 四、标签具体

### 1. 标题

>   **标题很重要**
>
>   请确保将 HTML heading 标签只用于标题。不要仅仅是为了产生粗体或大号的文本而使用标题。
>
>   搜索引擎使用标题为您的网页的结构和内容编制索引。
>
>   因为用户可以通过标题来快速浏览您的网页，所以用标题来呈现文档结构是很重要的。
>
>   应该将 h1 用作主标题（最重要的），其后是 h2（次重要的），再其次是 h3，以此类推。

-   标题（Heading）是通过 `<h1> - <h6>` 等标签进行定义的。

- `<h1>` 定义最大的标题。`<h6>` 定义最小的标题。

-   浏览器会自动地在标题的前后添加空行。
-   默认情况下，HTML 会自动地在块级元素前后添加一个额外的空行，比如段落、标题元素前后。
-   可以使用`<hr>`水平线来分割小节

### 2. 段落

-   段落是通过 `<p>`标签定义的。
-   浏览器会自动地在段落的前后添加空行。（ `<p>` 是块级元素）

-   可以使用`<br>`来换行

### 3. 文本格式化

| [`<b>`](https://www.w3school.com.cn/tags/tag_font_style.asp) | 定义粗体文本。                                               |
| :----------------------------------------------------------: | ------------------------------------------------------------ |
| [`<big>`](https://www.w3school.com.cn/tags/tag_font_style.asp) | 定义大号字。                                                 |
| [`<em>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义着重文字。                                               |
| [`<i>`](https://www.w3school.com.cn/tags/tag_font_style.asp) | 定义斜体字。                                                 |
| [`<smalll>`](https://www.w3school.com.cn/tags/tag_font_style.asp) | 定义小号字。                                                 |
| [`<strong>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义加重语气。                                               |
|   [`<sub>`](https://www.w3school.com.cn/tags/tag_sup.asp)    | 定义下标字。                                                 |
|   [`<sup>`](https://www.w3school.com.cn/tags/tag_sup.asp)    | 定义上标字。                                                 |
|   [`<ins>`](https://www.w3school.com.cn/tags/tag_ins.asp)    | 定义插入字。                                                 |
|   [`<del>`](https://www.w3school.com.cn/tags/tag_del.asp)    | 定义删除字。                                                 |
|   [`<s>`](https://www.w3school.com.cn/tags/tag_strike.asp)   | *不赞成使用。*使用 `<del>` 代替。                            |
| [`<strike>`](https://www.w3school.com.cn/tags/tag_strike.asp) | *不赞成使用。*使用 `<del>` 代替。                            |
|     [`<u>`](https://www.w3school.com.cn/tags/tag_u.asp)      | *不赞成使用。*使用样式（style="text-decoration: underline"）代替。 |

### 4. 计算机输出标签

| [`<code>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义计算机代码。                  |
| :----------------------------------------------------------: | --------------------------------- |
| [`<kbd>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义键盘码。                      |
| [`<samp>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义计算机代码样本。              |
| [`<tt>`](https://www.w3school.com.cn/tags/tag_font_style.asp) | 定义打字机代码。                  |
| [`<var>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义变量。                        |
|   [`<pre>`](https://www.w3school.com.cn/tags/tag_pre.asp)    | 定义预格式文本。                  |
|                         `<listing>`                          | *不赞成使用。*使用 `<pre>`代替。  |
|                        `<plaintext>`                         | *不赞成使用。*使用 `<pre>` 代替。 |
|                           `<xmp>`                            | *不赞成使用。*使用 `<pre>` 代替。 |

### 5. 引用和术语定义

|  [`<abbr>`](https://www.w3school.com.cn/tags/tag_abbr.asp)   | 定义缩写。         |
| :----------------------------------------------------------: | ------------------ |
| [`<acronym>`](https://www.w3school.com.cn/tags/tag_acronym.asp) | 定义首字母缩写。   |
| [`<address>`](https://www.w3school.com.cn/tags/tag_address.asp) | 定义地址。         |
|   [`<bdo>`](https://www.w3school.com.cn/tags/tag_bdo.asp)    | 定义文字方向。     |
| [`<blockquote>`](https://www.w3school.com.cn/tags/tag_blockquote.asp) | 定义长的引用。     |
|     [`<q>`](https://www.w3school.com.cn/tags/tag_q.asp)      | 定义短的引用语。   |
| [`<cite>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义引用、引证。   |
| [`<dfn>`](https://www.w3school.com.cn/tags/tag_phrase_elements.asp) | 定义一个定义项目。 |

### 6. HTML颜色

-   跨平台安全色

![image-20210825180847661](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/image-20210825180847661.png)

### 7. 链接

-   重要属性：

    -   `href`：链接
    -   `name`：锚点，现在被`id`取代
    -   `target`：跳转方式，默认当前页面(`_self`)跳转，`target="_blank"`时在新页面打开

-   示例：

    ```html
    <a href="https://www.baidu.com" id="baidu" target="_blank">baidu</a>
    <a href="http://116.62.195.199:8080" id="hhby" target="_blank">hhby</a>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <a href="#baidu">gobaidu</a>
    ```

### 8. 图像

-   重要属性：

    -   `src`：源，图像路径，可以是本地也可以是网络
    -   `alt`：替换文字，当图片加载失败时显示该图片
    -   `align`：对齐方式有`bottom(默认)，middle，top，left，right`
    -   `height，width`：尺寸
    -   `usemap`：使用`map`创建映射

-   示例：

    ```html
    <p>hh
        <img alt="星系团" src="https://www.w3school.com.cn/i/eg_planets.jpg" usemap="#hh">
        hh</p>
    <map id="hh" name="hh">
        <!--coords:可点击区域，圆心+半径  shape：区域形状(circle or react)-->
        <area alt="hh" coords="180,139,14" href="./a.html" shape="circle" target="_blank">
    </map>
    ```

### 9. 表格

```	html
<!--使用table定义表格-->
<table>
    <!--使用tr定义表格行-->
    <tr>
        <!--使用th定义表格标题-->
        <th>head</th>
    </tr>
    <tr>
        <!--使用td定义表格单元-->
        <td></td>
    </tr>
</table>
```

-   特殊属性：`rowspan`行合并，`colspan`列合并，`bolder`定义表格边框

-   示例：

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>table</title>
    </head>
    <body>
    <table border="1">
        <tr>
            <th colspan="10">head</th>
        </tr>
        <tr>
            <td rowspan="2">1</td>
            <td>2</td>
            <td>3</td>
            <td>4</td>
            <td>5</td>
            <td>6</td>
            <td>7</td>
            <td>8</td>
            <td>9</td>
            <td>10</td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </table>
    </body>
    </html>
    ```

### 10. 列表

-   无序列表：以`<ul> </ul>`开头，包含`<li> </li>`的列表

-   有序列表：以`<ol> </ol>`开头，包含`<li> </li>`的列表

-   自定义列表：以`<dl> </dl>`开头，包含`<dt> </dt>`以及`<dd> </dd>`的列表

-   示例：

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>list</title>
    </head>
    <body>
    <h4>Unordered List</h4>
    <ul>
        <li>hh</li>
        <li>by</li>
        <li>xx</li>
    </ul>
    <h4>Ordered List</h4>
    <ol>
        <li>hh</li>
        <li>bt</li>
        <li>ss</li>
    </ol>
    <dl>
        <dt>number</dt>
        <dd>1</dd>
        <dd>2</dd>
        <dt>word</dt>
        <dd>hhby</dd>
    </dl>
    </body>
    </html>
    ```

### 11. 视频、音频

-   使用`<video></video>`定义视频，使用`<audio></audio>`定义音频

-   示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>媒体元素</title>
</head>
<body>
<!--视频
		src 资源路径
        controls 控制面板
        autoplay 自动播放
-->
<video src="xxx/xxx/xxx" controls autoplay></video>
<!--音频-->
<audio src="xxx/xxx/xxx" controls autoplay></audio>
</body>
</html>
```

### 12. 内联框架

-   使用`<iframe src="URL"></iframe>`定义

-   可以添加`name`在内联标签内部打开链接(使用a标签的target)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>iframe</title>
</head>
<body>
<a href="http://116.62.195.199:8080/" target="wlq-ecs">hhby</a>
<iframe src="./a.html"  name="wlq-ecs" width="200" height="200" frameborder="0"></iframe>
</body>
</html>
```

### 13. **==表单(重点)==**

1.  表单(form)：

    -   使用`<form>`标签定义HTML表单，HTML 表单用于收集用户输入。

    -   `<form>`元素内常常包含不同类型的表单元素，如`<input>(输入)、<select>(下拉列表)、<button>(按钮)等`

    -   常用属性：

        -   `action`属性：action定义在提交表单时执行的动作(即提交的目的地)。向服务器提交表单的通常做法是使用提交按钮。通常，表单会被提交到 web 服务器上的网页。
        -   `method`属性：method规定在提交表单时所用的 HTTP 方法（*GET* 或 *POST*）。

        >   ### 关于 GET 的注意事项：
        >
        >   -   以名称/值对的形式将表单数据追加到 URL
        >   -   永远不要使用 GET 发送敏感数据！（提交的表单数据在 URL 中可见！）
        >   -   URL 的长度受到限制（2048 个字符）
        >   -   对于用户希望将结果添加为书签的表单提交很有用
        >   -   GET 适用于非安全数据，例如 Google 中的查询字符串
        >
        >   ### 关于 POST 的注意事项：
        >
        >   -   将表单数据附加在 HTTP 请求的正文中（不在 URL 中显示提交的表单数据）
        >   -   POST 没有大小限制，可用于发送大量数据。
        >   -   带有 POST 的表单提交无法添加书签
        >
        >   **提示：**如果表单数据包含敏感信息或个人信息，请务必使用 POST！

        -   属性列表

        | 属性           | 描述                                                       |
        | :------------- | :--------------------------------------------------------- |
        | accept-charset | 规定在被提交表单中使用的字符集（默认：页面字符集）。       |
        | action         | 规定向何处提交表单的地址（URL）（提交页面）。              |
        | autocomplete   | 规定浏览器应该自动完成表单（默认：开启）。                 |
        | enctype        | 规定被提交数据的编码（默认：url-encoded）。                |
        | method         | 规定在提交表单时所用的 HTTP 方法（默认：GET）。            |
        | name           | 规定识别表单的名称（对于 DOM 使用：document.forms.name）。 |
        | novalidate     | 规定浏览器不验证表单。                                     |
        | target         | 规定 action 属性中地址的目标（默认：_self）。              |

2.  表单元素：

    -   `<input>`元素：最重要的表单元素是 `<input>` 元素。`<input>` 元素根据不同的`type`属性，可以变化为多种形态。
    -   `<select>`元素：下拉列表元素，使用`<option>`元素定义选项，默认选择第一项，可以使用`<selected>`选项定义默认选项。

    ```html
    <label for="city">城市</label>
    <select name="city" id="city">
        <option value="beijing">北京</option>
        <option value="shanghai">上海</option>
        <option value="guangzhou">广州</option>
        <option value="shenzhen">深圳</option>
        <option value="suzhou" selected>苏州</option>
    </select>
    ```

    -   `<button>`元素：按钮元素

3.  利用`<fieldset>`标签组合表单元素

```html
<form action="./a.html" method="get" target="_blank">
    <fieldset>
        <!-- 利用legend设置标题 -->
        <legend>fieldset test</legend>
        ...
    </fieldset>
</form>
```

4.  `<input>`元素详解：
    -   常用属性：
        -   `value`：输入字段初始值
        -   `readonly`：规定输入字段只读(不可修改)
        -   `disabled`：规定输入字段不可点击，不可提交
        -   `size`：规定输入字段的长度(以字符计)
        -   `maxlength`：规定输入字段的最大长度
        -   `autocomplete`：属性规定表单或输入字段是否应该自动完成。当自动完成开启，浏览器会基于用户之前的输入值自动填写值(会覆盖表单的该属性)
        -   `autofocus`：规定当页面加载时` <input>` 元素应该自动获得焦点。
        -   `form`：属性规定 `<input>`元素所属的一个或多个表单。如需引用一个以上的表单，请使用空格分隔的表单 id 列表
        -   `formaction`：规定当提交表单时处理该输入控件的文件的 URL。属性覆盖 `<form>` 元素的 action 属性。 属性适用于 `type="submit"`以及 `type="image"`
        -   formenctype：规定当把表单数据（form-data）提交至服务器时如何对其进行编码（仅针对 `method="post"`的表单）。
        -   `formmethod`：定义用以向 action URL 发送表单数据（form-data）的 HTTP 方法。
        -   `formnovalidate`：定在提交表单时不对 `<input>` 元素进行验证。
        -   `list`：list 属性引用的 `<datalist>` 元素中包含了 `<input>` 元素的预定义选项。
        -   `min 和 max`：min 和 max 属性规定 `<input>` 元素的最小值和最大值。适用于如需输入类型：`number、range、date、datetime、datetime-local、month、time 以及 week`。
        -   `multiple`：如果设置，则规定允许用户在`<input>`元素中输入一个以上的值。适用于`type`为`file`或`email`的情况。
        -   `pattern (regexp)`：属性规定用于检查`<input>`元素值的正则表达式。
        -   `placeholder`：用以描述输入字段预期值的提示。
        -   `required`：规定在提交表单之前必须填写输入字段。
        -   `step`：规定`<input>`元素的合法数字间隔。
    -   常见类型(type)：
        -   `password`:密码输入框
        -   `submit`:提交按钮
        -   `radio`:单选框
        -   `checkbox`:多选框
        -   `button`:按钮
        -   `color`:颜色选择器
        -   `date`:日期
        -   `datetime-local`:本地时间
        -   `email`:邮箱
        -   `month`:月份
        -   `number`:数字
        -   `range`:范围滑动条
        -   `search`:搜索框
        -   `tel`:电话
        -   `time`:时间
        -   `url`:链接
        -   `week`:周

## 五、属性具体

### 1. HTML样式

-   使用`style="name1:value1; name2:value2; ..."`的样式属性来定义标签的样式

### 2. HTML类

-   使用`class`定义元素的类属性，类名可以有多个，用空格分开，类名可以重复使用，类名不能以数字开头。

```html
<div class="a b c">
    ...
</div>
```

### 3. HTML ID

-   使用`id`定义元素id，每个id在整个HTML文档中唯一，不能重复

