# JavaWeb

### 1. servlet的请求路径的映射

- 一对一: 

    ```xml
    <!--注册servlet-->
    <servlet>
        <!--servlet名字-->
        <servlet-name>hello</servlet-name>
        <!--servlet类地址-->
        <servlet-class>com.wlq.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--映射路径
    一对一映射一条-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <!--映射地址-->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    ```

- 一对多:

    ```xml
    <!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.wlq.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--映射路径
    一对多映射多条-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello1</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello2</url-pattern>
    </servlet-mapping>
    ...
    ```

- 使用通配符

    ```xml
    <!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.wlq.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--默认请求路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
    ```

- 指定后缀

    ```xml
    <!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.wlq.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--可以自定义后缀实现请求映射,但要注意.*前面不能加项目映射的路径-->
    <servlet-mapping>-->
         <servlet-name>hello</servlet-name>-->
         <url-pattern>*.hhby</url-pattern>-->
    </servlet-mapping>-->
    ```

- 优先级问题 

    - 指定了固有的映射路径优先级最高,如果找不到就会走默认的处理请求.

    ```xml
    <!--404-->
        <servlet>
            <servlet-name>error</servlet-name>
            <servlet-class>com.wlq.servlet.ErrorServlet</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>error</servlet-name>
            <url-pattern>/*</url-pattern>
        </servlet-mapping>
    ```

#### `附:web.xml文件内容`

```xml
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                      https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
  version="5.0"
  metadata-complete="true">

</web-app>

```

### 2. servletContext:上下文

- web容器在启动的时候,他会为每一个web程序都创建一个对应ServletContext对象,它代表了当前的web应用;

- 共享数据:
    - 在这个servlet中保存的数据,可以在另外一个servlet中拿到; 


- 获取初始参数:

    - 可以获取在xml中配置的初始参数

    ```xml
     <!--配置一些web应用的初始化参数-->
        <context-param>
            <param-name>url</param-name>
            <param-value>jdbc:mysql://localhost:3306/python</param-value>
        </context-param>
    ```

    ```java
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            ServletContext context = this.getServletContext();
    
            String url = context.getInitParameter("url");
            PrintWriter writer = resp.getWriter();
            writer.print(url);
    }
    ```

- 加载资源文件(properties):

    - 可以加载properties文件中的内容

        `附:类目录是指java文件夹和resources文件夹的通称,这2个文件夹的资源在运行后会被打包到同一文件夹classes下该目录称为类目录`

    ```properties
    username=root
    password=1248
    ```

    ```java
     	@Override
        protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");
            Properties properties = new Properties();
            properties.load(is);
            String username = properties.getProperty("username");
            String password = properties.getProperty("password");
    
            resp.getWriter().print("<h1>" + username + ":" + password + "</h1>");
        }
    
        @Override
        protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            doGet(req, resp);
        }
    ```

- 请求转发

    ```java
     @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        System.out.println("进入了sd4");
        //转发的请求路径
        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");
        //调用forward实现转发
        requestDispatcher.forward(req, resp);
    }
    ```

    

- [`参考1`](https://www.cnblogs.com/xzh0717/p/10638870.html#/c/subject/p/10638870.html)

- [`参考2`](https://blog.csdn.net/gavin_john/article/details/51399425)

### 3. HttpServletResponse

web服务器接收到客户端http请求,针对这个请求分别创建一个代表请求的HttpServletResquest对象,代表响应的一个HttpServletResponse对象.

- 如果要获取客户端请求服务端过来的参数:找HttpServletRequest.
- 如果要服务端给客户端响应一些信息:找HttpServletResponse.

#### 1.简单分类

- 负责向浏览器发送数据的方法

    ```java
    //写二进制数据流,位于ServletResponse接口
    public ServletOutputStream getOutputStream() throws IOException;
    //写字符文本,位于ServletResponse接口
    public PrintWriter getWriter() throws IOException;
    ```
    
- 负责向浏览器发送响应头的方法

    ```java
    //设置发送到client的字符编码为UTF-8
    public void setCharacterEncoding(String charset);
    //设置响应体内容长度
    public void setContentLength(int len);
    //设置响应体内容长度
    public void setContentLengthLong(long len);
    //给未发送的响应设置类型
    public void setContentType(String type);
    //
    ...
    ```

- 常量

    ```java
    
    
    public static final int SC_CONTINUE = 100;
    
    
    public static final int SC_SWITCHING_PROTOCOLS = 101;
    
    
    public static final int SC_OK = 200;
    
    
    public static final int SC_CREATED = 201;
    
    
    public static final int SC_ACCEPTED = 202;
    
    
    public static final int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    
    
    public static final int SC_NO_CONTENT = 204;
    
    
    public static final int SC_RESET_CONTENT = 205;
    
    
    public static final int SC_PARTIAL_CONTENT = 206;
    
    
    public static final int SC_MULTIPLE_CHOICES = 300;
    ```

#### 2.常见应用

1. 向浏览器输出消息.
2. 下载文件
    1. 获取下载文件路径
    2. 获取文件名
    3. 设置让浏览器能支持下载我们需要的东西
    4. 获取下载输入流
    5. 创建缓冲区
    6. 获取OutputStream对象
    7. 将FileOutputStream流写入到buffer缓冲区
    8. 使用OutputStream将缓冲区中的数据输出到客户端

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //1. 获取下载文件路径
    String realPath = "D:\\project\\JavaEE\\javaweb-02-servlet\\response\\target\\classes\\1.jpg";
    System.out.println("下载文件的路径" + realPath);
    //2. 获取文件名
    String filename = realPath.substring(realPath.lastIndexOf("\\") + 1);
    //3. 设置让浏览器(Content-disposition)能支持下载我们需要的东西,中文文件名用URLEncoder.encode编码,否则可能会乱码.
    resp.setHeader("Content-disposition", "attachment;filename=" + 
                   URLEncoder.encode(filename,"UTF-8"));
    //4. 获取下载输入流
    FileInputStream in = new FileInputStream(realPath);
    //5. 创建缓冲区
    int len = 0;
    byte[] buffer = new byte[1024];
    //6. 获取OutputStream对象
    ServletOutputStream out = resp.getOutputStream();
    //7. 将FileOutputStream流写入到buffer缓冲区
    while ((len = in.read(buffer)) > 0) {
        //8. 使用OutputStream将缓冲区中的数据输出到客户端
        out.write(buffer, 0, len);
    }
    in.close();
    out.close();
    }
```

3. 验证码功能

- 前端实现
- 后端实现,需要用到java图片类(Image),生成一个图片.

```java
@Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //如何让浏览器5秒自动刷新一次
        resp.setHeader("Refresh", "3");
        //在内存中创建一个图片
        BufferedImage image = new BufferedImage(800, 200, BufferedImage.TYPE_INT_RGB);
        //得到图片
        //笔
        Graphics2D g = (Graphics2D) image.getGraphics();
        //设置图片背景颜色
        g.setColor(Color.WHITE);
        //填充背景颜色
        g.fillRect(0, 0, 800, 200);
        //给图片写数据
        g.setColor(Color.BLUE);
        g.setFont(new Font(null, Font.BOLD, 40));
        g.drawString(makeNum(), 200, 100);

        //告诉浏览器这个请求用图片方式打开
        resp.setContentType("image/jpeg");
        //网站存在缓存,不让浏览器缓存
        resp.setDateHeader("expires", -1);
        resp.setHeader("Cache-Control", "no-cache");
        resp.setHeader("Pragma", "no-cache");
        //把图片写给浏览器
        ImageIO.write(image, "jpg", resp.getOutputStream());
    }

    /**
     * 生成随机数
     *
     * @return 随机数字符串
     * @author 王林清
     * @since 2021/6/7 20:47
     */
    public String makeNum() {
        Random random = new Random();
        String num = String.valueOf(random.nextInt(9999999));
        StringBuffer sb = new StringBuffer();
        //当stringBuilder位数小于7时用0填充
        for (int i = 0; i < 7 - num.length(); i++) {
            sb.append("0");
        }
        String s = num + sb;
        System.out.println(s);
        return s;
    }
```

4. 实现重定向

- 一个web资源B收到客户端A请求后,B会通知A客户端去访问另外一个web资源C,这个过程叫做重定向.

- 常见场景:

    - 用户登录

    ```java
    void sendRedirect(String var) throws IOException;
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            resp.sendRedirect("/r/img");
    }
    ```

- 重定向和转发的区别:
    - 相同点
        - 页面都会实现跳转
    - 不同点
        - 请求转发时URL不会发生变化 307
        - 重定向时URL地址栏会变     302

### 4. HttpServletRequest

- HttpServletRequest代表客户端的请求,用户通过Http协议访问服务器,Http请求中的所有信息会装到HttpServletRequest,通过这个HttpServletRequest的方法,获得客户端的所有信息.

##### 1. 获取前端传递的参数

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //设置编码
    resp.setCharacterEncoding("utf-8");
    req.setCharacterEncoding("utf-8");

    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobbies = req.getParameterValues("hobbies");
    System.out.println("============================================");
    System.out.println(username);
    System.out.println(password);
    System.out.println(Arrays.toString(hobbies));
    System.out.println(req.getContextPath());
    System.out.println("============================================");

    //通过请求转发
    //这里的'/'就是当前web应用的目录与req.getContextPath()的值一样
    req.getRequestDispatcher("/success.jsp").forward(req, resp);
}
```

##### 2. 请求转发

### 5. Session、Cookie

##### 5.1 会话

- 会话:用户打开超链接,点击了很多超链接,访问多个web资源,关闭浏览器,这个过程称之为会话.
- 有状态会话:一个网站怎么证明你来过?
    - 客户端	服务端
        1. 服务端给客户端一个信件,客户端下次访问服务端带上信件就可以了.cookie
            - 服务端发送给客户端Cookie,客户端接下来请求带着Cookie
        2. 服务器登记你来过了,下次你来的时候我来匹配你.session
            - 客户端去服务端登记一个Session,客户端获得Session的唯一标识sessionid.

##### 5.2 保存会话的2种技术

###### **cookie**

- 客户端技术	(响应, 请求)

###### **session**

- 服务器技术,利用这个技术,可以保存用户的会话信息,我们可以把信息或数据存放在Session中

###### 常见应用

- 一般网站进过一次后登录后,就不用登录了. 

##### 5.3 Cookie

1. 从请求中获取cookie信息
2. 服务器响应给客户端cookie

```java
Cookie[] cookies = req.getCookies();//获取Cookie
cookie.getName();//获取cookie的key
cookie.getValue();//获取cookie的value
Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis() + "");//新建一个cookie
cookie.setMaxAge(24 * 60 * 60);//设置有效期(s)
```

**cookie:一般会保存在本地的用户目录下的 Appdata**

- 一个cookie只能保存一个信息
- 一个web可以给浏览器发送多个cookie,最多存放20个cookie
- cookie大小有限制为4KB
- 浏览器cookie上限300

编码解码:

```java
URLEncoder.encode();
URLDecoder.decode();
```

##### 5.4 Session(重点)

1. 什么是Session?

- 服务器会给每一个用户(浏览器)创建一个Seesion对象.
- 一个Session独占一个浏览器,只要浏览器没有关闭,这个Session就存在.
- 用户登录之后,整个网站它都可以访问.-->保存用户的信息、保存购物车的信息...

2. Session 和 Cookie

- Cookie是把用户的数据写给用户的浏览器,浏览器保存(可保存多个)
- Session把用户的数据写到用户独占Session中,服务器端保存(保存重要信息,减少服务器资源浪费)
- Session由服务创建.

3. 使用场景

- 保存一个登录用户的信息.
- 购物车信息.
- 在整个网站中经常会使用的数据,我们将它保存在Session中.

4. 使用Session

```java
public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到session
        HttpSession session = req.getSession();

        //给Session中存东西
        session.setAttribute("name", new Person("王林清", 20));

        //获取Session的id
        String id = session.getId();

        //判断session是不是新创建的
        PrintWriter writer = resp.getWriter();
        if (session.isNew()) {
            writer.write("session创建成功,ID:" + id);
        } else {
            writer.write("session已经在服务器中存在了,ID:" + id);
        }

        //session创建的时候做了什么事情.
//        Cookie cookie = new Cookie("JSESSIONID", id);
//        resp.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
public class SessionDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到session
        HttpSession session = req.getSession();

        Person name = (Person) session.getAttribute("name");
        System.out.println(name.toString());
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
public class SessionDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        HttpSession session = req.getSession();
        session.removeAttribute("name");
        session.invalidate();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
```

5.自动注销

```xml
<!--设置session默认的失效时间-->
    <session-config>
        <!--1分钟后session自动失效-->
        <session-timeout>1</session-timeout>
    </session-config>
```

### 6. JSP

##### 6.1 什么是JSP?

- Java Server Pages: java服务器端页面,和servlet一样用于动态web技术.
    - 特点:写JSP就像是在写HTML.
    - 区别:
        - HTML只给用户提供静态数据.
        - JSP页面可以嵌入Java代码,为用户提供动态数据.

##### 6.2 JSP原理

1. JSP是如何运行的

- 代码层面没有问题

- 服务器内部工作

    - tomcat中有一个work目录.
    - IDEA中使用tomcat中也会生成一个word目录.
    - [目录路径](C:\Users\王林清\AppData\Local\JetBrains\IntelliJIdea2021.1\tomcat)

- 浏览器向服务器发送请求,不管访问什么资源其实都是在访问Servlet.

- JSP最终会被转换成为一个java类.

- JSP本质上就是一个Servlet.

    ```java
    //初始化
    public void _jspInit()
    //销毁
    public void _jspDestroy()
    //服务
    public void _jspService(final javax.servlet.http.HttpServletRequest request, final javax.servlet.http.HttpServletResponse response)throws java.io.IOException, javax.servlet.ServletException
    ```

    1. 判断请求
    2. 内置一些对象

    ```java
    //页面上下文
    final javax.servlet.jsp.PageContext pageContext;
    //session
    javax.servlet.http.HttpSession session = null;
    //applicationContext
    final javax.servlet.ServletContext application;
    //config
    final javax.servlet.ServletConfig config;
    //out
    javax.servlet.jsp.JspWriter out = null;
    //page 当前
    final java.lang.Object page = this;
    //请求
    javax.servlet.jsp.JspWriter _jspx_out = null;
    //响应
    javax.servlet.jsp.PageContext _jspx_page_context = null;
    ```

    3. 输出页面前增加的代码

    ```java
    //设置响应到页面类型
    response.setContentType("text/html;charset=UTF-8");
    pageContext = _jspxFactory.getPageContext(this, request, response,
                                              null, true, 8192, true);
    _jspx_page_context = pageContext;
    application = pageContext.getServletContext();
    config = pageContext.getServletConfig();
    session = pageContext.getSession();
    out = pageContext.getOut();
    _jspx_out = out;
    ```

    4. 以上这些对象我们可以在JSP页面中直接使用
    5. 在JSP页面中只要是JAVA代码就会原封不动到输出,HTML代码就会被直接转换为:

    ```java
    out.write("<html>\r\n")
    ```

    输出到前端.

##### 6.3 JSP基础语法

任何语言都有自己的语法,java中有,JSP作为java技术中的一种应用,他拥有一些自己的扩充的语法(了解知道即可)jav所有语法都支持.

1. **JSP表达式**

    ```jsp
    <%--jsp表达式
        作用将程序的输出,输出到客户端
        <%= 变量或表达式%>
    --%>
    <%= new java.util.Date()%>
    ```

2. JSP脚本片段

    ```jsp
    <%--jsp脚本片段--%>
    <%
            int sum = 0;
            for (int i = 0; i < 100; i++) {
                sum += i;
            }
            out.pirntln("<h1>sum=" + sum + "</h1>");
    %>
    ```

3. jsp声明

    ```jsp
    <%!
            static {
                System.out.println("Loading servlet!");
            }
    
            private int globalVar = 0;
    
            public void wlq() {
                System.out.println("进入了方法wlq!");
            }
    %>
    ```

    jsp声明会被jsp生成到java类的类中,其他的会被生成到_jspService方法中!

    在jsp中嵌入java代码即可.

    ```jsp
    <%%>
    <%=%>
    <%!%>
    <%--JSP注释-->
    <!--HTML注释-->
    ```

    JSP注释不会在客户端显示,HTML的可以显示

##### 6.4 JSP指令

```jsp
<%@page args...%>
<%@include file=""%>
<%--include会将2个页面合二为一--%>
<%@ include file="common/header.jsp" %>
<h1>网页主体</h1>
<%@ include file="common/footer.jsp" %>
<%--jsp标签
    jsp:include: 拼接页面,本质还是三个--%>
<jsp:include page="common/footer.jsp"/>
<h1>网页主体</h1>
<jsp:include page="common/header.jsp"/>
```

##### 6.5 九大内置对象

- PageContext: 存东西
- Request: 存东西
    - 客户端向服务器发送请求,产生到数据,用户看完就没用了,比如:新闻,用户看完没用的!
- Response
- Session: 存东西
    - 客户端向服务器发送请求,产生到数据,用户用完一会还有用,比如:购物车
- Application (ServletContext): 存东西
    - 客户端向服务器发送请求,产生到数据,一个用户用完了,其他用户可能还要用,比如:聊天数据
- config (ServletConfig)
- out
- page (this): 不用了解
- exception

```jsp
<%
    //pageContext只在一个页面中有效
    pageContext.setAttribute("name1", "wlq1");
    //保存的数据只在一次请求中有效,请求转发会携带这个数据
    request.setAttribute("name2", "wlq2");
    //保存数据在一次会话中有效,从打开浏览器到关闭浏览器
    session.setAttribute("name3", "wlq3");
    //保存的数据在服务器中有效
    application.setAttribute("name4", "wlq4");
%>
<%--脚本片段中的代码会被原封不动到生成到.jsp.java文件中
要求:其中的代码必须保证Java语法到正确性--%>
<%
    //从PageContext中取出,通过寻找的方式来
    //从底层到高层(作用域): page-->request-->session-->application
    //JVM:双亲委派机制:
    String name1 = (String) pageContext.findAttribute("name1");
    String name2 = (String) pageContext.findAttribute("name2");
    String name3 = (String) pageContext.findAttribute("name3");
    String name4 = (String) pageContext.findAttribute("name4");
    String name5 = (String) pageContext.findAttribute("name5");
%>
<%--使用EL表达式输出 ${}--%>
<h1>${name1}</h1>
<h1>${name2}</h1>
<h1>${name3}</h1>
<h1>${name4}</h1>
<h1><%= name5 %>
```

##### 6.6 JSP标签、JSTL标签和EL表达式

- EL表达式(express language)

    - **获取数据**
    - **执行运算**
    - **获取web开发到常用应用**
    - **~~调用java方法~~**

- JSP标签

    ```jsp
    <jsp:include page="common/header.jsp"/>
    <jsp:forward page="jsptag2.jsp">
        <jsp:param name="name" value="wlq"/>
        <jsp:param name="age" value="20"/>
    </jsp:forward>
    <jsp:include page="common/footer.jsp"/>
    ```

- JSTL表达式

    - JSTL标签库的使用就是为了弥补HTML标签的不足;它自定义了许多标签,可以供我们使用,标签的功能和java代码一样.

    **核心标签**(掌握)

    ![cn](https://myimageshack.oss-cn-hangzhou.aliyuncs.com/img/bX6c7m2RAHwkiWS.jpg)

    **格式化标签**

    **SQL标签**

    **XML标签**

### 7. JavaBean

实体类

JavaBean有特定的写法:

- 必须有一个无参构造
- 属性必须私有化
- 必须有对应的getter/setter

一般用来和数据库字段做映射 ORM.

ORM:对象关系映射

- 表 --> 类
- 字段 --> 属性
- 行记录 --> 对象

| id   | name   | age  | address |
| ---- | ------ | ---- | ------- |
| 1    | 王林清 | 3    | 常州    |
| 2    | 五六千 | 15   | 常州    |
| 3    | 我去   | 100  | 常州    |

### 8. MVC三层架构

早些年用户直接访问控制层，控制层就可以直接操作数据库。

```java
servlet——CRUD——>数据库
程序十分臃肿，不利于维护

架构：
    程序员调用JDBC，JDBC操作数据库。
```

现在：

- Model 模型
    - 业务处理：业务逻辑（Service）
    - 数据持久层：CRUD（DAO）

> 控制业务操作，保存数据，修改数据，删除数据，查询数据。
>
> 1. service 业务层
> 2. dao 实体层
> 3. javabean

- View 视图 JSP

    1. 展示数据

    2. 提供链接发起Servlet请求（a ,form,img...)

- Controller 控制器
    1. 接受用户请求：（req：请求参数，Session信息...）
    2. 响应给客户端内容（交给业务层去做）
    3. 重定向或转发
    4. 视图跳转

> 注：Servlet和JSP都可以写java代码：为了易于维护和使用，Servlet专注于处理请求，以及控制视图跳转；JSP专注于显示数据。

### 9. Filter过滤器

- Filter：过滤器、用来实现过滤网站的数据：

    1. 处理中文乱码。

    2. 登录验证。

- Filter开发流程：

    1. 导包：

    ```xml
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId>
        <version>2.3.3</version>
    </dependency>
    <dependency>
        <groupId>javax.servlet.jsp.jstl</groupId>
        <artifactId>jstl-api</artifactId>
        <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>taglibs</groupId>
        <artifactId>standard</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.37</version>
    </dependency>
    ```

    2. 编写Filter：

    ```java
    package com.wlq.filter;
    
    import javax.servlet.*;
    import java.io.IOException;
    
    /**
     * program: javaweb-Filter
     * <br>description:
     *
     * @author by 王林清 on 2021/7/24
     * @version Java1.9 IntelliJ IDEA
     */
    public class CharacterEncodingFilter implements Filter {
        @Override
        //web服务启动时初始化随时等待过滤对象
        public void init(FilterConfig filterConfig) throws ServletException {
            System.out.println("CharacterEncodingFilter已启动...");
        }
    
        @Override
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
            /*
            * chain: 链
            * 1.过滤中的所有代码在过滤特定请求时都会执行
            * 2.必须要让过滤器继续执行 chain.doFilter(request, response)
            */
            request.setCharacterEncoding("utf-8");
            response.setCharacterEncoding("utf-8");
            response.setContentType("text/html;charset=UTF-8");
    
            System.out.println("CharacterEncodingFilter执行前...");
            //让我们的请求继续走，如果没有，程序到这里就会被拦截
            chain.doFilter(request, response);
            System.out.println("CharacterEncodingFilter执行后...");
        }
    
        @Override
        //web服务销毁时过滤器销毁
        public void destroy() {
            System.out.println("CharacterEncodingFilter已销毁...");
        }
    }
    ```

    3. 在web.xml中配置filter

    ```xml
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>com.wlq.filter.CharacterEncodingFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/show</url-pattern>
    </filter-mapping>
    ```

### 10. listener监听器

1. 实现监听器接口，重写方法

```java
package com.wlq.listener;

import javax.servlet.ServletContext;
import javax.servlet.http.HttpSessionEvent;
import javax.servlet.http.HttpSessionListener;

/**
 * program: javaweb-Filter
 * <br>description: 统计网站在线人数：统计session
 *
 * @author by 王林清 on 2021/7/24
 * @version Java1.9 IntelliJ IDEA
 */
public class OnlineCountListener implements HttpSessionListener {
    @Override
    //创建session监听：创建就会触发
    public void sessionCreated(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();
        System.out.print("新创建的sessionID：");
        System.out.println(se.getSession().getId());
        Object onlineCount = ctx.getAttribute("OnlineCount");
        if (onlineCount == null) {
            onlineCount = 1;
        } else {
            int count = (int) onlineCount;
            onlineCount = count + 1;
        }
        ctx.setAttribute("OnlineCount", onlineCount);
    }

    @Override
    //销毁session监听
    public void sessionDestroyed(HttpSessionEvent se) {
        ServletContext ctx = se.getSession().getServletContext();
        System.out.print("销毁的sessionID：");
        System.out.println(se.getSession().getId());
        Object onlineCount = ctx.getAttribute("OnlineCount");
        if (onlineCount == null) {
            onlineCount = 0;
        } else {
            int count = (int) onlineCount;
            onlineCount = count - 1;
        }
        ctx.setAttribute("OnlineCount", onlineCount);
    }
}

```

2. web.xml配置监听器

```xml
<!--注册监听器-->
<listener>
    <listener-class>com.wlq.listener.OnlineCountListener</listener-class>
</listener>
```

### 11. 过滤器、监听器常见应用

- 监听器：GUI编程中常用

    ```java
    package com.wlq.listener;
    
    import java.awt.*;
    import java.awt.event.WindowAdapter;
    import java.awt.event.WindowEvent;
    
    /**
     * program: javaweb-Filter
     * <br>description:
     *
     * @author by 王林清 on 2021/7/24
     * @version Java1.9 IntelliJ IDEA
     */
    public class TestPanel {
        public static void main(String[] args) {
            Frame f = new Frame("hhby");
            Panel panel = new Panel(null);
            f.setLayout(null);
    
            f.setBounds(300, 300, 500, 500);
            f.setBackground(new Color(0, 0, 255));
    
            panel.setBounds(100, 100, 200, 200);
            panel.setBackground(new Color(5, 25, 125));
    
            f.add(panel);
            f.setVisible(true);
            f.addWindowListener(new WindowAdapter() {
                @Override
                public void windowClosing(WindowEvent e) {
                    System.out.println("close");
                    System.exit(0);
                }
            });
        }
    }
    ```

- 过滤器：用户登录后才能进入主页！用户注销后就不能进入主页

    1. 用户登录后向Session中放入用户数据

    2. 进入主页时判断用户是否已登录，在过滤器中实现！

        ```java
        @Override
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
            // ServletRequest --> HttpServletRequest
            HttpServletRequest req = (HttpServletRequest) request;
            HttpServletResponse resp = (HttpServletResponse) response;
        
            Object userSession = req.getSession().getAttribute(Constant.USER_SESSION);
            if (userSession == null) {
                resp.sendRedirect("/error.jsp");
            }
            chain.doFilter(request, response);
        }
        ```

### 12. JDBC复习

>   见：[MySQL学习](./../基本知识/MySQL.md)

Junit单元测试

-   依赖：

    ```xml
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <!--scope:作用域，默认compile-->
        <scope>compile</scope>
    </dependency>
    ```

-   使用@Test注解可以使方法直接运行