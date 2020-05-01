---
title: Java Notes
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/Commom/xiangxiang.jpg
date: 2018-3-25
---
# JavaEE

## Tomcat

### tomcat启动问题

#### 1.一闪而过

> 未找到jdk%JAVA_HOME%
>

#### 2.报错-端口占用

    cmd netstat -ano  找到8080进程pid 在任务管理器中关掉
    修改配置

### 部署方式

**wabapps目录下 __/项目文件**

1.简化部署-项目打包成war包复制到目录下,会自动解压缩

2.配置server.xml

```
<Context docbase="原项目路径" path="虚拟路径(随便写)"/>
```

缺点:多个项目,配置不安全

3.在F:\Develop_Apache\apache-tomcat-8.5.45-windows-x64\apache-tomcat-8.5.45\conf\Catalina\localhost目录下创建任意名的xml文件

键入

```
<Context docbase="原项目路径"/>
```

则项目的虚拟路径为/xml的文件名

### 静态项目和动态项目的目录结构

### IDEA配置Tomcat

run-> edit configurations->tomcatserver

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Images20191031210806.png)


## Servlet和Http请求协议

### Servlet简介-server applet

![](https://raw.githubusercontent.com/FenQingyang/Ey_PicBed/master/Imagesservlet%E6%9E%B6%E6%9E%84.png)

**1）作用：**
规范了浏览器与服务器(代码编写的一个可以根据用户请求实时的调用执行对应的逻辑代码的一个容器)的数据交互；
格式：key:value;
**2）特点：**
简单快速；
灵活：允许传输任何数据对象，有Content-Type加以标记。
无连接：HTTP1.1后支持可持续连接
无状态：对于事物处理没有记忆能力
**3）HTTP交互流程：**
建立连接
发送数据
响应客户端
**4）请求格式：**
请求头：
请求行：
空行：
请求数据
**5）get与post的区别**
**6）响应格式及状态码**（三个十进制数字组成，第一个定义了状态码的类型，后两个数组没有分类的作用）
HTTP状态码分类：

### demo1

```java
package com.web.servlet;

import javax.servlet.*;
import java.io.IOException;

public class servlet implements Servlet {
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello servlet");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

**web.xml**

```xml
 <servlet>
        <servlet-name>demo01</servlet-name>
        <servlet-class>com.web.servlet.servlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>demo01</servlet-name>
        <url-pattern>/demo01</url-pattern>
    </servlet-mapping>
```

### Servlet技术

**Servlet 是什么？**

> Java Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。
>
> 使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页。
>

Java Servlet 通常情况下与使用 CGI（`Common Gateway Interface`，公共网关接口）实现的程序可以达到异曲同工的效果。但是相比于 CGI，Servlet 有以下几点优势：

> 性能明显更好。
> Servlet 在 Web 服务器的地址空间内执行。这样它就没有必要再创建一个单独的进程来处理每个客户端请求。
> Servlet 是独立于平台的，因为它们是用 Java 编写的。
> 服务器上的 Java 安全管理器执行了一系列限制，以保护服务器计算机上的资源。因此，Servlet 是可信的。
> Java 类库的全部功能对 Servlet 来说都是可用的。它可以通过 sockets 和 RMI 机制与 applets、数据库或其他软件进行交互。

**Servlet 任务**

Servlet 执行以下主要任务：

> 读取客户端（浏览器）发送的显式的数据。这包括网页上的 HTML 表单，或者也可以是来自 applet 或自定义的 HTTP 客户端程序的表单。
> 读取客户端（浏览器）发送的隐式的 HTTP 请求数据。这包括 cookies、媒体类型和浏览器能理解的压缩格式等等。
> 处理数据并生成结果。这个过程可能需要访问数据库，执行 RMI 或 CORBA 调用，调用 Web 服务，或者直接计算得出对应的响应。
> 发送显式的数据（即文档）到客户端（浏览器）。该文档的格式可以是多种多样的，包括文本文件（HTML 或 XML）、二进制文件（GIF 图像）、Excel 等。
> 发送隐式的 HTTP 响应到客户端（浏览器）。这包括告诉浏览器或其他客户端被返回的文档类型（例如 HTML），设置 cookies 和缓存参数，以及其他类似的任务。

**Servlet使用流程：**

1、创建普通Java类，并继承HttpServlet
2、覆写service方法
3、在service方法中书写逻辑代码
4、在webroot下的web-inf文件夹下的web.xml文件中配置servlet(demo1)

> ​	servlet3.0注解配置
>
> 在类上使用`@webservlet("资源路径")`不需要web.xml配置

**Servlet访问流程**

输入URL

```
服务器地址：端口号/project/要执行的servlet的ul-pattern->classname->methodname
```

> Tomcat将全类名对应的字节码文件加载进内存Class.forname()
>
> 创建class对象.newInstance()
>
> 调用service方法

**servlet接口的实现**

1、实现 Servlet 接口

因为是实现 Servlet 接口，所以我们需要实现接口里的方法。



**Servlet生命周期**

Servlet的生命周期:从Servlet被创建到Servlet被销毁的过程

特点:

> 一次创建，到处服务
> 一个Servlet只会有一个对象，服务所有的请求

 * 1.实例化（使用构造方法创建对象）

    * 指定servlet的创建时机

       * 在servlet标签下配置load-on-startup

          * ```
            <load-on-startup>负整数</load-on-startup>//第一次访问时
            ```

            

          * ```
            <load-on-startup>正整数</load-on-startup>//服务器启动时
            ```

            

 * 2.初始化  执行init方法

 * 3.服务     执行service方法

 * 4.销毁    执行destroy方法

```
public class ServletDemo1 implements Servlet {
    
//public ServletDemo1(){}
    
     //生命周期方法:当Servlet第一次被创建对象时执行该方法,该方法在整个生命周期中只执行一次,Servlet在内存中只存在一个对象,多个用户访问时存在线程安全问题,so,尽量不要在Servlet中定义变量,即使定义了不要修改.
    public void init(ServletConfig arg0) throws ServletException {
                System.out.println("=======init=========");
    }
    
    //生命周期方法:对客户端响应的方法,该方法会被执行多次，每次请求该servlet都会执行该方法
    public void service(ServletRequest arg0, ServletResponse arg1)
            throws ServletException, IOException {
    System.out.println("hehe");
    
}
    
    //生命周期方法:当Servlet被销毁时执行该方法
    public void destroy() {
        System.out.println("******destroy**********");
}
    //当停止tomcat时也就销毁的servlet。
public ServletConfig getServletConfig() {
    
        return null;

    }
//获取Servlet信息
    public String getServletInfo() {
    
    return null;
 
	 }
 }
```

 

2、继承 GenericServlet 类

它实现了 Servlet 接口除了 service 的方法，不过这种方法我们极少用。

public class ServletDemo2 extends GenericServlet {

    @Override
    public void service(ServletRequest arg0, ServletResponse arg1)
            throws ServletException, IOException {
        System.out.println("heihei");
    
    }
}

3、继承 HttpServlet 方法

public class ServletDemo3 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        System.out.println("haha");
    }
    
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        System.out.println("ee");
        doGet(req,resp);
    }

}
**关于 HttpServlet、GenericServlet 和 Servlet 的关系**

>
> 对于一个 Servlet 类，我们日常最常用的方法是继承自 HttpServlet 类，提供了 Http 相关的方 HttpServlet 扩展了 GenericServlet 类，而 GenericServlet 类又实现了 Servlet 类和 ServletConfig 类。
>

**Servlet方法**

> Servlet类提供了五个方法，其中三个生命周期方法和两个普通方法，关于 Servlet类的方法，不再赘述，我主要补充一下另外两个类的实现思路。
>

**GenericServlet**

GenericServlet 是一个抽象类，实现了 Servlet 接口，并且对其中的 init() 和 destroy() 和 service() 提供了默认实现。在 GenericServlet 中，主要完成了以下任务：

> 将 init() 中的 ServletConfig 赋给一个类级变量，可以由 getServletConfig 获得；
> 为 Servlet 所有方法提供默认实现；
> 可以直接调用 ServletConfig 中的方法；

基本的结构如下：

```
abstract class GenericServlet implements Servlet,ServletConfig{

   //GenericServlet通过将ServletConfig赋给类级变量
   private trServletConfig servletConfig;

   public void init(ServletConfig servletConfig) throws ServletException {

  this.servletConfig=servletConfig;

  /*自定义init()的原因是：如果子类要初始化必须覆盖父类的init() 而使它无效 这样
   this.servletConfig=servletConfig不起作用 这样就会导致空指针异常 这样如果子类要初始化，
   可以直接覆盖不带参数的init()方法 */
  this.init();

   }

   //自定义的init()方法，可以由子类覆盖  
   //init()不是生命周期方法
   public void init(){

   }

   //实现service()空方法，并且声明为抽象方法，强制子类必须实现service()方法 
   public abstract void service(ServletRequest request,ServletResponse response) 
     throws ServletException,java.io.IOException{
   }

   //实现空的destroy方法
   public void destroy(){ }
}
```

以上就是 GenericServlet 的大致实现思想，可以看到如果继承这个类的话，我们必须重写 service() 方法来对处理请求。

**HttpServlet**

HttpServlet 也是一个抽象类，它进一步继承并封装了 GenericServlet，使得使用更加简单方便，由于是扩展了 Http 的内容，所以还需要使用 HttpServletRequest 和 HttpServletResponse，这两个类分别是 ServletRequest 和 ServletResponse 的子类。代码如下：

```
abstract class HttpServlet extends GenericServlet{

   //HttpServlet中的service()
   protected void service(HttpServletRequest httpServletRequest,
                       HttpServletResponse httpServletResponse){
        //该方法通过httpServletRequest.getMethod()判断请求类型调用doGet() doPost()
   }

   //必须实现父类的service()方法
   public void service(ServletRequest servletRequest,ServletResponse servletResponse){
      HttpServletRequest request;
      HttpServletResponse response;
      try{
         request=(HttpServletRequest)servletRequest;
         response=(HttpServletResponse)servletResponse;
      }catch(ClassCastException){
         throw new ServletException("non-http request or response");
      }
      //调用service()方法
      this.service(request,response);
   }
}
```

我们可以看到，HttpServlet 中对原始的 Servlet 中的方法都进行了默认的操作，不需要显式的销毁初始化以及 service()，在 HttpServlet 中，自定义了一个新的 service() 方法，其中通过 getMethod() 方法判断请求的类型，从而调用 doGet() 或者 doPost() 处理 get,post 请求，使用者只需要继承 HttpServlet，然后重写 doPost() 或者 doGet() 方法处理请求即可。

PS:IDEA与Tomcat配置

`IDEA会为每一个tomcat部署的项目单独创建一份配置文件`

控制台log:using CATALINA_BASE:

`工作空间项目和tomcat部署的web项目`

- tomcat真正访问的是"tomcat部署的web项目","tomcat部署的web项目"对应者工作空间项目下的所有资源.

- WEB-INF目录下的资源不能被浏览器直接访问.

  ------

  

### Http协议

* 概念：Hyper Text Transfer Protocol 超文本传输协议
	* 传输协议：定义了，客户端和服务器端通信时，发送数据的格式
	* 特点：
		1. 基于TCP/IP的高级协议
		2. 默认端口号:80
		3. 基于请求/响应模型的:一次请求对应一次响应
		4. 无状态的：每次请求之间相互独立，不能交互数据

	* 历史版本：
		* 1.0：每一次请求响应都会建立新的连接
		* 1.1：复用连接

* 请求消息数据格式
	1. 请求行
		请求方式 请求url 请求协议/版本
		GET /login.html	HTTP/1.1

		* 请求方式：
			* HTTP协议有7中请求方式，常用的有2种
				* GET：
					1. 请求参数在请求行中，在url后。
					2. 请求的url长度有限制的
					3. 不太安全
				* POST：
					1. 请求参数在请求体中
					2. 请求的url长度没有限制的
					3. 相对安全
	2. 请求头：客户端浏览器告诉服务器一些信息
		请求头名称: 请求头值
		* 常见的请求头：
			1. User-Agent：浏览器告诉服务器，我访问你使用的浏览器版本信息
				* 可以在服务器端获取该头的信息，解决浏览器的兼容性问题

			2. Referer：http://localhost/login.html
				* 告诉服务器，我(当前请求)从哪里来？
					* 作用：
						1. 防盗链：
						2. 统计工作：
	3. 请求空行
		空行，就是用于分割POST请求的请求头，和请求体的。
	4. 请求体(正文)：
		* 封装POST请求消息的请求参数的

	* 字符串格式：
		
		```
		POST /login.html	HTTP/1.1
		Host: localhost
		User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:60.0) Gecko/20100101 Firefox/60.0
		Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
		Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
		Accept-Encoding: gzip, deflate
		Referer: http://localhost/login.html
		Connection: keep-alive
		Upgrade-Insecure-Requests: 1
		
		username=zhangsan	
		```
		
		------
		
		### Request

## JSTL

Java Server Pages Tag Library----JSP标准标签库
是由Apache免费提供的用于简化和替换jsp页面上的java代码
使用步骤:
1.导包
2.引入标签库taglib指令<%@ taglib %>
3.使用

常用标签:
if 
```jsp
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%--c:if--%>
<%--test 必须属性,接收boolean表达式,如果为真显示标签的内容,false不显示
一般这个属性值结合EL表达式使用
--%>
```

choose
```

<%--c:choose
switch
    when __case
    otherwis default
--%>
```

foreach


```

<%--c:foreach
--%>
<c:forEach begin="0" end="10"  step="1" var="i" >
${i}
</c:forEach>
<%
    List list=new ArrayList();
    list.add("aaa");
    list.add("bbb");
    list.add("ccc");
    request.setAttribute("list", list);
%>
<c:forEach items="${list}" varStatus="s" var="str">
${s.count}
${s.index}
</c:forEach>
```
