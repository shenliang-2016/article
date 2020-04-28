# Java Web 开发发展简介

https://www.jianshu.com/p/bec6736dcc3d



## 远古期 - 静态页面时代

讲Java Web开发的历史进程，不得不提Web开发的历史进程。
在互联网刚发展的时候，那时候的网站功能是很简单的。那时候的网站还都是**静态**的。这里所说的**静态**是指，请求访问的网页都是事先编辑好的，不能改变的。

这里先讲下当时一个请求是如何返回结果的。

比如，你想访问新浪上的一张图片，会在浏览器键入这个图片的地址：



![img](https://upload-images.jianshu.io/upload_images/1996876-5c1251aeeecde06e.png)



浏览器会根据地址像新浪服务器发送HTTP请求。新浪服务器上的HTTP Server接收到请求后，会根据路径地址`/img/12345.jpg`查找的这个文件，然后read文件，再把图片数据发送给客户端，客户端的浏览器就能正确展示图片了。



![img](https://upload-images.jianshu.io/upload_images/1996876-4390fbfa8a99aecf.png)



也就是说，这里的URL对服务器来说就是查找文件的地址，而文件必须实实在在存在于服务器中的特定目录下的。

**缺点**
很明显，访问的资源必须事先已经存在，否则访问不到。而动态展示也是没法实现的。比如：某人刚发布了一篇文章，想在首页立即看到是不可能的。只能重新手动编辑首页，把文章链接加进去

## 混沌期 - CGI时代

然而，如果页面一直是静态的额，也就不会有现在纷繁复杂的网站了。那么动态展示页面的解决方案是什么呢？**是CGI**！
CGI全称是通用网关接口(Common Gateway Interface)。那么它的作用是啥呢？

### CGI是啥

首先，要清楚CGI是啥？
CGI是一个可执行的程序或者可运行的脚本。几乎所有语言都能写CGI，像python，C，甚至shell。

举个例子。下面一段C代码，经过编译成可执行程序后，就是一个CGI。

```cpp
int _tmain(int argc, _TCHAR* argv[])
{
    printf("Content-type:text/html\n\n");
    printf("%s",getenv("QUERY_STRING")); //打印get获取的信息
    return 0;
}
```

再或者，下面一个python脚本，也是一个CGI

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

print "Content-type:text/html"
print                               # 空行，告诉服务器结束头部
print '<html>'
print '<head>'
print '<meta charset="utf-8">'
print '<title>Hello Word - 我的第一个 CGI 程序！</title>'
print '</head>'
print '<body>'
print '<h2>Hello Word! 我是来自菜鸟教程的第一CGI程序</h2>'
print '</body>'
print '</html>'
```

OK，知道了CGI是可执行的程序或脚本，但是怎么工作的呢？

### CGI怎么用



![img](https://upload-images.jianshu.io/upload_images/1996876-c3946bacbaaa8636.png)



如上图，当浏览器发送一个CGI请求后，服务器会启动一个进程运行CGI程序或脚本，由CGI来处理数据，并将结果返回给服务器，服务器再将结果返回给浏览器。

举个表单提交的例子：

```vbscript-html
<form id="form" name="form" method="post" action="http://localhost/cgi-bin/test/cgi_test.cgi">
  <p>输入内容：
    <input type="text" name="user" id="user" />
  </p>
  <p>
    <input type="submit" name="submit" id="submit" value="提交" />
  </p>
</form>
```

上面是一个表单提交的html代码，展示的效果是下面这个样子：



![img](https://upload-images.jianshu.io/upload_images/1996876-a6b1731897142e03.png)



细心的你会发现，`action`的值是`http://localhost/cgi-bin/test/cgi_test.cgi`。这里，`cgi_test.cgi`就是一个cgi程序。
还记得上面那段C++代码吗？

```cpp
int _tmain(int argc, _TCHAR* argv[])
{
    printf("Content-type:text/html\n\n");
    printf("%s",getenv("QUERY_STRING")); //打印get获取的信息
    return 0;
}
```

cgi_test.cgi就是这段代码编译出来的可执行程序。
**这段代码的作用是什么呢？**
作用是将表单提交的信息直接打印出来。
**如何做到的？**
只有两行代码，第二行代码是关键。`getenv()是C函数库中的函数`，`getenv("QUERY_STRING")`的意思是读取环境变量`QUERY_STRING`的值。而`QUERY_STRING`的值就是表单提交的信息。
OK，这个CGI的功能就清晰了。表单提交后展示下面的结果也就不奇怪了：



![img](https://upload-images.jianshu.io/upload_images/1996876-0536fa48c7edf3e9.png)



我们再通过一个图梳理下上述流程：



![img](https://upload-images.jianshu.io/upload_images/1996876-53a368da34eed68d.png)



综上，CGI工作模式示意图如下：



![img](https://upload-images.jianshu.io/upload_images/1996876-103824db9ee9408b.png)



### CGI的特点

- 由Http Server唤起。常见的Http Server如Apache，Lighttpd，nginx都支持CGI
- CGI单独启动进程，并且每次调用都会重新启动进程
- 可以用任何语言编写，只要该语言支持标准输入、输出和环境变量

### CGI的缺点

- **消耗资源多**：每个请求都会启动一个CGI进行，进程消耗资源15M内存的话，同时到达100个请求的话，就会占用1.5G内存。如果请求更多，资源消耗是不可想象的。
- **慢**：启动进程本身就慢。每次启动进程都需要重新初始化数据结构等，会变得更慢。

**引申**

> 为了解决CGI重复启动进程和初始化的问题，后来出现了**FastCGI**

## 开荒期 - Servlet时代

在CGI繁荣发展的时代，Java还没有发展起来。当Java开始参与历史，引领潮流的时候，也必然会借鉴和改进之前的技术和思想。

鉴于CGI的一些缺点，Java Web在开始设计的时候就想出了一种解决方案 -- Servlet
同样，第一个问题，Servlet是啥？

### Servlet是啥？

举个例子，网站一般都有注册功能。当用户填写好注册信息，点击“注册”按钮时，谁来处理这个请求？用户名是否重复谁来校验？用户名和密码需要写入数据库，谁来写入？是Servlet！

Servlet是实现`javax.servlet.Servlet`接口的类。一般处理Web请求的Servlet还需要继承`javax.servlet.http.HttpServlet`

```java
abstract class HttpServlet implements Servlet{
    void doGet();
    void doPost();
}
```

`doGet()`方法处理GET请求
`doPost()`方法处理POST请求

浏览器发来的请求是怎么被Servlet处理的呢？还是举表单提交的例子。
我们假设表单样式如下，只是简单提交两个数据：网址名和网址。并假设处理URL为`http://localhost:8080/TomcatTest/HelloForm`



![img](https://upload-images.jianshu.io/upload_images/1996876-27bcc8bc57381ce0.png)



**浏览器工作**
当表单使用GET方式提交时，浏览器会把表单数据组装成这样的URL：`http://localhost:8080/TomcatTest/HelloForm?name=菜鸟教程&url=www.runoob.com`

好，现在浏览器的任务暂时告一段落，开始Java Web服务工作了。

**Java Web服务**
首先，我们得指定`http://localhost:8080/TomcatTest/HelloForm`这个URL由谁来处理。这个映射关系需要在web.xml中配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app>
  <servlet>
    <servlet-name>HelloForm</servlet-name>
    <servlet-class>com.runoob.test.HelloForm</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>HelloForm</servlet-name>
    <url-pattern>/TomcatTest/HelloForm</url-pattern>
  </servlet-mapping>
</web-app>
```

web.xml中配置的意思是：当URI为`/TomcatTest/HelloForm`时，交给`com.runoob.test.HelloForm`处理。而`HelloForm`正是个Servlet。

因此，我们需要编写`HelloForm`这样一个Servlet：

```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class HelloForm
 */
@WebServlet("/HelloForm")
public class HelloForm extends HttpServlet {
    private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public HelloForm() {
        super();
        // TODO Auto-generated constructor stub
    }

    /**
     * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
     */
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置响应内容类型
        response.setContentType("text/html;charset=UTF-8");

        PrintWriter out = response.getWriter();
        String title = "使用 GET 方法读取表单数据";
        // 处理中文
        String name =new String(request.getParameter("name").getBytes("ISO8859-1"),"UTF-8");
        String docType = "<!DOCTYPE html> \n";
        out.println(docType +
            "<html>\n" +
            "<head><title>" + title + "</title></head>\n" +
            "<body bgcolor=\"#f0f0f0\">\n" +
            "<h1 align=\"center\">" + title + "</h1>\n" +
            "<ul>\n" +
            "  <li><b>站点名</b>："
            + name + "\n" +
            "  <li><b>网址</b>："
            + request.getParameter("url") + "\n" +
            "</ul>\n" +
            "</body></html>");
    }
    
    // 处理 POST 方法请求的方法
    public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}
```

由于请求方式是GET，因此需要`doGet()`方法来处理。仔细阅读`doGet()`方法的代码，发现处理逻辑只是把表单数据放入到了一段html代码中。这段html代码会被传输给浏览器，然后浏览器渲染出结果，如下图所示：



![img](https://upload-images.jianshu.io/upload_images/1996876-46291ae941a20227.png)



### Servlet的特点

Servlet相对于CGI有了很大的改进，效率更高，功能更强大，更容易移植。主要表现在一下几个方面：

- CGI每个请求启动一个进程，而Servlet是更轻量的线程。线程和进程的对比和优劣请自行Google。
- CGI每个进程都需要初始化，Servlet只初始化一次实例就行
- Servlet依托于Java语言，具有很好的跨平台型。CGI根据语言的不同，跨平台型不同
- CGI与数据库连接需要重连，Servlet可以使用数据库连接池。
- Java有丰富的、各种各样的库函数

### Servlet的缺点

看上面的代码，会发现，html代码是写在Java代码中的。对于前端人员来说，这种形式非常非常难以开发和修改。

### Servlet的升级 -- JSP

Servlet是在**Java代码中写HTML代码**。与之对应的就是在**HTML代码中写Java代码**，这就是JSP。

#### JSP是啥？

JSP：JavaServer Pages
简单点说，就是可以在html中写Java代码。

还是先从例子中大概了解下JSP：

还是上面表单处理的例子。表单的html代码就不展示了，我们直接模拟GET请求，即在浏览器中输入地址：`http://localhost:8080/testjsp/main.jsp?name=菜鸟教程&url=http://www.runoob.com`

很明显，这个URL的关键是`main.jsp`。这个文件的内容是啥呢？
**main.jsp**

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import="java.io.*,java.util.*" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<h1>使用 GET 方法读取数据</h1>
<ul>
<li><p><b>站点名:</b>
   <%= request.getParameter("name")%>
</p></li>
<li><p><b>网址:</b>
   <%= request.getParameter("url")%>
</p></li>
</ul>
</body>
</html>
```

这就是JSP，在html代码中插入Java代码。java代码被`<% %>`所包围。
`<%= request.getParameter("name")%>`表示获取请求参数name的值，`<%= request.getParameter("url")%>`表示获取请求参数url的值。最终展示结果是怎样的呢？看下图：



![img](https://upload-images.jianshu.io/upload_images/1996876-b07d5d84210916bc.png)



#### JSP是如何工作的？

为啥html代码中可以写Java代码呢？看下图：



![img](https://upload-images.jianshu.io/upload_images/1996876-b219f3d0b0d94510.png)



其实原理是这样的：

> 就像其他普通的网页一样，您的浏览器发送一个HTTP请求给服务器。
>
> Web服务器识别出这是一个对JSP网页的请求，并且将该请求传递给JSP引擎。通过使用URL或者.jsp文件来完成。
>
> JSP引擎从磁盘中载入JSP文件，然后将它们转化为servlet。这种转化只是简单地将所有模板文本改用println()语句，并且将所有的JSP元素转化成Java代码。
>
> JSP引擎将servlet编译成可执行类，并且将原始请求传递给servlet引擎。
>
> Web服务器的某组件将会调用servlet引擎，然后载入并执行servlet类。在执行过程中，servlet产生HTML格式的输出并将其内嵌于HTTP response中上交给Web服务器。
>
> Web服务器以静态HTML网页的形式将HTTP response返回到您的浏览器中。
>
> 最终，Web浏览器处理HTTP response中动态产生的HTML网页，就好像在处理静态网页一样。

用一句话来讲：**每个JSP都最终会变成对应的Servlet执行**

#### JSP的缺点

在HTML代码中写Java代码，方便了前端人员，但是苦了后端人员。因此，单纯使用JSP，开发效率依旧不高。

后来，有牛人发现，Servlet天生非常适合逻辑处理(因为主要是Java代码)，而JSP非常适合页面展示(因为主要是html代码)，那么在结合Servlet和JSP各自的优缺点后，诞生了Web开发中最常用和最重要的架构设计模式：**MVC**

## 发展期 - MVC时代

> MVC模式（Model-View-Controller）是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）：
>
> - Controller——负责转发请求，对请求进行处理
> - View——负责界面显示
> - Model——业务功能编写（例如算法实现）、数据库设计以及数据存取操作实现



![img](https://upload-images.jianshu.io/upload_images/1996876-9f3ef5f055f5e520.png)



简而言之，请求发来后，会首先经过Controller层处理，需要返回的结果封装成对象传递给JSP，然后JSP负责取出数据展示就够了。这样，后端开发人员只负责编写Servlet，前端人员负责JSP，极大提升了开发效率。

```java
@WebServlet("/userPosts")
public class UserPostController extends HttpServlet {

    private static final long serialVersionUID = -4208401453412759851L;

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        User user = Data.getByUsername(username);
        List<Post> posts = Data.getPostByUser(user);

        req.setAttribute("posts", posts);
        req.setAttribute("user", user);
        RequestDispatcher dispatcher = req.getRequestDispatcher("/templates/userPost.jsp");
        dispatcher.forward(req, resp);
    }
}
```

像上面这段代码，`UserPostController`就是一个Servlet，负责逻辑处理。需要返回的数据封装到`HttpServletRequest`对象中，传递给jsp页面。而负责展示的就是`/templates/userPost.jsp`这个jsp文件。

## 繁盛期 - 框架时代

有了Servlet和JSP，相当于有了武器。有了MVC，相当于有了战术。但是武器和战术之间还缺少一层，就是具体实施者。

实践证明，单纯使用Servlet、JSP和MVC开发，依然会面临诸多的问题。而程序员普遍存在一种特质，就是懒。因为懒，所以才想着能有更简单的解决办法。因为懒，针对一些通用问题，才会想出通用解决方法。可以说，因为懒，科技才有了进步。。。这时候，为了解放劳动力，一些开源框架营运而出。这些框架的目的只有一个：**让开发简单，简单，更简单**

提到Java Web框架，就不得不提几乎所有开发者都知道的三大框架：**SSH**

### SSH

关于三大框架，这里不做介绍了，网上的文章铺天盖地。想要说的是：无论什么框架，都是对常见问题的抽象和封装，再出什么新的框架，也万变不离其宗，脱离不了Servlet这个根基。学习的时候千万不能跟着框架走，框架让做什么就做什么，而是要想为什么这样做。否则，今天学会了一个框架，明天又出了新的框架，又会抓瞎了。

## 参考

- [Servlet3.0学习总结(一)——使用注解标注Servlet](https://link.jianshu.com/?t=http://www.cnblogs.com/xdp-gacl/p/4222902.html)
- [jsp container vs servlet container](https://link.jianshu.com/?t=https://stackoverflow.com/questions/10680332/jsp-container-vs-servlet-container)
- [Servlet 工作原理解析](https://link.jianshu.com/?t=https://www.ibm.com/developerworks/cn/java/j-lo-servlet/)
- [JSP/Servlet——MVC设计模式](https://link.jianshu.com/?t=https://www.tianmaying.com/tutorial/jsp-servlet-mvc-architecture)
- [J2EE开发框架发展简史 开源框架的出现](https://link.jianshu.com/?t=http://developer.51cto.com/art/200906/130235.htm)
- [Java新手如何学习Spring、Struts、Hibernate三大框架？](https://link.jianshu.com/?t=https://www.zhihu.com/question/21142149)