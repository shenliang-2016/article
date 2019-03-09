# 目录

----

- 1  概述
  - 1.1  Servlet 是什么？

    - 1.2  Servlet 容器是什么？
    - 1.3  一个例子
    - 1.4  与其他技术的比较
    - 1.5  与 JavaEE 的关系
    - 1.6  与Java Servlet Spec V2.5 的比较
      - 1.6.1  处理注解
- 2  Servlet 接口
  - 2.1  请求 Request 处理方法
    - 2.1.1  HTTP Request 专门的处理方法
    - 2.1.2  附加方法
    - 2.1.3  条件 GET 支持
  - 2.2  实例个数
    - 2.2.1  关于单线程模型的说明
  - 2.3  Servlet 生命周期
    - 2.3.1  加载和实例化
    - 2.3.2  初始化
      - 2.3.2.1  初始化中发生错误的情况
      - 2.3.2.2  工具层面的考虑
    - 2.3.3  请求 Request 处理
      - 2.3.3.1  多线程问题
      - 2.3.3.2  请求 Request 处理过程中的异常
      - 2.3.3.3  异步处理
      - 2.3.3.4  线程安全
      - 2.3.3.5  （协议）升级处理
    - 2.3.4  服务结束
- 3  请求 Request 

  - 3.1  HTTP 协议参数
    - 3.1.1  参数生效的时机
  - 3.2  文件上传
  - 3.3  协议属性
  - 3.4  协议头部
  - 3.5  请求路径元素
  - 3.6  路径转化方法
  - 3.7  非阻塞 IO
  - 3.8  HTTP/2 服务端推送
  - 3.9  Cookies
  - 3.10  SSL 属性
  - 3.11  国际化
  - 3.12  请求数据编码
  - 3.13  请求对象的存活时间
- 4  Servlet 上下文

  - 4.1  ServletContext 接口介绍
  - 4.2  ServletContext 接口的作用域
  - 4.3  初始化参数
  - 4.4  配置方法
    - 4.4.1  通过编程方式添加和配置 Servlets
      - 4.4.1.1  addServlet(String servletName, String className) 
      - 4.4.1.2  addServlet(String servletName, Servlet servlet) 
      - 4.4.1.3  addServlet(String servletName, Class <? extends Servlet>
        servletClass) 
      - 4.4.1.4  addJspFile(String servletName, String jspfile) 
      - 4.4.1.5  &lt;T extends Servlet> T createServlet(Class&lt;T> clazz) 
      - 4.4.1.6  ServletRegistration getServletRegistration(String
        servletName) 
      - 4.4.1.7  Map&lt;String, ? extends ServletRegistration>
        getServletRegistrations() 
    - 4.4.2  通过编程方式添加和配置 Filters
      - 4.4.2.1  addFilter(String filterName, String className) 
      - 4.4.2.2  addFilter(String filterName, Filter filter) 
      - 4.4.2.3  addFilter(String filterName, Class <? extends Filter>
        filterClass) 
      - 4.4.2.4  &lt;T extends Filter> T createFilter(Class&lt;T> clazz) 
      - 4.4.2.5  FilterRegistration getFilterRegistration(String filterName) 
      - 4.4.2.6  Map&lt;String, ? extends FilterRegistration>
        getFilterRegistrations() 
    - 4.4.3  通过编程方式添加和配置 Listeners
      - 4.4.3.1  void addListener(String className) 
      - 4.4.3.2  &lt;T extends EventListener> void addListener(T t) 
      - 4.4.3.3  void addListener(Class <? extends EventListener>
        listenerClass) 
      - 4.4.3.4  &lt;T extends EventListener> void createListener(Class<T>
        clazz) 
      - 4.4.3.5  编程方式添加 Servlets、Filters 以及 Listeners 需要的注解
    - 4.4.4  编程方式配置 session 超时
    - 4.4.5  编程方式配置字符集编码
  - 4.5  Context  属性
    - 4.5.1  分布式容器中的 Context 属性
  - 4.6  资源
  - 4.7  多主机环境下的 Servlet Contexts
  - 4.8  类动态重新加载分析
    - 4.8.1  临时工作目录
- 5  响应 Response

  - 5.1  缓冲
  - 5.2  响应头
  - 5.3  HTTP 追踪器
  - 5.4  非阻塞 IO
  - 5.5  核心方法
  - 5.6  国际化
  - 5.7  响应对象关闭
  - 5.8  响应对象存活时间
- 6  过滤 Filtering

  - 6.1  过滤器 Filter 是什么
    - 6.1.1  举个例子
  - 6.2  概念
    - 6.2.1  过滤器生命周期
    - 6.2.2  包装请求和响应
    - 6.2.3  过滤器环境
    - 6.2.4  Web 应用中的过滤器配置
    - 6.2.5  过滤器和请求分发器 RequestDispatcher
- 7  会话 Sessions

  - 7.1  会话跟踪机制
    - 7.1.1  Cookies
    - 7.1.2  SSL 会话
    - 7.1.3  URL 重写
    - 7.1.4  会话保全
  - 7.2  创建会话
  - 7.3  会话作用域
  - 7.4  绑定属性到会话
  - 7.5  会话超时
  - 7.6  上次访问时间
  - 7.7  几个重要的会话语义
    - 7.7.1  线程问题
    - 7.7.2  分布式环境
    - 7.7.3  客户端语义
- 8  注解和可插拔性

  - 8.1  注解
    - 8.1.1  @WebServlet
    - 8.1.2  @WebFilter
    - 8.1.3  @WebInitParam
    - 8.1.4  @WebListener
    - 8.1.5  @MultipartConfig
    - 8.1.6  其他注解和约定
  - 8.2  可插拔性
    - 8.2.1  web.xml 的模块化
    - 8.2.2  web.xml 和 web-fragment.xml 的顺序
    - 8.2.3  从 web.xml、web-fragment.xml 以及注解收集部署描述符
    - 8.2.4  共享类库以及运行时可插拔性
  - 8.3  JSP 容器可插拔性
  - 8.4  处理注解和部署描述片段
- 9  请求分发

  - 9.1  获取 RequestDispatcher
    - 9.1.1  请求分发器路径中的查询字段
  - 9.2  使用 请求分发器
  - 9.3  Include 方法
    - 9.3.1  涉及到的请求参数
  - 9.4  Forward 方法
    - 9.4.1  查询字段
    - 9.4.2  涉及到的请求参数
  - 9.5  错误处理
  - 9.6  获取 AsyncContext
  - 9.7  Dispatch 方法
    - 9.7.1  查询字段
    - 9.7.2  涉及到的请求参数
- 10  Web 应用

  - 10.1  Web 服务器中的 Web 应用
  - 10.2  与 ServletContext 的关系
  - 10.3  组成元素
  - 10.4  部署层级结构
  - 10.5  目录结构
    - 10.5.1  举个例子
  - 10.6  Web 应用打包文件
  - 10.7  Web 应用部署描述符
    - 10.7.1  扩展依赖
    - 10.7.2  类加载器
  - 10.8  Web 应用热更新
  - 10.9  错误处理
    - 10.9.1  请求参数
    - 10.9.2  错误页面
    - 10.9.3  错误过滤器
  - 10.10  欢迎文件
  - 10.11  Web 应用环境
  - 10.12  Web 应用部署
  - 10.13  部署描述文件 web.xml 一句话总结
- 11  应用生命周期事件

  - 11.1  介绍
  - 11.2  事件监听器
    - 11.2.1  事件类型和 Listener 接口
    - 11.2.2  举个例子
  - 11.3  监听器类配置
    - 11.3.1  监听器类规范
    - 11.3.2  部署声明
    - 11.3.3  监听器注册
    - 11.3.4  关闭时通知
  - 11.4  部署描述符举例
  - 11.5  监听器实例以及线程
  - 11.6  监听器异常
  - 11.7  分布式容器
  - 11.8  会话事件
- 12  将请求映射到 Servlets

  - 12.1  URL 路径的作用
  - 12.2  映射规范
    - 12.2.1  隐含映射
    - 12.2  举个例子
  - 12.3  运行时映射发现
    - 12.3.1  运行时 Servlet 映射发现
- 13  安全

  - 13.1  介绍
  - 13.2  声明式安全机制
  - 13.3  编程式安全机制
  - 13.4  编程式安全策略配置
    - 13.4.1  @ServletSecurity 注解
      - 13.4.1.1  例子
      - 13.4.1.2  将 @ServletSecurity 映射到安全约束
      - 13.4.1.3  将 @HttpConstraint 以及 @HttpMethodConstraint 映射到 XML
    - 13.4.2  ServletRegistration.Dynamic 的 setServletSecurity 方法
  - 13.5  角色
  - 13.6  认证
    - 13.6.1  HTTP 基本认证
    - 13.6.2  HTTP 摘要认证
    - 13.6.3  表单认证
      - 13.6.3.1  登录表单
    - 13.6.4  HTTPS 客户端认证
    - 13.6.5  附加容器认证机制
  - 13.7  认证信息的服务端追踪
  - 13.8  指定安全约束
    - 13.8.1  联合约束
    - 13.8.2  例子
    - 13.8.3  处理请求
    - 13.8.4  没有涉及到的 HTTP 方法
      - 13.8.4.1  安全约束配置规则
      - 13.8.4.2  未涉及的 HTTP 方法的处理
  - 13.9  默认策略
  - 13.10  登入和登出
- 14  部署描述符

  - 14.1  部署描述符元素
  - 14.2  部署描述符处理规则
  - 14.3  部署描述符
  - 14.4  部署描述符图示
  - 14.5  例子

    - 14.5.1  基本例子
    - 14.5.2  安全的例子
- 15  涉及到的其他规范

  - 15.1  会话
  - 15.2  Web 应用

    - 15.2.1  Web 应用类加载器
    - 15.2.2  Web 应用环境
    - 15.2.3  JNDI 以及 Web 模块路径 URL
  - 15.3  安全

    - 15.3.1  安全标识在 EJB 调用过程中的传播
    - 15.3.2  容器鉴权需求
    - 15.3.3  容器认证需求
  - 15.4  部署

    - 15.4.1  部署描述符元素
    - 15.4.2  JAX-WS 组件的打包和部署
    - 15.4.3  部署描述符处理规则
  - 15.5  注解和资源注入

    - 15.5.1  处理 metadata-complete 属性
    - 15.5.2  @DeclareRoles
    - 15.5.3  @EJB
    - 15.5.4  @EJBs 
    - 15.5.5  @Resource
    - 15.5.6  @PersistenceContext 
    - 15.5.7  @PersistenceContexts 
    - 15.5.8  @PersistenceUnit 
    - 15.5.9  @PersistenceUnits
    - 15.5.10  @PostConstruct
    - 15.5.11  @PreDestroy
    - 15.5.12  @Resources
    - 15.5.13  @RunAs
    - 15.5.14  @WebServiceRef
    - 15.5.15  @WebServiceRefs
    - 15.5.16  需要支持 Java EE 上下文和依赖注入

---

# 概述

----

## 1.1 Servlet 是什么

servlet 是一种基于 Java 的 Web 组件，由容器管理，产生动态内容。类似于其他基于 Java 的组件，servlet 也是平台无关的 Java 类，被编译称为跨平台的中间代码之后可以被任何支持 Java 的 Web 服务器动态加载并运行。容器，有时也称为 servlet 引擎，作为 Web 服务器的扩展提供对 servlet 的支持。servlets  通过容器实现的请求/响应范式与 Web 客户端互动。

## 1.2  Servlet 容器是什么？

servlet 容器作为 Web 服务器或者应用服务器的一部分，通过发送请求和响应提供网络服务。同时负责解码 MIME 请求数据和编码 MIME 类型的响应数据。servlet 整个生命周期都被容器持有和管理。

servlet 容器可以被内建进 Web 服务器，或者通过本地扩展 API 作为扩展插件安装。当然，也可以内建进或者安装进具有 Web 功能的应用服务器。

所有的 servlet 容器都必须支持 HTTP 作为请求响应协议，其他类似的请求-响应协议，例如 HTTPS (HTTP over SSL) 也可以支持。必须支持的 HTTP 协议规范版本有 HTTP/1.1 和 HTTP/2 。对于 HTTP/2，容器必须支持 “h2” 和 "h2c" 协议标识符 （在3.1章节中 HTTP/2 RFC 中规定）。这就隐含表明所有的容器都必须支持 ALPN。根据 RFC(HTTP/1.1 缓存) 所述，容器可以实现某种缓存机制，它可以在将来自客户端的请求分发到 servlet 之前修改请求，可以在将响应发送给客户端之前修改它，当然也可以根据 RFC 7234 规范直接响应请求而不把它们分发到 servlet 。

容器可以在 servlet 执行环境中布置安全约束。在 J2SE v1.3 及以上版本或者 Java EE v1.3 或以上版本环境中，这种安全约束必须采用 Java 平台定义的认证体系架构。例如某些应用服务器会限制线程对象的创建以避免对容器的其他组件产生消极影响。

此版本 servlet 容器需要的最低语言版本是 Java SE 8 。

## 1.3  例子

下面是一个典型的事件序列：

1. 客户端（比如 Web 浏览器）发起一个 HTTP 请求以访问 Web 服务器；
2. 请求被 Web 服务器接收到然后交接给 servlet 容器。容器可能和 Web 服务器运行在同一台主机的同一个进程内，可能在同一台主机的不同进程内，当然也可能运行在不同主机上；
3. 根据配置文件，容器确定应该调用哪个 servlet 处理请求，然后以请求对象和响应对象作为参数调用之；
4. 通过请求对象，servlet 可以找出远程用户信息、请求方法以及其他相关数据。执行它被赋予的程序逻辑之后，产生的数据被发回给客户端。servlet通过响应对象将结果数据发送给客户端。
5. 一旦完成请求的处理，servlet 容器确认响应数据已经完整发送，就将控制权交还给 Web 服务器。

## 1.4  Servlet 与其他技术的比较

从功能来看， servlet 提供了提供了比通用网关接口 CGI 更高一层的抽象，但是要比 JSF 之类的 web 框架的抽象层次要低一些。

servlets 相比于其他服务器扩展机制有以下优点：

- 由于采用了不同点处理模型，通常要比 CGI 脚本快。
- 采用了很多 Web 服务器都支持的标准 API 。
- 继承了 Java 语言的所有优点，包括部署简单和平台无关性。
- 可以方便地使用 Java 平台提供的大量 API 。

## 1.5  与 Java EE 平台的关系

Java Servlet API v4.0 是 Java EE 8 的一部分必要 API 。为了运行在 Java EE 环境中，容器以及部署在其中的 servlet 必须满足 Java EE 规范所描述的其他需求。

## 1.6  与 2.5 版本规范的区别

### 1.6.1  配置注解  

Servlet 2.5 中， metadata-complete 属性只是在部署过程中影响注解的扫描，而且也没有 web-fragments 的概念。在 servlet 3.0 之后，metadata-complete 属性会在部署过程中影响到所有指定部署信息的注解，同时还有 web-fragments 。部署描述符的版本绝对不能影响容器扫描应用中的注解。本规范的任何版本的实现都必须扫描所有该配置所支持的注解，除非指定了 metadata-complete 属性。

# Servlet 接口

----

Servlet 接口是 Java Servlet API 的核心抽象。所有的 servlets 都必须直接或者间接实现该接口。Java Servlet API 中已经实现了 Servlet 接口的两个类是 GenericServlet 和 HttpServlet 。大多数情况下，开发者可以继承 HttpServlet 来实现自己的 servlets 。

## 2.1  请求处理方法

基本的 Servlet 接口定义了处理客户端请求的 service 方法。每个请求到来，容器将它路由到某个 servlet 实例，该方法就会被调用。

为了处理并发请求，开发者需要将 servlet 设计成可多线程执行，也就是同一时刻可以有多个线程同时执行 service 方法。

通常容器会在多线程中执行 service 方法来处理对同一个 servlet 的多个并发请求。

### 2.1.1  HTTP 特定的请求处理方法

HttpServlet 抽象子类在基本的 Servlet 接口基础上添加了被  service 接口调用的方法，用于处理基于 HTTP 的请求。

- doGet 处理 HTTP GET 请求
- doPost 处理 HTTP POST 请求
- doPut 处理 HTTP PUT 请求
- doDelete 处理 HTTP DELETE 请求
- doHead 处理 HTTP HEAD 请求
- doOptions 处理 HTTP OPTIONS 请求
- doTrace 处理 HTTP TRACE 请求


通常，开发基于 HTTP 的 servlet 的开发者仅仅只会关注 doGet 和 doPost 方法。其他几个方法是供那些对 HTTP 协议非常熟悉的开发者使用。

### 2.1.2   附加方法

doPut 和 doDelete 方法允许 Servlet 开发者支持那些支持此类特性的 HTTP/1.1 客户端。doHead 方法是 doGet 方法的一种特殊形式，它仅仅返回 doGet 产生的响应的头部。doOptions 方法返回 servlet 都支持哪些 HTTP 方法。doTrace 方法产生的响应包含了所有的 TRACE 请求的头部实例。

CONNECT 方法不支持，因为它是作用于代理以及被绑定到服务访问点上的 Servlet API 。

### 2.1.3  条件 GET 支持

HttpServlet 抽象类定义的 getLastModified 方法支持条件 GET 操作。条件 GET 操作请求的资源，只有在某个时刻之后被修改过的情况下才会被返回给客户端。在适当的场景下，实现该方法可以改善网络资源的利用率。

## 2.2  实例个数

声明 servlet ，无论是通过注解还是部署描述符，都可以控制容器如何提供 servlet 实例。

因为默认情况下， servlet 并不是生存在分布式环境中，因此容器必须为每个 servlet 声明产生唯一的实例。然而，由于 servlet 实现了 SingleThreadModel 接口，容器可以初始化多个实例以应对大量的请求，每个请求将被分配给某个特性的实例处理。

如果 servlet 作为应用的一部分部署，而部署描述符又明确说明是分布式部署，那么容器可以为每个 Java 虚拟机提供唯一的 servlet 实例。然而，如果 servlet 实现了 SingleThreadModel 接口，容器就可以为每个虚拟机提供多个 servlet 实例。

### 2.2.1  关于 Single Thread Model 的说明

SingleThreadModel 接口的作用是保证在同一时刻只有一个线程可以执行给定 servlet 实例的 service 方法。需要特别注意的是，这个保证只是对于单个 servlet 实例而言，因为容器可以有选择地池化此类对象。那些可以同时被多个 servlet 实例访问的对象，比如 HttpSession 实例，可能在任何时刻对多个 servlet 都是可用的，SingleThreadModel 接口的实现应该包含此内容。

推荐开发者采用其他方式解决以上问题，而不要实现 SingleThreadModel 接口。比如避免使用实例变量或者将访问此类资源的代码同步化。此版本规范中 SingleThreadModel 接口已被废弃。

## 2.3  Servlet 生命周期

servlet 的管理基于定义良好的生命周期。所谓的生命周期，定义了 servlet 应该如何被加载、实例化、初始化、处理请求以及如何从服务中被移除。在 API 生命周期的形式表现为 javax.servlet.Servlet 接口的 init，service 以及 destroy 方法。所有的 servlet 都必须直接实现该接口，或者通过继承 GenericServlet 或者 HttpServlet 抽象类间接实现该接口。

### 2.3.1  加载和实例化

容器负责加载和实例化 servlets 。加载和实例化可以发生在容器启动时，或者延迟到容器真正认为需要它处理请求时。

当 servlet 引擎启动后，容器必须找到所需要的 servlet 类。容器利用通常的 Java 类的加载机制加载这些 servlet 类。可以从本地文件系统、远程文件系统甚至网络服务处加载。

加载完 Servlet 类之后，容器将实例化它们以备使用。

### 2.3.2  初始化

servelt 对象实例化之后，必须经过容器的初始化才能处理来自客户端的请求。基于初始化机制，servlet 可以读取持久化配置数据，初始化动作消耗资源（比如基于的 JDBC API 的数据库连接），同时执行其他一些一次性的活动。容器通过调用 Servlet 接口的 init 方法来初始化 servlet 实例，该方法的参数是唯一的（每个 servlet 声明）实现了 ServletConfig 接口的类对象。servlet 可以通过这个配置对象从 Web 应用的配置信息中获取“名—值”对形式的初始化参数。还可以通过该对象获取描述 servlet 运行期环境的类对象（实现了 ServletContext 接口）。关于 ServletContext 接口的更多内容将在第四章中介绍。

#### 2.3.2.1  初始化的错误

初始化过程中，servlet 实例可以抛出 UnavailableException 或者 ServletException 。这种情况下，servlet 必须被容器清理掉，不能放到活动的服务中去。这种情况被认为初始化失败，因此 destroy 方法不会被调用。

在一次失败的初始化之后，容器可以实例化和初始化新的实例。唯一需要额外说明的就是 UnavailableException 表示一个最小时间段内的不可用状态，因此容器必须等待这个时间段过去然后再开始创建并初始化下一个 servlet 实例。

#### 2.3.2.2  工具考量

静态初始化方法在工具加载并内省（反射）Web 应用过程中被触发的情况与 init 方法被调用的情况是不同的。开发者在Servlet 接口的 init 方法被调用之前都不能假定 servlet 已经在活动容器的运行时环境中了。比如说，servlet不应该在仅仅只有静态初始化方法被调用的情况下试图建立与数据库或者 EJB 容器的连接。

### 2.3.3  请求处理

servlet 正确初始化之后，就可以被容器用来处理客户端请求。请求由 ServletRequest 类型的请求对象表示。servlet 调用相应的处理方法并以 ServletResponse 类型的对象填充响应。这些对象作为参数被传递给 Servlet 接口的 service 方法。

如果是 HTTP 请求，容器提供的对象类型就是 HttpServletRequest 和 HttpServletResponse 。

特别的，被容器放进服务中的 servlet 实例可以在整个生命周期内不处理任何请求。

#### 2.3.3.1  多线程问题

servlet 容器可以通过 servlet 的 service 方法发送并发请求。为了处理这些请求，servlet 开发者必须保证 service 方法的实现具有处理并发请求的能力。

尽管不推荐，开发者可以采取实现 SingleThreadModel 接口的方式来要求容器保证同一时刻只有一个请求线程处于 service 方法内部。容器可以通过串行化请求或者将 servlet 实例池化的方式来满足此要求。如果应用已经被被指为可分布式的，那么当应用分布式部署时容器将在每个 JVM 内部都维护一个 servlet 实例池。

由于 servlet 并未实现 SingleThreadModel 接口，如果 service 方法（或者由该方法分发到的 HttpServlet 抽象类的 doGet 或者 doPost 方法）被 synchronized 关键字修饰，容器将无法采用池化技术，而不得不强行将请求串行化。强烈建议开发者在这种环境下不要同步化 service 方法（或者由它分发到的方法），因为这将对性能造成决定性的影响。

#### 2.3.3.2  请求处理过程中的异常

处理请求过程中 servlet 可以抛出 ServletException 或者 UnavailableException 异常。ServletException 表示在处理请求过程中发生了某些错误因而容器应该采取对应措施将请求清除掉。

UnavailableException 表示 servlet 暂时或者永久性地无法处理请求。

如果 UnavailableException 表示永久性的不可用，容器就必须从服务中清除该 servlet ，调用它的 destroy 方法，然后释放该 servlet 实例。由此导致的被决绝的请求都必须返回 SC_NOT_FOUND (404) 响应。

如果 UnavailableException 表示暂时性的不可用，容器可以选择在这段不可用的时间内不再将请求路由到该 servlet 。所有因此而被拒绝的请求都必须返回 SC_SERVICE_UNAVAILABEL (503) 状态的响应，同时附带 Retry-After 响应头用于表示不可用状态何时结束。

容器可以选择不区分这两种情况，而认为 UnavailableException 就是表示永久性的不可用，而后直接将抛出该异常的 servlet 从服务中清除掉。

#### 2.3.3.3  异步处理

有时候一个过滤器和一个 servlet 不能立即完成请求的处理，比如需要等待其他资源，有时候甚至是等待响应的产生。比如，servlet 在产生响应之前可能需要等待可用的 JDBC 连接，来自远程服务的响应，JMS 消息，或者应用事件。等待这样的 servlet 是低效率的操作，因为它是一个阻塞性的行为，消耗线程和其他有限资源。很多时候，像数据库之类的慢资源会导致大量等待存取的线程阻塞，因而会导致线程饥饿甚至是整个 web 容器的服务质量下降。

请求的异步处理机制的目的是允许将线程归还给容器执行其他任务。当请求的异步处理过程开始之后，另外一个线程或者回调可以要么产生响应然后调用 complete 方法，要么使用 AsyncContext.dispatch 方法分发请求因而它可以在容器的上下文中运行。典型的异步处理事件序列如下：

1. 请求被接收到，通过正常的过滤器，比如身份认证，到达 servlet 。

2. servlet 处理请求参数和请求内容以确定请求自身的特性。

3. servlet 发出资源或者数据请求，比如，发送请求到远程服务或者加入 JDBC 连接的等待队列。
4. servlet 立即返回，并不产生响应。
5. 一段时间之后，请求的资源变为可用状态，处理该事件的线程要么在本线程内继续处理，要么通过 AsyncContext 将请求分发到容器内的资源。

Java EE 特性，比如 15.2.2 节中的 “ Web 应用环境 ” 和 15.3.1 节中 “ 安全标识在 EJB 调用过程中的传播 ” ，都只是对处理初始请求的线程或者处理通过 AsyncContext.dispatch 方法分发到容器的请求的线程可用。  也可以对通过 AsyncContext.start ( Runnable ) 方法直接处理响应对象的其他线程可用。

第八章中描述的 @WebServlet 和 @WebFilter 注解包含一个 boolean 类型的参数 asyncSupported ，默认值 false 。该属性为 true 时应用就能通过调用 startAsync 方法在独立的线程中开始异步处理，传递请求和响应对象的引用，然后在最初的线程上从容器退出。这意味着响应将逆序遍历相同的过滤器链，刚好跟请求进入的路径相反。响应直到 AsyncContext 上的 complete 方法被调用后才会被提交。应用负责在容器调用 startAsync 初始化分发的处理任务结果返回容器之前处理执行中的异步任务对请求和响应对象的并发访问。

从 asyncSupported=true 的 servlet 分发请求到 asyncSupported=false 的 servlet 是允许的。这种情况下，响应在不支持异步的 servlet 的 service 方法退出之后才会被提交，而容器需要负责调用 AsyncContext 上的 complete 方法从而通知所有关注中的 AsyncListener 实例。AsyncListener.onComplete 通知也应该被过滤器使用，作为提供给异步任务执行的资源的清理机制。

从同步 servlet 分发请求到异步 servlet 是不行的。不过抛出 IllegalStateException 的时机取决于应用合适调用 startAsync 方法。这将允许 servlet 可以同步或者异步执行。

应用等待的异步任务可以通过另一个线程直接将结果写入响应，而不是必须在最初接收请求的线程中进行。这个另外的线程完全不知道任何过滤器的存在。如果一个过滤器想要在这个新的线程中操作响应，它就必须在请求进入时处理它并包装相应的响应，然后将这个响应一并传递给过滤器链上的下一个过滤器，最终到达 servlet 。因此，如果响应被包装（可能会包装很多层，每个过滤器一层），而后应用处理请求并直接讲返回数据写入响应，实际上是在向响应包装器写入数据，例如，任何被添加到响应中的数据都将被响应包装器处理。当应用从一个单独的线程中读取请求，并且将输出添加到响应中，实际上它是从请求包装器中读取，写入到响应包装器中，因此，包装器可能会持续不断地执行任何输入输出操作。

另一方面，如果应用选择这样做，它就可以基于 AsyncContext 将请求从新的线程分发到容器内的资源。这种情况可以采用相应的内容产生技术，比如容器管理下的 JSP 。

为了配合上述的注解属性，我们添加了以下方法和类：

> ServletRequest

* public AsyncContext startAsyc ( ServletRequest  req , ServletResponse res )

  这个方法将请求转化为异步模式，基于给定的请求对象和响应对象以及 getAsyncTimeout 方法返回的超时时间初始化对应的 AsyncContext 。其中作为参数的 ServletRequest 和 ServletResponse 必须要么和被传递给 servlet 的 service 方法、或者过滤的 doFilter 方法的是同一个对象，要么是包装它们的 ServletRequestWrapper 或者 ServletResponseWrapper 的子类。调用本方法可以保证响应在应用退出 service 方法之前不会被提交。响应的提交时机是返回的 AsyncContext 上的 AsyncContext.complete 方法被调用、或者 AsyncContext 超时而又没有相应的监听器处理该超时事件。异步超时的定时器在请求连同对应的响应从容器返回之前不会开始计时。AsyncContext 可以用于从异步线程中将数据写入响应。当然也可以仅仅用来将响应尚未关闭和提交的通知消息发送出来。

  以下情形调用 startAsync 是非法的：请求处于不支持异步操作的 servlet 或者过滤器的作用域中，或者响应已经被提交和关闭，或者通过同一次 dispatch 的再次调用。调用 startAsync 返回的 AsyncContext 接下来可以被用于后续的异步处理过程。在返回的 AsyncContext 上调用 AsyncContext.hasOriginalRequestResponse ( ) 将得到返回 false ，除非参数 ServletRequest 和 ServletResponse 都是最初的对象，或者尚未被应用包装过。任何响应返回方向上的过滤器在请求进入异步模式之后都可能将其作为标记，标记某些在请求进入路径上由它们添加的请求或者响应包装器，在异步操作中这些包装器可能需要保持不变，有关的资源可能不会被释放。一个在请求进入路径上被某个过滤器添加的 ServletRequestWrapper 可能在响应返回路径上被该过滤器释放，前提是用于初始化 AsyncContext 的 ServletRequest 将在 AsyncContext.getRequest ( ) 方法调用时被返回，而并不包含上面所说的 ServletRequestWrapper 。同样的规则也适用于 ServletResponseWrapper 实例。

* public AsyncContext startAsync ( ) 

  此方法的目的是方便在异步处理中使用初始的请求和响应对象。注意！此方法的用户应该将输出倾倒干净，如果在调用此方法之前他们对响应进行过包装，用户需要确保所有需要写入包装后的响应的数据已经全部写入。

* public AsyncContext getAsyncContext ( ) 

  返回调用 startAsync 方法创建或者重新初始化的 AsyncContext 。如果请求尚未处于异步状态，调用此方法是非法的。

* public boolean isAsyncSupported ( ) 

  如果请求支持异步处理则返回 true ，否则返回 false 。一旦请求经过不支持异步处理的 ( 通过注解或者声明 ) 过滤器或者 servlet 处理，请求马上就会变为不支持异步状态。

* public boolean isAsyncStarted ( )

  如果请求的异步处理已经开始，则返回 true ，否则返回 false 。如果请求已经被通过 AsyncContext.dispatch 方法分发，因此它已经进入异步模式，或者 AsyncContext.complete 被调用，则此方法返回 false 。

* public DispatcherType getDispatcherType ( )

  返回请求的分发器类型。容器根据请求的分发器类型选择哪些过滤器应该被应用与该请求。只有分发器类型和 url 模式都匹配的过滤器才会应用与请求。允许被配置了多种分发器类型的过滤器根据请求的不同分发器类型对请求采用不同的处理方式。初始的分发器类型定义为 DispatcherType.REQUEST 。被分发过的请求的分发器类型由分发方式决定，RequestDispatcher.forward ( ServletRequest, ServletResponse ) 产生的分发器类型是 DispatcherType.FORWARD ，而 RequestDispatcher.include ( ServletRequest, ServletResponse ) 产生的分发器类型是 DispatcherType.INCLUDE 。通过 AsyncContext.dispatch 方法分发的异步请求的分发器类型就是 DispatcherType.ASYNC 。最后，被容器的错误处理机制分发到错误页面的请求的分发器类型是 DispatcherType.ERROR 。

> AsyncContext

此类型表示开始于 ServletRequest 之上的异步操作的执行上下文。上文说过，当 ServletRequest.startAsync 被调用时 AsyncContext  被创建和初始化。下面列出该类的方法。

* public ServletRequest getRequest ( )

  返回通过调用 startAsync 方法用于初始化 AsyncContext 的请求。在异步周期中 complete 或者任何 dispatch 方法被调用之后再调用 getRequest 方法都会导致 IllegalStateException 。

* public ServletResponse getResponse ( )

  返回通过调用 startAsync 方法用于初始化 AsyncContext 的响应。在异步周期中 complete 或者任何 dispatch 方法被调用之后再调用 getResponse 方法都会导致 IllegalStateException 。

* public void setTimeout ( long timeoutMilliseconds )

  设定异步处理超时时间毫秒数。容器会调用此方法用来设置超时时间。如果没有通过此方法设置超时时间，则默认为30000 。0 或者更小的值表示异步操作将永远不会超时。一旦容器初始化分发开始，这个超时时间就将作用于 AsyncContext ，衡量的时间是 ServletRequest.startAsync 方法被调用直到返回容器为止。在异步周期被开始的容器初始化分发已经返回容器之后设置超时时间是非法的，此时调用此方法会导致 IllegalStateException 。

* public long getTimeout ( )

  获取 AsyncContext 关联的超时毫秒数。此方法返回的要么是容器默认的超时毫秒数，要么是最近一次调用 setTimeout 方法设定的超时毫秒数。

* public void addListener ( AsyncListener listener, ServletRequest req, ServletResponse res ) 

  注册用于监听 onTimeout、 onError、onComplete 或者 onStartAsync 通知的监听器。前三个通知跟最近的通过调用 ServletRequest.startAsync 方法启动的异步周期有关。而 onStartAsync 则跟下一个通过调用 ServletRequest.startAsync 方法启动的新的异步周期相关。异步监听器将按照它们被添加到请求上的顺序依次被通知到。传入方法的请求和响应对象在监听器接收到通知时可以通过 AsyncEvent.getSuppliedRequest ( ) 和 AsyncEvent.getSuppliedResponse ( ) 方法获取。这些对象不应该被读取或者写入，因为由于 AsyncListener 的注册，可能会发生附加的对请求和响应对象的包装。不过这些对象可以用于释放相关资源操作。当容器初始化分发的异步周期开始并已经返回容器，而新的异步周期已经开始的时刻，调用此方法将导致 IllegalStateException 。

* public < T extends AsyncListener > createListener ( Class< T >  clazz ) 

  实例化给定的 AsyncListener 。返回的 AsyncListener 实例在通过下面将要说到的 addListener  方法注册到 AsyncContext 之前可以被进一步定制。作为参数的 AsyncListener 必须定义一个无参构造器用来实例化。此方法支持任何 AsyncListener 适用的注解。

* public void addListener ( AsyncListener ) 

  注册用于监听 onTimeout、 onError、onComplete 或者 onStartAsync 通知的监听器。前三个通知跟最近的通过调用 ServletRequest.startAsync 方法启动的异步周期有关。而 onStartAsync 则跟下一个通过调用 ServletRequest.startAsync 方法启动的新的异步周期相关。如果请求上的 startAsync ( req, res ) 或者 startAsync ( ) 方法被调用，则请求和响应对象可以从 AsyncListener 监听到的通知事件 AsyncEvent 中获取。当然，此时的请求和响应可以是包装过的或者尚未包装过的。异步监听器将按照它们被添加到请求上的顺序依次被通知到。当容器初始化分发的异步周期开始并已经返回容器，而新的异步周期已经开始的时刻，调用此方法将导致 IllegalStateException 。

* public void dispatch ( String path ) 

  将用于初始化 AsyncContext 的请求和响应分发到给定路径对应的资源。给定的路径基于用于初始化 AsyncContext 的 ServletContext 进行解释。所有查询类型的请求路径必须说明分发对象，同时，初始的请求 URI、Context Path、路径信息以及请求字符串可以从请求属性中获取，具体细节在9.7.2章节中说明。这些属性必须始终反映最初的请求路径元素，及时经过多次分发。

* public void dispatch ( ) 

  将用于初始化 AsyncContext 的请求和响应分发的快捷方法。如果通过 startAsync ( ServletRequest, ServletResponse ) 初始化 AsyncContext ，而且作为参数传入的请求是一个 HttpServletRequest 实例，接下来分发到的 URI 可以通过 HttpServletRequest.getRequestURI ( ) 方法获取。否则该分发将转向请求最后一次被容器分发时的 URI 。下面的代码实例说明了不同情况下的分发目标 URI 。

  ````java
  // REQUEST to /url/A
  AsyncContext ac = request.startAsync();
  ...
  ac.dispatch();	// ASYNC dispatch to /url/A
  ````

  ````java
  // REQUEST to /url/A
  // FORWARD to /url/B
  request.getRequestDispatcher("/url/B").forward(request, response);
  // Start async operation from within the target of the FORWARD
  AsyncContext ac = request.startAsync();
  ac.dispatch();	// ASYNC dispatch to /url/A
  ````

  ````java
  // REQUEST to /url/A
  // FORWARD to /url/B
  request.getRequestDispatcher("/url/B").forward(request, response);
  // Start async operation from within the target of the FORWARD
  AsyncContext ac = request.startAsync(request, response);
  ac.dispatch();	// ASYNC dispatch to /url/B
  ````

* public void dispatch( ServletContext context, String path ) 

  在给定的 ServletContext 环境下将用于初始化 AsyncContext 的请求和响应分发到给定路径对应的资源。

  以上3种 dispatch 方法，方法调用在将请求对象和响应对象传递给容器管理的线程之后会立即返回，该线程中执行分发操作。请求的分发器类型将被设置为 ASYNC 。不像 RequestDispatcher.forward( ServletRequest, ServletResponse ) 分发，响应缓冲和响应头部将不会被重置，而且在响应被提交之后进行分发就是非法的。对请求和响应的控制都委托给了分发目标，当分发目标执行完成之后响应就会被关闭。除非 ServletRequest.startAsync( ) 或者 ServletRequest.startAsync( ServletRequest, ServletResponse ) 被调用。如果有任何分发方法在调用 startAsync 方法的容器初始分发返回容器之前被调用，则在 dispatch 方法被调用直至控制权返回容器期间，下面的条件就必须保持。

  1. 任何 dispatch 调用在此期间都将不生效，直到容器初始分发返回容器。
  2. 任何 AsyncListener.onComplete( AsyncEvent ) ， AsyncListener.onTimeout( AsyncEvent ) ， AsyncListener.onError( AsyncEvent ) 调用都将延迟到容器初始分发返回容器之后。
  3. 任何 request.isAsyncStarted( ) 在容器初始分发返回容器之前都必须返回 true 。

  每个异步周期内最多只能有一个异步分发操作，它由 ServletRequest.startAsync 方法的一次调用开启。一个异步周期内任何执行额外的异步分发操作的企图都是非法的，将导致 IllegalStateException 。如果 startAsync 方法随后在被分发的请求上被调用，接下来任何 dispatch 方法的调用都需要满足上述约束。

  在 dispatch 方法执行过程中发生的任何错误和异常都必须被容器捕获并处理。处理方法如下：

  1. 调用所有注册到 ServletRequest 上的 AsyncListener 实例的 AsyncListener.onError( AsyncEvent ) 方法。同时通过 AsyncEvent.getThrowable( ) 暴露 Throwable 。
  2. 如果没有任何监听器调用 AsyncContext.complete 或者 AsyncContext.dispatch 方法，就执行指向错误页面的分发，此时状态码是 HttpServletResponse.SC_INTERNAL_SERVER_ERROR ，然后暴露 Throwable ，同时给请求属性赋值 RequestDispatcher.ERROR_EXCEPTION 。
  3. 如果没有匹配到错误页面，或者错误页面没有调用 AsyncContext.complete( ) 或者任何 AsyncContext.dispatch 方法，容器就必须自己调用 AsyncContext.complete 方法。

* public boolean hasOriginalRequestAndResponse( ) 

  此方法检查 AsyncContext 是否通过调用 ServletRequest.startAsync( ) 方法由初始的请求对象和响应对象初始化，或者通过调用 ServletRequest.startAsync( ServletRequest, ServletResponse ) 方法初始化，并且其中的 ServletRequest 和 ServletResponse 都没有经过任何包装，如果是这样，此方法返回 true 。如果通过 ServletRequest.startAsync( ServletRequest, ServletResponse ) 方法进行的 AsyncContext 的初始化基于包装过的请求和响应对象，此方法返回 false 。此信息可以被响应返回方向上的过滤器使用，在请求进入异步模式之后，决定在请求进入方向上由它们对请求和响应进行的包装在异步操作过程中是应当保留还是释放。

* public void start( Runnable r ) 

  此方法会导致容器分发一个线程，可能是从容器管理下的线程池中获取，以运行给定的 Runnable 。容器可以传递适当的上下文信息给该 Runnable 。

* public void complete( ) 

  如果 request.startAsync 被调用了，那么此方法就必须被调用以完成异步处理过程并提交和关闭响应。此方法能够被容器调用，如果请求被分发给不支持异步的 servlet ，或者 AsyncContext.dispatch 的目标 servlet 并没有接下来调用 startAsync 方法。这种情况下，容器就需要在servlet 的 service 方法退出时马上调用 complete 方法。如果 startAsync 方法没有被调用，则必须抛出 IllegalStateException 。在 ServletRequest.startAsync( ) 或者  ServletRequest.startAsync( ServletRequest, ServletResponse ) 方法调用之后，同时在任何的分发方法被调用之前，调用此方法都是合法的。如果此方法在调用 startAsync 方法的容器初始分发返回容器之前被调用，则如下条件就必须在 complete 方法调用直到控制权返回容器期间保持不变：

  1. 指定 complete 的特定行为将不生效，直到容器初始分发返回容器；
  2. 任何 AsyncListener.onComplete( AsyncEvent ) 调用都将延迟到容器初始分发返回容器；
  3. 任何 request.isAsyncStarted( ) 调用都必须返回 true ，直到容器初始分发返回容器。

> ServletRequestWrapper

* public boolean isWrapperFor( ServletRequest req ) 

  递归检查是否此包装器已经包装了给定的 ServletRequest ，是返回 true ，否则返回 false 。

> ServletResponseWrapper

* public boolean isWrapperFor( ServletResponse res ) 

  递归检查是否此包装器已经包装了给定的 ServletResponse ，是返回 true ，否则返回 false 。

> AsyncListener

* public void onComplete( AsyncEvent event ) 

  用于通知事件监听器开始于 ServletRequest 之上异步操作已经完成。

* public void onTimeout( AsyncEvent event ) 

  用于通知事件监听器开始于 ServletRequest 之上异步操作已经超时。

* public void onError( AsyncEvent event ) 

  用于通知事件监听器开始于 ServletRequest 之上异步操作已经失败。

* public void onStartAsync( AsyncEvent event ) 

  用于通知事件监听器一个新的异步周期已经通过 ServletRequest.startAsync 方法调用被初始化。对应于这个新的被重新初始化的异步操作的 AsyncContext 可以通过 AsyncEvent.getAsyncContext 方法从给定事件中获取。

对于异步操作超时事件，容器必须执行以下步骤：

* 在该异步操作初始化对应的 ServletRequest 上注册的所有 AsyncListener 实例上调用 AsyncListener.onTimeout 方法。
* 如果所有监听器都没有调用 AsyncContext.complete( ) 或者任何 AsyncContext.dispatch 方法，则执行指向错误页面的分发，状态码为 HttpServletResponse.SC_INTERNAL_SERVER_ERROR 。
* 如果没有找到匹配的错误页面，或者错误页面也没有调用 AsyncContext.complete( ) 或者任何 AsyncContext.dispatch 方法，则容器必须自己调用 AsyncContext.complete( ) 方法。
* 如果在调用 AsyncListener 的方法是发生异常，应该把异常纪录在日志里，而不能影响其他的 AsyncListener 。
* JSP 的异步处理被用于内容产生默认不支持，同时异步处理必须在内容产生之前完成。处理这种情况是容器的能力范围。一旦所有的异步活动都结束，指向 JSP 页面的分发，尽管采用了 AsyncContext.dispatch ，仍然可以用于内容产生。

下面的图展示了所有异步操作的状态变迁：

![异步操作的状态变迁](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181223193212373-5564732.png)


#### 2.3.3.4  线程安全

不同于 startAsync 和 complete 方法，请求和响应对象的实现都不保证线程安全。这意味着要么它们仅仅在处理请求的线程作用域内使用，要么应用必须保证对请求和响应对象的访问是线程安全的。

如果一个线程由应用创建，使用容器管理下的对象，比如请求和响应对象，访问这些对象必须在它们的生命周期之内，对象的声明周期定义在下文3.13章节，“ 请求对象的生命周期 ”，以及5.8章节，“ 响应对象的生命周期 ”。注意，不同于 startAsync 和 complete 方法，请求和响应对象都不是线程安全的。如果这些对象在多线程环境中被访问，则访问必须被同步，或者通过一个包装器来添加线程安全。比如，同步所有对访问请求参数方法的调用，或者对一个线程内的响应对象使用本地输出流。

#### 2.3.3.5  升级处理

在 HTTP/1.1 中，升级通用头部允许客户端指定它所支持的或者希望使用的附加通信协议。服务器根据该头部切换协议，然后后续的通信中就将采用新的协议。

Servlet 容器提供了 HTTP 升级机制，然而容器本身并不了解协议升级。协议处理被封装在 HttpUpgradeHandler 中。容器和 HttpUpgradeHandler 之间的数据读写都是字节流形式。

当携带协议升级信息的请求到来， servlet 能够调用 HttpServletRequest.upgrade 方法启动协议升级过程。该方法实例化给定的 HttpUpgradeHandler 类。返回的实例可以被进一步定制化。应用准备好并发送一个合适的响应给客户端。退出 servlet 的 service 方法之后，容器完成所有过滤器的处理同时将连接标记为需要 HttpUpgradeHandler 处理。然后它调用 HttpUpgradeHandler 的 init 方法，传入一个 WebConnection 以允许协议处理器访问数据流。

Servlet 过滤器仅仅处理初始的 HTTP 请求和响应。它们不会参与后续的通信。换句话说，一旦请求升级，它们就不会再被调用。

HttpUpgradeHandler 可以采用非阻塞式 IO 消费和生产消息。

在处理 HTTP 协议升级的过程中，开发者需要保证访问 ServletInputStream 和 ServletOutputStream 的线程安全性。

当协议升级完成， HttpUpgradeHandler.destroy 方法将被调用。

### 2.3.4  服务结束

Servlet 容器不需要保持任何时间点的 servlet 都被加载。servlet 实例在容器中可以存活若干毫秒，跟随容器的生命周期，几天，几个月或者几年，或者随便多长时间。

当容器认为一个 servlet 实例应该从服务中移除，它将调用  Servlet 接口的 destroy 方法，允许该实例释放它所使用的所有资源，保存所有持久化状态。比如，容器进行内存回收或者被关闭时就会这么做。

容器在调用 destroy 方法之前，必须允许当前运行在 service 方法中的所有线程完成运行，或者至少是执行一个服务器预定义的截止时间。

一旦 servlet 实例上的 destroy 方法被调用，容器就不再将其他请求路由到该实例。如果容器需要重新使用该 servlet，就必须重新实例化该 servlet 。

destroy 方法执行完成之后，容器必须释放该 servlet 实例，保证它可以被虚拟机垃圾回收。

----

# 请求

----

请求对象封装了所有来自客户端请求的信息。在 HTTP 协议中，这些信息放在请求的 HTTP 协议头和消息体中从客户端传递给服务器。

## 3.1 HTTP 协议参数

Servlet 的请求参数就是一些由客户端发送给 servlet 容器的一些字符串，它们作为请求的一部分。当请求是 HttpServletRequest 对象，同时满足 “ 何时请求参数可用 ” 条件，容器将从请求的 URI 查询字符串中或者从被 POST 过来的数据中获取这些参数。

这些参数通常以 “ 名－值 ” 对的形式存储。任何参数名称都可以有任意复杂程度的参数值。ServletRequest 接口的下列方法可用于访问参数：

* getParameter
* getParameterNames
* getParameterValues
* getParameterMap

getParameterValues 方法返回一个字符串数组，包含了对应于参数名称的所有参数值。getParameter 方法的返回值必须是 getParameterValues 方法返回的字符串数组的第一个返回值。getParameterMap 方法返回请求参数的 java.util.Map ，其中参数名是键，参数值是值。

从查询字符串和 post 请求体中得到的数据都被放进请求参数集合。查询字符串放在 post 请求体数据之前。例如，如果请求携带的查询字符串是 a=hello 而 post 体中的数据是 a=goodbye&a=world ，则最终参数集合会是 a=(hello, goodbye, world ) 。

路径变量作为 GET 请求（由 HTTP 1.1 定义）的一部分，并不通过此接口暴露。它们必须由 getRequestURI 方法或者 getPathInfo 方法返回的字符串转化而来。

### 3.1.1 何时请求参数可用

只有当下面条件满足时 post 过来的表单数据才会被加入请求参数集合：

1. 请求是 HTTP 或者 HTTPS 请求。
2. HTTP 方法是 POST 。
3. 内容类型是 application/x-www-form-urlencoded。
4. servlet 已经执行过请求对象上的 getParameter 方法族中任一方法的初始化调用。

如果条件不满足，则表单数据就不会被加入请求参数集合，那么 post 数据就必须仍然可以让 servlet 通过请求对象的输入流中获取到。如果条件满足，post 表单数据就将不再能直接从请求对象的输入流中读取。

## 3.2 文件上传

Servlet 容器支持文件上传，此时 content-type 设置为 multipart/form-data 。

当下列任一条件满足时容器提供 multipart/form-data 处理功能：

* 处理该请求的 servlet 被 @MultipartConfig 注解修饰，该注解在章节8.1.5中定义。
* 部署描述文件中处理该请求的 servlet 描述包含 multipart-config 元素。

内容类型为 multipart/form-data 的请求数据是否可以访问以及如何访问取决于 servlet 容器是否提供 multipart/form-data 处理功能：

* 如果容器提供该处理功能，可以通过 HttpServletRequest 的下列方法访问请求数据：

  * public Collection\<Part\> getParts( )
  * public Part getPart( String name )

  通过 Part.getInputStream 方法，每个 part 都支持访问头部、内容类型以及内容。

  作为 Content-Disposition 的 form-data 部分，并没有文件名，不过仍然可以通过 HttpServletRequest 的 getParameter 和 getParameterValues 方法访问器字符串值。

* 如果容器没有提供该处理功能，则数据可以通过 HttpServletRequest.getInputStream 方法访问。

## 3.3 属性

属性是一些与请求相关的对象。容器可以设置属性用于表示某些无法通过 API 表达的信息。Servlet 也可以设置属性用于通过 RequestDispatcher 与其它 servlet 通信。属性通过 ServletRequest 接口的下列方法访问：

* getAttribute
* getAttributeNames
* setAttribute

每个属性名只能关联唯一一个属性值。

作为本规范的保留规则，所有的属性名都要以 java. 或者 javax. 这样的前缀开始。类似的，Oracle 公司的保留规则是所有的属性名以 sun. 或者 com.sun.  或者 oracle 或者 com.oracle 等前缀开头。建议所有被放进属性集合的属性都以逆序域名开始，就像 Java 语言规范中关于包命名规范的约定。

## 3.4 头部

servlet 可以通过 HttpServletRequest 接口的下列方法访问 HTTP 请求的头部：

* getHeader
* getHeaders
* getHeaderNames

getHeader 方法返回指定名称的头部字段。HTTP 请求可以有多个同名的头部字段，比如 Cache-Control ，这种情况下，getHeader 方法返回其中的第一个。而 getHeaders 方法可以将给定名称的头部字段的值以字符串 Enumeration 形式返回。

头部可以包含字符串形式的 int 或者 Date 数据。可以用 HttpServletRequest 接口的下面几个方法访问这些数据：

* getIntHeader
* getDateHeader

如果 getIntHeader 方法无法将给定的头部字段值转化为 int ，将会抛出 NumerFormatException 。如果 getDateHeader方法无法将给定的头部字段值转化为 Date ，将会抛出 IllegalArgumentException 。

## 3.5 请求路径元素

请求路径，用于将请求指引到为它提供服务的 servlet ，由几部分构成。以下元素可以通过请求对象从请求 URI 路径中获取：

* Context Path：servlet 所在的 ServletContext 路径的前缀。如果该 context 是所谓的默认 context ，则它处在 web server 的 URL 命名空间的根路径上，此时本路径片段就是空字符串。否则，这个路径片段就会以 "/" 字符开头，但是并不以 “/” 字符结尾。
* Servlet Path：本路径片段直接对应于请求对应的映射关系。它以 "/" 字符开始，除非请求符合 “/*” 或者 "" 映射关系，此时本路径片段是空字符串。
* PathInfo：请求路径剩余的部分，要么是空，要么是 "/" 开头的字符串。

HttpServletRequest 接口中的下列方法用来访问这些信息：

* getContextPath
* getServletPath
* getPathInfo

重要提示：除了 URL 编码的差异，请求 URI 和路径各个部分之间始终满足如下等式：

requestURI = contextPath + servletPath + pathInfo

举个例子：

Context 配置

````xml
Context Path		/catalog
Servlet Mapping		Pattern: /lawn/*
					Servlet: LawnServlet
Servlet Mapping		Pattern: /garden/*
					Servlet: GardenServlet
Servlet Mapping		Pattern: *.jsp
					Servlet: JSPServlet
````

相应的行为：

````xml
Request Path					Path Element
/catalog/lawn/index.html		ContextPath: /catalog
								ServletPath: /lawn
								PathInfo: /index.html
/catalog/garden/implements		ContextPath: /catalog
								ServletPath: /garden
								PathInfo: /implements
/catalog/help/feedback.jsp		ContextPath: /catalog
								ServletPath: /help/feedback.jsp
								PathInfo: null
````

## 3.6 路径转化方法

API 中有两个方法允许开发者获取特定的请求路径对应的系统路径：

* ServletContext.getRealPath
* HttpServletRequest.getPathTranslated

getRealPath 方法需要一个字符串类型的参数，返回一个字符串，表示请求路径对应的文件在本地文件系统中的位置。getPathTranslated 方法计算请求的 pathInfo 的真实路径。

某些情况下，servlet 容器无法确定有效的文件路径，比如说，当 Web 应用从打包文件启动，或者运行在远程文件系统上，或者运行在数据库服务器上，此时这两个方法都必须返回 null 。

JAR 包内部 META-INF/resources 目录下的资源文件需要被考虑到，只要容器将它们解压出来。如果 getRealPath( ) 方法被用于获取这些资源的路径，那么就必须返回解压后的文件位置。

## 3.7 非阻塞 IO

非阻塞式的请求处理可以提升 Web 容器的处理性能和可伸缩性，增加 Web 容器可以并发处理的连接数。servlet 容器中的非阻塞式 IO 机制允许开发者在数据可用时才及时读取或者写入。非阻塞式 IO 仅仅可以和 Servlets 和 Filters 中的异步请求处理协同工作，或者在协议升级过程中工作。否则，当调用 ServletInputStream.setReadListener 或者 ServletOutputStream.setWriteListener 方法时就必须抛出 IllegalStateException 异常。

ReadListener 为非阻塞 IO 提供了如下回调方法：

* ReadListener
  * onDataAvailable()  当数据可以从到来的请求数据流中读取时 ReadListener 上的 onDataAvailable 方法被调用。当数据可读取时容器会首次调用此方法。当且仅当 ServletInputStream 上的 isReady 方法被调用并返回 false 时容器会再次调用此方法，然后数据就变为可读取状态。
  * onAllDataRead()  当注册了 Listener 的 ServletRequest 中的数据读取完成时此方法会被调用。
  * onError( Throwable t )  当请求处理过程中发生任何错误或异常时此方法被调用。

Servlet 容器必须以线程安全的模式访问 ReadListener 的方法。

除此之外，ServletInputStream 中也添加了以下方法：

* ServletInputStream
  * boolean isFinished() 当请求关联的 ServletInputStream 中所有数据都被读取完毕时返回 true ，否则返回 false 。
  * boolean isReady() 当数据可以被读取而无需等待时返回 true ，否则返回 false 。当 isReady 方法返回 false 情况下调用读取方法必须抛出 IllegalStateException 。
  * void setReadListener( ReadListener listener ) 为数据的非阻塞读取方式设置上述的 ReadListener 。一旦此监听器与给定的 ServletInputStream 建立联系，当数据可以读取时容器就会调用监听器上的此方法，所有的数据都会被读取，除非请求处理过程中发生了错误。ReadListener 的注册将启动非阻塞 IO 。此时试图切换回传统的阻塞式 IO 是非法的，必须抛出 IllegalStateException 异常。当前请求作用域内 setReadListener 的再次调用是非法的，必须抛出 IllegalStateException 异常。

## 3.8 HTTP/2 服务端推送

HTTP/2 在 servlet API 中最明显的改进就是服务端推送。包括服务端推送在内的所有 HTTP/2 改进目的都是改善浏览器的用户体验。该特性可以奏效是基于这样的事实，那就是，服务端相对于客户端来说，在判断请求需要的额外资源（比如图片、样式表或者脚本等）方面，显然具有优势的。例如，当浏览器请求 ````index.html ```` 时，它肯定会接下来马上请求 ```` header.gif````、````footer.gif ```` 以及 ````style.css ```` 等，对服务端来说，获得这种认识是可能的。一旦获取了这些知识，服务端就可以在发送 ```` index.html ```` 的同时提前发送这些资源数据。

使用服务端推送，需要从```` HttpServletRequest ````中获取````PushBuilder````引用，按需修改它，然后调用````push()````方法。请参考````javax.servlet.http.HttpServletRequest.newPushBuilder()````方法和````javax.servlet.http.PushBuilder````类的规范文档。本章节剩余部分对应于附录 “其它重要参考文献” 中的 HTTP/2 规范文档中的 "Server Push" 部分。

除非显式排除，所有 Servlet 4.0 容器都必须遵循 HTTP/2 规范中 “Server Push” 部分内容支持服务端推送。当客户端使用 HTTP/2 协议时容器必须保证服务端推送可用，除非客户端通当前连接发送值为0的 SERRINGS_ENABLE_PUSH 信号显式关闭服务端推送。此时，对当前连接来说，服务端推送必须不可用。

除了客户端通过上述设置主动关闭服务端推送的情况，当客户端请求不能接收推送响应时，servlet 容器必须将推送数据流标识为 CANCEL 或者 REFUSED_STREAM 。通常当资源在客户端缓存中已经存在时会出现这种交互。

## 3.9 Cookies

````HttpServletRequest````接口提供了````getCookies````方法用于从请求中获取 cookies 数组。这些 cookies 随着客户端产生的请求被发送到服务端。典型的情况，客户端向服务端发送的 cookie 只包含名值对。其他可以在服务端设置的 cookie 属性，比如注释等，都不会被客户端返回。此规范也允许 HttpOnly cookies 存在。HttpOnly cookies 的作用是告诉客户端它们不应该暴露客户端脚本代码（只有当客户端知道去获取该属性时才有这个过滤）。使用 HttpOnly 可以防止某些跨站脚本攻击。

## 3.10 SSL 属性

当请求通过某种安全协议传输，比如 HTTPS ，此信息就必须通过 ServletRequest 接口的 isSecure 方法暴露出来。容器必须将下列属性暴露给 servlet 开发者：

| Attribute                 | Attribute Name                       | Java Type |
| ------------------------- | ------------------------------------ | --------- |
| cipher suite              | javax.servlet.request.cipher_suite   | String    |
| bit size of the algorithm | javax.servlet.request.key_size       | Integer   |
| SSL session id            | javax.servlet.request.ssl_session_id | String    |

如果请求中存在某种 SSL 凭证，它就必须被容器以````java.security.cert.X509Certificate````对象数组的形式暴露给 servlet 开发者，通过````ServletRequest````接口的````javax.servlet.request.X509Certificate````属性访问。该数组元素以预定义的信任顺序升序排列。数据链中第一个凭证由客户端设置，下一个元素就是用来对前面一个元素进行认证的，依此类推。

 ## 3.11 国际化

客户端可以有选择地通知 Web 服务器它希望接收的响应的语言。该信息可以通过````Accept-Language````头部的形式传递，或者 HTTP/1.1 规范描述的其他机制。````ServeltRequest````接口中的下列方法用于访问请求发送方的区域设置：

* getLocale
* getLocales

````getLocale````方法将返回客户端希望获得响应的区域设置。参考 RFC 7231(HTTP/1.1) 的14.4章节获取更多有关如何设置````Accept-Language````头部以表达客户端希望的区域设置的知识。

````getLocales````方法返回````Locale````对象的枚举，表示客户端可以接受的所有地区设置，按照客户端的接受程度降序排列。

如果客户端没有显式声明区域设置，那么````getLocale````方法必须返回 servlet 容器的默认区域设置，````getLocales````方法必须返回只包含容器默认区域设置一个元素的枚举结果。

## 3.12 请求数据编码

目前，许多浏览器并不会通过 Contect-Type 请求头发送字符编码限定词，导致无法确定读取 HTTP 请求时采用何种字符编码。当没有字符编码限定词，而````Content-Type````是````application/x-www-form-urlencoded````时，容器用于创建请求数据读取器和 POST 数据转换器的字符编码必须是````US-ASCII````。任何````%nn````编码值必须被解码为 ISO-8859-1 。对其他的````Content-Type````，如果客户端请求、web 应用以及容器提供的配置（对容器内所有应用生效）都没有指定，那么容器用于创建请求数据读取器和 POST 数据转换器的字符编码必须是 ISO-8859-1 。不过，为了告知开发者字符编码限定词没有指定这种情况，此时````getCharacterEncoded()````方法必须返回````null````。

如果客户端没有设置字符编码而请求数据又不是以上述默认情况进行了编码，服务端读取请求数据就会出错。为了处理这种情况，````ServletContext```` 中添加了````setRequestCharacterEncoding(String enc)````方法。````web.xml````中添加了````\<request-character-encoding\>````元素。````ServletRequest````接口中也添加了````setCharacterEncoding(String enc)````方法。开发者可以覆盖容器调用此方法设置的字符编码。此方法必须在读取请求输入数据或者转换 post 数据之前调用，一旦数据已经读取就无法再修改字符编码。

## 3.13 请求对象的生存时间

每个请求对象都只存活在 servlet 的````service````方法的作用域内，或者在过滤器的````doFilter````方法的作用域内。除非容器支持异步处理而且该请求对象上的````startAsync````方法被调用。异步处理过程中，请求对象可以存活到````AsyncContext````上的````complete````方法被调用。容器为了降低创建对象的额外资源消耗而复用请求对象。开发者在上述作用域之外维护其上的````startAsync````方法并没有被调用的请求对象的引用时要特别小心，这会导致不确定的结果。

协议升级的情况下，上述规则依旧成立。

----

# Servlet Context

----

## 4.1 介绍

````ServletContext````接口定义了 servlet 运行于其中的 Web 应用的 servlet 视角的视图。容器提供方必须在容器中提供````ServletContext````接口的实现。通过````ServletContext````接口实现类对象，servlet 可以记录事件、获取指向资源的 URL 、设置并保存当前上下文中能够访问的其他 servlets 的属性。

````ServletContext````位于 Web 服务器的周知路径下。例如，servlet 上下文可以位于````http://example.com/catalog````下，所有以````/catalog````开头的请求路径，由于包含了上下文路径，因而都会被路由到该````ServletContext````对应的 Web 应用上。

## 4.2 Servlet 接口的作用域

每个部署到容器内的 Web 应用都有一个````ServletContext````接口对象与之关联。当容器分布在多台虚拟机器上时，Web 应用将在每个 JVM 中都有一个与之关联的````ServletContext````接口对象。

容器中那些没有作为 Web 应用的组成部分部署的 servlets 都隐含地成为所谓的 “默认” 应用的组成部分，同时拥有相应的默认````ServletContext````接口对象。在分布式容器中，这个默认````ServletContext````接口对象只能存在于一个 JVM 中而不能是分布式的。

## 4.3 初始化参数

````ServletContext````接口的下列方法允许 servlet 访问应用开发者在部署描述器中为应用指定的上下文初始化参数。

* getInitParameter
* getInitParameterNames

初始化参数通常被应用开发者用来传递配置信息。典型的例子是管理员的邮箱或者控制关键数据的系统的名称。

## 4.4 配置方法

从 Servlet 3.0 开始，下列方法就被添加到 ````ServletContext````接口中，用于以编程方式定义 servlets 、过滤器以及它们映射到的 url 匹配模式。这些方法只能在应用初始化过程中被调用，调用者要么是````ServletContextListener````实现对象的````contextInitialized````方法，要么是````ServletContainerInitializer````实现对象的````onStartup````方法。除了添加 servlets 和过滤器，我们还可以搜寻发现对应于 servlet 或者过滤器的````Registration````对象实例，或者有关 servlet 或者过滤器的所有````Registration````对象实例的 map。如果````ServletContext````实例对象被传入````ServletContextListener````的````contextInitialized````方法，而````ServletContextListener````既没有在````web.xml````或者````web-fragment.xml````中声明，也没有注解为````@WebListener````，此时为编程方式配置 servlets 、过滤器和监听器添加的方法都必须抛出````UnsupportedOperationException````。

### 4.4.1 编程方式添加和配置 Servlets

通过编程方式向上下文中添加 servlet 的能力对框架开发者非常有用。比如框架可以使用此方法声明一个控制器 servlet 。此方法的返回值是一个````ServletRegistration````实例对象或者````ServletRegistration.Dynamic````实例对象。接下来你可以为这个对象设置诸如````init-params````或````url-mapping````之类的属性。下面是此方法的三个重载版本：

#### 4.4.1.1 ````addServlet(String servletName, String className)````

此方法允许应用以编程方式基于给定的名称和类型名称声明一个 servlet ，并将其添加到上下文中。

#### 4.4.1.2 ````addServlet(String servletName, Servlet servlet)````

此方法允许应用以编程方式基于给定的名称和 servlet 对象实例声明 servlet ，并将其添加到上下文中。

#### 4.4.1.3 ````addServlet(String servletName, Class<? extends Servlet> servletClass)````

此方法允许应用以编程方式基于给定的名称和 servlet 类型对象实例声明 servlet ，并将其添加到上下文中。

#### 4.4.1.4 ````addJspFile(String servletName, String jspfile)````

此方法允许应用以编程方式基于给定的名称和对应于给定 jsp 文件的 servlet 类型对象实例声明 servlet ，并将其添加到上下文中。

#### 4.4.1.5 ````<T extends Servlet> T createServlet(Class<T> clazz)````

此方法实例化给定的````Servlet````类。此方法必须支持所有可用于````Servlet````的注解，除了````@WebServlet````。返回的````Servlet````实例在通过调用上面提到的````addServlet(String, Servlet)````方法被注册到````ServletContext````之前可以被进一步定制化。

#### 4.4.1.6 ````ServletRegistration getServletRegistration(String servletName)````

此方法返回对应于给定名称的 servlet 的````ServletRegistration````，如果不存在，则返回````null````。如果````ServletContext````实例对象被传入````ServletContextListener````的````contextInitialized````方法，而````ServletContextListener````既没有在````web.xml````或者````web-fragment.xml````中声明，也没有注解为````@WebListener````，此方法都必须抛出````UnsupportedOperationException````。

#### 4.4.1.7 ````Map<String, ? extends ServletRegistration> getServletRegistrations()````

此方法返回````ServletRegistration````对象的 map ，其中的 key 是注册到````ServletContext````中的所有````servlets````的名字。如果没有````servlet````注册到````ServletContext````中则返回空 map 。返回的 map 包含对应于所有声明的和注解的````servlets````，还包含所有通过````addServlet````或者````addJspFile````方法添加的````servlets````对应的````ServletRegistration````。对这个返回的 map 的任何改变都绝对不能影响````ServletContext````。如果````ServletContext````实例对象被传入````ServletContextListener````的````contextInitialized````方法，而````ServletContextListener````既没有在````web.xml````或者````web-fragment.xml````中声明，也没有注解为````@WebListener````，此方法都必须抛出````UnsupportedOperationException````。

### 4.4.2 编程方式添加和配置过滤器

#### 4.4.2.1 ````addFilter(String filterName, String className)````

此方法允许应用以编程方式声明一个过滤器，并将该过滤器以给定的名称和类名添加到应用中。

#### 4.4.2.2 ````addFilter(String filterName, Filter filter)````

此方法允许应用以编程方式声明一个过滤器，并将该过滤器以给定的名称和过滤器实例添加到应用中。

#### 4.4.2.3 ````addFilter(String filterName, Class<? extends Filter> filterClass)````

此方法允许应用以编程方式声明一个过滤器，并将该过滤器以给定的名称和过滤器类型实例添加到应用中。

#### 4.4.2.4 ````<T extends Filter> T createFilter(Class<T> clazz)````

此方法实例化给定的````Filter````类。此方法必须支持所有可用于````Filters````的注解。返回的````Filter````实例在通过调用上面提到的````addFilter(String, Filter)````方法被注册到````ServletContext````之前可以被进一步定制化。给定的````Filter````类必须定义一个无参构造器用于实例化。

#### 4.4.2.5 ````FilterRegistration getFilterRegistration(String filterName)````

此方法返回对应于给定名称的过滤器的````ServletRegistration````，如果不存在，则返回````null````。如果````ServletContext````实例对象被传入````ServletContextListener````的````contextInitialized````方法，而````ServletContextListener````既没有在````web.xml````或者````web-fragment.xml````中声明，也没有注解为````@WebListener````，此方法都必须抛出````UnsupportedOperationException````。

#### 4.4.2.6 ````Map<String, ? extends FilterRegistration> getFilterRegistrations()````

此方法返回````FilterRegistration````对象的 map ，其中的 key 是注册到````ServletContext````中的所有````filters````的名字。如果没有````servlet````注册到````ServletContext````中则返回空 map 。返回的 map 包含对应于所有声明的和注解的````filters````，还包含所有通过````addFilter````方法添加的````filters````对应的````FilterRegistration````。对这个返回的 map 的任何改变都绝对不能影响````ServletContext````。如果````ServletContext````实例对象被传入````ServletContextListener````的````contextInitialized````方法，而````ServletContextListener````既没有在````web.xml````或者````web-fragment.xml````中声明，也没有注解为````@WebListener````，此方法都必须抛出````UnsupportedOperationException````。

### 4.4.3 编程方式添加和配置监听器

#### 4.4.3.1 ````void addListener(String className)````

以给定的类名添加监听器到````ServletContext````。给定的类型将由该````ServletContext````表示的应用的类加载器加载，而且必须实现以下接口之一：

* ````javax.servlet.ServletContextAttributteListener````
* ````javax.servlet.ServletRequestListener````
* ````javax.servlet.ServletRequestAttributeListener````
* ````javax.servlet.http.HttpSessionListener````
* ````javax.servlet.http.HttpSessionAttributeListener````
* ````javax.servlet.http.HttpSessionIdListener````

如果````ServletContext````被传入````ServletContainerInitializer````的````onStartup````方法，则给定的类可以实现上述接口的同时实现````javax.servlet.ServletContextListener````接口。作为此方法调用的一部分，容器必须加载给定类名的类型以确保所需的接口被实现。如果给定名称的类型实现了一个监听器接口，而该接口的调用顺序对应于它们的声明顺序，也就是说，如果它实现了````javax.servlet.ServletRequestListener````、````javax.servlet.ServletContextListener````或者````javax.servlet.http.HttpSessionListener````，则这个新的监听器将被添加到实现此接口的监听器有序列表的末尾。

#### 4.4.3.2 ````<T extends EventListener> void addListener(T t)````

将给定的监听器添加到````ServletContext````中。给定的监听器必须实现以下接口之一：

* ````javax.servlet.ServletContextAttributteListener````
* ````javax.servlet.ServletRequestListener````
* ````javax.servlet.ServletRequestAttributeListener````
* ````javax.servlet.http.HttpSessionListener````
* ````javax.servlet.http.HttpSessionAttributeListener````
* ````javax.servlet.http.HttpSessionIdListener````

如果````ServletContext````被传入````ServletContainerInitializer````的````onStartup````方法，则给定的类可以实现上述接口的同时实现````javax.servlet.ServletContextListener````接口。作为此方法调用的一部分，容器必须加载给定类名的类型以确保所需的接口被实现。如果给定名称的类型实现了一个监听器接口，而该接口的调用顺序对应于它们的声明顺序，也就是说，如果它实现了````javax.servlet.ServletRequestListener````、````javax.servlet.ServletContextListener````或者````javax.servlet.http.HttpSessionListener````，则这个新的监听器将被添加到实现此接口的监听器有序列表的末尾。

#### 4.4.3.3 ````void addListener(Class <? extends EventListener> listenerClass)````

将规定类型的监听器添加到````ServletContext````。给定的监听器必须实现以下接口之一：

- ````javax.servlet.ServletContextAttributteListener````
- ````javax.servlet.ServletRequestListener````
- ````javax.servlet.ServletRequestAttributeListener````
- ````javax.servlet.http.HttpSessionListener````
- ````javax.servlet.http.HttpSessionAttributeListener````
- ````javax.servlet.http.HttpSessionIdListener````

如果````ServletContext````被传入````ServletContainerInitializer````的````onStartup````方法，则给定的类可以实现上述接口的同时实现````javax.servlet.ServletContextListener````接口。作为此方法调用的一部分，容器必须加载给定类名的类型以确保所需的接口被实现。如果给定名称的类型实现了一个监听器接口，而该接口的调用顺序对应于它们的声明顺序，也就是说，如果它实现了````javax.servlet.ServletRequestListener````、````javax.servlet.ServletContextListener````或者````javax.servlet.http.HttpSessionListener````，则这个新的监听器将被添加到实现此接口的监听器有序列表的末尾。

#### 4.4.3.4 ````<T extends EventListener> void createListener(Class <T> clazz)````

实例化给定的````EventListener````类。给定的````EventListener````类必须实现以下接口之一：

- ````javax.servlet.ServletContextAttributteListener````
- ````javax.servlet.ServletRequestListener````
- ````javax.servlet.ServletRequestAttributeListener````
- ````javax.servlet.http.HttpSessionListener````
- ````javax.servlet.http.HttpSessionAttributeListener````
- ````javax.servlet.http.HttpSessionIdListener````

此方法必须支持所有可用于由本规范定义的监听器接口的注解。返回的````EventListener````实例在通过调用上面提到的````addListener(T t)````方法被注册到````ServletContext````之前可以被进一步定制化。给定的````EventListener````类必须定义一个无参构造器用于实例化。

#### 4.4.3.5 编程方式添加 Servlets、过滤器和监听器需要的注解

当使用编程方式添加或创建一个 servlet 时，除了````addServlet````方法使用的一个实例，以下注解必须被标注在所使用的类型上。注解定义的元数据必须被使用，除非它被调用````ServletRegistration.Dynamic````或者````ServletRegistration````中的 API 而被覆盖。

* @ServletSecurity
* @RunAs
* @DeclareRoles
* @MultipartConfig

以上注解对过滤器和监听器不是必需的。

编程方式添加或创建以上组件所需要的资源，除了方法本身使用的实例之外，仅仅当组件是所谓的 CDI 管理的 Bean 时才被支持。详情请参考15.5.16章节 “ 上下文和依赖注入的 Java EE 需求” 部分内容。

### 4.4.4 编程方式配置会话超时

````ServletContext````接口中的下列方法允许应用访问和配置默认的会话超时时间，该超时时间作用于该应用创建的所有会话。````setSessionTimeout````方法中指定超时时间的单位是分钟，如果超时时间是0或者更小，容器保证默认行为是会话永不超时。

* ````getSessionTimeout()````
* ````setSessionTimeout(int timeout)````

### 4.4.5 编程方式配置

````ServletContext````接口中的下列方法允许应用访问和配置请求和响应的字符编码。

* ````getRequestCharacterEncoding()````
* ````setRequestCharacterEncoding(String encoding)````
* ````getResponseCharacterEncoding()````
* ````setResponseCharacterEncoding(String encoding)````

如果部署描述器和容器配置（对容器中所有应用生效）中都没有指定请求字符编码，````getRequestCharacterEncoding()````方法返回````null````。如果部署描述器和容器配置（对容器中所有应用生效）中都没有指定响应字符编码，````getResponseCharacterEncoding()````方法返回````null````。

## 4.5 Context 属性

一个 servlet 可以通过名称将对象属性绑定到 context 。任何绑定到 context 的属性可以被同一个应用下的所有 servlet 公用。通过````ServletContext````接口中的下列方法可以访问这些属性：

* ````setAttribute````
* ````getAttribute````
* ````getAttributeNames````
* ````removeAttribute````

### 4.5.1 分布式容器中的 Context 属性

Context 属性处于创建它的 JVM 本地。这就使得````ServletContext````属性无法在分布式容器中的共享内存中存储。当运行在分布式环境中的 servlet 之间需要共享信息时，该信息就应该放进````session```` 中，存储到数据库中，或者设置到 Java EE Beans 组件中。

## 4.6 资源

````ServletContext````接口只提供了对作为 Web 应用一部分的静态文件层级结构的直接访问能力，这些静态文件包括 HTML、GIF 和 JPEG 文件。通过下列方法访问静态资源：

* ````getResource````
* ````getResourceAsStream````

这两个方法使用以“/”开头的字符串作为参数，该字符串给出了资源相对于 context 根目录的位置，或者相对于web 应用的````WEB-INF/lib````目录下的 JAR 文件内````META-INF/resources````目录的位置。如果在````WEB-INF/lib````目录下的 JAR 文件内````META-INF/resources````实体中存在一个````WEB-INF````实体，则它自己和所有的子实体都只能作为静态资源。该````WEB-INF````实体中的任何类或者 jar 都不会被放在 context 的 classpath 下，任何 Servlets 配置描述符也不会被处理。这些方法会首先在应用上下文的根目录下搜索请求资源，然后才在````WEB-INF/lib````目录下的 jar 包内搜索。而扫描这些 jar 包的顺序是为定义的。这些文件的层级结构可以存在于服务器的文件系统中，或者在 Web 应用的归档文件里，或者在远程服务器上，或者在其它什么位置。

这些方法不能用于获取动态资源。比如，在一个支持 JavaServerPages 规范的容器里，形如````getResource("/index.jsp")````的方法调用将返回该 JSP 文件的源代码，而不是处理之后的输出结果。获取动态内容的方法参见第9章 “分发请求” 。

Web 应用的所有资源完整列表可以通过````getResourcePaths(String path)````获取。有关此方法的完整细节描述参见本规范的 API 文档。

## 4.7 多个 Hosts 和 Servlet Contexts

物理服务器上的Web 服务器可以支持多个逻辑主机共享一个 IP 地址。这种能力有时候被称为 “虚拟主机”。这中情况下，每个逻辑主机必须有它自己的 servlet context 或者 servlet context 集合。servlet context 不能在虚拟主机之间共享。

````ServletContext````接口的````getVirtualServerName````方法用于访问该````ServletContext````部署于其中的逻辑主机的配置名称。容器可以支持多个逻辑主机，但是对于部署在同一个逻辑主机中的所有 servlet context 该方法必须返回同一个名字。每个虚拟主机上，该方法的返回值必须是独特而稳定的，同时应该是适合应用于逻辑主机所在的物理服务器的配置信息中。

## 4.8 重新载入

尽管容器提供类的重新载入机制的实现可以方便开发人员，但是该特性并不是本规范要求的。任何此类机制的实现都必须保证所有的 servlets 以及所有它们使用的类都是在同一个类加载器的作用域内被载入。这个要求保证了应用的行为如开发者所想。作为开发辅助工具，容器应该提供 session 绑定监听器所需通知的完整语义，用于重新载入类时会话终止的监控。

之前版本的容器创建新的类加载器来加载 servlet，不同于在 servlet context 中用于加载其它 servlets 和类的类加载器。这样可能会导致 servlet context 中的对象引用指向不期望的类对象，从而导致期望之外的行为。本规范中的唯一类加载器的要求就是要避免这种问题。

### 4.8.1 临时工作目录

每个 servlet context 都需要临时工作目录。Servlet 容器必须为每个 servlet context 提供私有的临时工作目录，同时通过 context 的````javax.servlet.context.tempdir````属性暴露它的位置。该属性对应的对象类型必须是````java.io.File````。

这条需求是很多 servlet 引擎通用的便利基础设施。当容器重启时并不需要维护临时工作目录的内容。但是，容器需要保证临时工作目录的内容对容器内的其它应用的 servlet contexts 是不可见的。

----

# 响应

----

响应对象封装了从服务端返回客户端的所有信息。在 HTTP 协议中，这些信息通过请求的 HTTP 头部或者消息体由服务端传输到客户端。

## 5.1 缓冲

本规范允许，但是并不强制要求，为了性能对即将发送给客户端的输出数据进行缓冲。典型的情形是服务器默认会提供该特性，同时允许 serlvet 指定各自的缓冲参数。

````ServletResponse````接口的以下方法允许 servlet 访问并设置缓冲信息：

* ````getBufferSize````
* ````setBufferSize````
* ````isCommitted````
* ````reset````
* ````resetBuffer````
* ````flushBuffer````

这些方法在````ServletResponse````接口中提供，目的是无论 servlet 使用````ServletOutputStream````还是````Writer````缓冲都能工作。

````getBufferSize````方法返回正在使用的缓冲区的大小。如果当前并没有使用缓冲，该方法必须返回````int````值 0 。

servlet 可以使用````setBufferSize````方法请求一个想要的缓冲大小。分配的缓冲区大小不一定要刚好等于 servlet 请求的，但是不能小于请求的大小。这就允许容器重复使用一个固定大小的缓冲区集合，在适当的时候提供更大的缓冲区给 servlet。该方法必须在任何内容通过````ServletOutputStream````或者````Writer````被写入之前被调用。如果已经有内容写入或者响应已经被提交，该方法必须抛出````IllegalStateException````。

````isCommitted````方法返回一个逻辑值，表示是否有任何响应数据已经返回客户端。````flushBuffer````方法会强制奖缓冲区内容写入给客户端。

````reset````方法在响应尚未提交时清空缓冲区数据。在调用该方法之前的头部数据、状态码以及 servlet 设置的````getWriter````或者````getOutputStream````方法调用的状态等也都必须清空。````resetBuffer````方法当响应未提交时晴空缓冲区内容，但是并不清空头部数据和状态码。

如果响应已被提交，调用````reset````或者````resetBuffer````方法将会抛出````IllegalStateException````。响应以及有关缓冲将保持不变。

当使用缓冲时，容器必须清空已经被装满的客户端缓冲区。如果这是首次发往客户端的数据，则响应被认为已经提交。

## 5.2 头部

servlet 可以通过````HttpServletResponse````接口的下列方法设置 HTTP 响应的头部：

* ````setHeader````
* ````addHeader````

````setHeader````方法将给定的字段名和字段值设置到响应头部中，之前的头部同名字段将会被覆盖。如果原先该字段值是一个集合，则该集合会被清除而被新的值覆盖。

````addHeader````方法将给定的字段名和字段值添加到响应头部中。如果之前没有同名的头部字段，则会创建。

头部可以包含表示````int````或者````Date````类型对象的数据。servlet 可以通过````HttpServletResponse````接口的下列方法将适当数据类型的数据对象设置到响应头部字段中：

* ````setIntHeader````
* ````setDateHeader````
* ````addIntHeader````
* ````addDateHeader````

为了成功地从服务端传输到客户端，响应头部（除了头部 trailer 字段）数据必须在响应被提交之前设置。响应被提交之后设置头部（除了 trailer 字段）将会被容器忽略。如果 RFC 7230 中定义的 HTTP trailer 字段被放进响应中，它们就必须通过````HttpServletResponse````接口的````setTrailerFields()````方法设置。该方法必须在分块编码响应数据的最后一个数据分块被写入之前调用。

servlet 开发者必须保证 servlet 产生的响应对象的````Content-Type````头部字段设置了适当的值。HTTP 1.1 规范并没有要求响应中该头部字段一定被赋值。当 servlet 开发者未设置时容器必须保证不对该字段赋默认值。

本规范推荐容器使用````X-Powered-By```` HTTP 头部来发布其实现信息。该字段的值应该由一个或多个实现类型，比如 “Servlet/4.0”。容器还可以有选择地将容器的支持信息和基于的 Java 平台信息添加到实现类型之后。容器应该设置为禁用此头部字段。

该头部字段的例子：

````X-Powered-By: Servlet / 4.0````

````X-Powered-By: Servlet / 4.0  JSP/2.3 (GlassFish Server Open Source Edition 5.0 Java/Oracle Corporation/1.8)````

## 5.3 HTTP Trailer

RFC 7230 中定义，Http Trailer 是一个特定类型的 HTTP 头部字段的集合，它在响应体之后发送。它们在分块转化编码的场景中非常有用，同时也用在附加通信协议的实现中。servlet 容器提供支持。

如果该头部数据已经可以读取，````isTrailerFieldsReady()````方法将返回````true````。然后 servlet 就可以通过````HttpServletRequest````接口的````getTrailerFields()````方法读取 HTTP 请求的 trailer 头部数据。

servlet 可以通过将````Supplier````传入````HttpServletResponse````接口的````setTrailerFields````方法来写入响应的 trailer 头部。放在响应 trailer 头部中的````Supplier````可以通过````HttpServletResponse````接口的````getTrailerFields()````方法访问。

## 5.4 非阻塞 IO

非阻塞 IO 只能跟 servlet 或者过滤器中的异步请求处理过程配合工作，或者用在协议升级过程中。否则，````ServletInputStream.setReadListener````和````ServletInputStream.setWriteListener````方法必须抛出````IllegalStateException```` 。为了支持非阻塞写，````ServletRequest````中进行的修改都在3.7章节中进行了介绍。接下来的是对响应相关的类和接口的修改。

````WriteListener````提供了如下回调方法供容器调用。

* ````WriteListener````
  * ````void onWritePossible()```` 当一个````WriteListener````被注册到````ServletOutputStream````时，如果数据可以写则此方法将首次被容器调用。容器接下来将继续调用````ServletOutputStream````的````onWritePossible````方法，当且仅当````ServletOutputStream````上的````isReady````方法返回````false````然后写操作接下来成为可能。
  * ````onError```` 当响应处理过程中发生错误时被调用。

以下方法被添加到````ServletOutputStream````类中，开发者可以通过它们在运行时检查数据是否可以向客户端写入。

* ````ServletOutputStream````
  * ````boolean isReady()```` 当向````ServletOutputStream````写入操作可行时返回````true````，否者返回````false````。如果此方法返回````true````，则数据写入操作就能成功。如果没有更多数据可以被写入````ServletOutputStream````，则此方法将一直返回````false````直到潜在的数据全部被写入。此时容器将调用````WriteListener````的````onWritePossible````方法。然后此方法的后续调用都将返回````true````。
  * ````void setWriteListener(WriteListener listener)```` 将给定的````WriteListener````关联到当前````ServletOutputStream```` 。当数据可写入时容器将调用````WriteListener````上的这个回调方法。注册````WriteListener````将开始非阻塞 IO 。此时切换回传统的阻塞式 IO 是非法的。这种非法切换之后的任何 IO 相关方法都将产生不可预测的行为。

容器必须以线程安全的方式调用````WriteListener````中的方法。

## 5.5 便捷方法

````HttpServletResponse````接口提供了以下便捷方法：

* ````sendRedirect````
* ````sendError````

````sendRedirect````方法将设置适当的头部和请求体内容并把请求重定向到另外的 URL 。将相对路径作为参数是合法的，不过此时容器就必须先将相对路径转化成绝对路径再传递给客户端。如果由于任何原因导致参数只是一个 URL 片段而且无法转化成合法的 URL，则此方法必须抛出````IllegalArgumentException````。

````sendError````方法将为发送给客户端的错误信息相应设置适当的头部和主体数据。该方法的可选的字符串类型的参数可用于在错误相应主体数据中描述错误信息。

这些方法对响应的提交有副作用，如果响应尚未被提交，则终止之。这些方法调用之后，servlet 就不应再向客户端发送任何其他数据。这些方法调用之后写入响应的数据都会被忽略。

如果数据已经被写入响应数据缓冲区，但是尚未返回客户端，比如响应尚未提交的情形，则这些数据都必须被这些方法设置的数据替换掉。如果响应已经提交，则这些方法必须抛出````IllegalStateException````。

## 5.6 国际化

Servlets 应该设置区域和响应的字符编码。区域通过````ServletResponse.setLocale````方法设置，该方法可以重复调用，但是在响应提交之后调用是无效的。如果响应提交之前 servlet 并未设置区域信息，则容器的默认区域将生效。但是如何与客户端通信则没有规范定义，比如对 HTTP 来说通过````Content-Language````头部字段：

````xml
<locale-encoding-mapping-list>
	<locale-encoding-mapping>
		<locale>ja</locale>
		<encoding>Shift_JIS</encoding>
	</locale-encoding-mapping>
</locale-encoding-mapping-list>
````

````<response-character-encoding>````元素可以用于显式指定给定应用所有响应的默认字符编码：

````xml
<response-character-encoding>UTF-8</response-character-encoding>
````

如果既没有上述元素，也没有提供映射关系，````setLocale````方法使用依赖容器的映射关系。````setCharacterEncoding````、````setContentType````、以及````setLocale````方法可以重复调用以改变字符编码。在响应的````getWriter````方法被调用或者响应已经被提交之后，这些方法将无法再修改字符编码。只有当给定的内容类型字符串提供了````charset````属性的值时才能调用````setContentType````方法设定字符编码。只有当````setCharacterEncoding````和````setContentType````方法都没有设定字符编码时才能调用````setLocale````方法设置字符编码。

如果````ServletResponse````接口的````getWriter````方法被调用或者响应已经被提交之后 servlet 并未设置字符编码，默认使用````ISO-8859-1````。

如果使用的协议提供了相应的机制，容器必须与客户端交流用于响应写入器的区域设置和字符编码设置信息。HTTP 的情形，区域信息通过````Content-Language````头部字段传输，字符编码作为字符媒体类型描述符的````Content-Type````头部的一部分。需要注意的是，如果 servlet 并未指定内容类型，则字符编码就不能通过 HTTP 头部传输，不过，它仍然会被用于响应内容的编码。

## 5.7 响应对象关闭

当响应被关闭，容器必须马上清理所有剩余的客户端缓冲区数据。以下事件表示 servlet 已经正确处理请求，而且响应对象即将关闭：

* servlet 接口的````service````方法的终止。
* ````setContentLength````或者````setContentLengthLong````方法设置的内容数据的数量大于零，而且数据已经被写入响应。
* ````sendError````方法被调用。
* ````sendRedirect````方法被调用。
* ````AsyncContext````的````complete````方法被调用。

## 5.8 响应对象的生存时间

每个响应对象都只是在 servlet 的````service````方法作用域内可用，或者在过滤器的````doFilter````方法的作用域内。除非容器支持异步处理而且该请求对象上的````startAsync````方法被调用。异步处理过程中，响应对象可以存活到````AsyncContext````上的````complete````方法被调用。容器为了降低创建对象的额外资源消耗而复用响应对象。开发者在维护其对应的请求对象上的````startAsync````方法并没有被调用的响应对象的引用时要特别小心，这会导致不确定的结果。

----

# 过滤

----

过滤器是这样一种 Java 组件，它可以对指向资源的请求和来自资源的响应的载荷数据和头部数据进行转化。

Java Servlet API 中的类和方法提供了一套过滤动态和静态资源的轻量级框架。它描述了如何在 Web 应用中配置过滤器，以及实现相关的约定和语义。

servlet 过滤器 API 文档已经在线上公布。过滤器配置语法通过部署描述器概要描述，在本规范第14章 “部署描述器” 中详细介绍。读者请自行参考。

## 6.1 过滤器是什么

过滤器是一个可以复用的程序片段，可以转化 HTTP 请求和响应的内容数据和头部信息。过滤器并不像 servlet 那样创建响应或者对请求作出反应。它们做的是修改或者适配请求到资源，或者修改或者适配资源到响应。

过滤器可以处理静态或者动态内容。在本章节内，动态和静态资源都是指的 Web 资源。

开发者需要用到的过滤器功能有这几类：

* 在请求之前对资源进行访问
* 在资源被访问之前对指向该资源的请求进行处理
* 通过将请求包装进定制化的请求对象实现对请求头和请求体的修改
* 通过将响应包装进定制化的响应对象实现对响应头和响应体的修改
* 拦截对某个资源的请求
* 任意数量的过滤器以特定顺序作用于任意数量的 servlet 或者 servlet 组，或者静态资源

### 6.1.1 过滤组件举例

* 认证过滤器
* 日志和审计过滤器
* 图片转换过滤器
* 数据压缩过滤器
* 加密过滤器
* 令牌过滤器
* 资源访问事件触发过滤器
* XML 转换过滤器
* MIME-type 链过滤器
* 缓存过滤器

## 6.2 主要概念

本节介绍过滤器模型的核心概念。

应用开发者通过实现````javax.servlet.Filter````接口创建过滤器并提供无参构造器。这个类和组成 Web 应用的静态资源以及 servlets 一起打包成 war 包。过滤器通过部署描述器中的````<filter>````元素声明。单个过滤器或者过滤器集合可以通过在部署描述器中定义````<filter-mapping>````元素与请求建立映射关系。实际上就是根据 servlet 的逻辑名称将过滤器映射到其上，或者通过将过滤器映射到一个 URL 模式将过滤器映射到一组 servlet 和静态资源。

### 6.2.1 过滤器生命周期

 在 Web 应用部署之后、而请求到来而导致容器访问 Web 资源之前，容器必须如下文所述定位必须应用到该资源上的过滤器列表。容器必须保证已经实例化好了过滤器列表中的每个过滤器类，而且已经调用过其````init(FilterConfig config)```` 方法。过滤器无法正常工作时可以抛出异常。如果过滤器抛出了````UnavailableException````，容器可以检查异常的````isPermanent````属性并可以选择一段时间之后再次尝试使用该过滤器。

部署描述器中的每个````<filter>````声明在每个容器的 JVM 中只会实例化出唯一一个实例。基于部署描述器中的过滤器声明，容器提供过滤器````config````，涉及到应用的````ServletContext````以及初始化参数集合。

当容器接收到进入的请求，它将使用过滤器列表上的第一个过滤器实例，调用它的````doFilter````方法，传入````ServletRequest````和````ServletResponse````，同时还有一个````FilterChain````对象的引用。

过滤器的````doFilter````方法的典型实现遵循以下模式或其子集：

1. 该方法检查请求头部。
2. 该方法可以使用定制化的````ServletRequest````或者````HttpServletRequest````实现包装请求对象来修改请求头或者请求体。
3. 该方法可以使用定制化的````ServletResponse````或者````HttpServletResponse````实现包装响应对象来修改响应头或者响应体。
4. 过滤器可以调用过滤器链上的下一个实体。下一个实体可以是另一个过滤器。如果发起请求的过滤器已经是部署描述器中配置的过滤器链上最后一个，则下一个实体就是目标 Web 资源。对下一个实体的请求受到````FilterChain````对象上的````doFilter````方法的调用的影响，同时传入原始的请求和响应或者被它包装之后的版本。过滤器链的````doFilter````方法实现由容器提供，必须定位过滤器链上的下一个实体，然后调用该实体的````doFilter````方法，传入相应的请求和响应对象。或者，过滤器链不调用下一个实体从而能够阻塞请求，此时当前过滤器就有责任填满响应对象数据。servlet 的````service````方法必须与应用到该 servlet 的所有过滤器运行在同一个线程内。
5. 调用过滤器链上的下一个实体后，过滤器可以检查响应头。
6. 或者，过滤器可以抛出异常来表示处理过程中发生了错误。如果过滤器在````doFilter````过程中抛出了````UnavailableException````，容器就不能继续试图继续执行过滤器链。如果异常没有标记为永久，则容器可以选择稍后尝试重新执行整个过滤器链。
7. 当过滤器链上的最后一个过滤器已经被调用，下一个访问的实体就是处于链尾的目标 servlet 或者资源。
8. 在过滤器实例可以被容器从服务中移除之前，容器必须首先调用该过滤器的````destroy````方法以确保该过滤器释放所有资源，同时执行其它的清理操作。

### 6.2.2 包装请求和响应

过滤这个概念的核心就是包装，通过包装请求和响应，过滤器就可以改变它们的行为从而完成所谓的过滤任务。在这种模型中，开发者不仅仅拥有覆盖请求和响应对象现存方法的能力，还能够为过滤器链上的下一个过滤器或者资源提供适合特定过滤任务的新的 API 。比如，开发者也许希望用更高层次的输出对象扩展响应对象，比如输出流或者写入器，譬如那些允许 DOM 对象可以被写回客户端的 API 。

为支持这种类型的过滤器，容器必须满足以下需求。当过滤器调用容器的过滤器链实现的````doFilter````方法时，容器必须确保它传递给过滤器链上的下一个实体，如果过滤器是链尾实体则是目标资源，的请求和响应对象，和上一个过滤器调用它的````doFilter````方法时传入的是同一个对象。

对于包装器对象的相同的需求同样适用于从 servlet 后者过滤器到````RequestDispatcher.forward````或者````RequestDispatcher.include````方法，只要调用着试图包装请求或者响应对象。这种情况下，被调用的 servlet 看到的请求和响应对象必须和调用它的 servlet 或者过滤器传入的是相同的包装器对象。

### 6.2.3 过滤器环境

初始化参数集合可以通过部署描述器中的````<init-params>````元素与一个过滤器建立关联。这些参数的名称和值在运行期对过滤器是可见的，可以通过过滤器的````FilterConfig````对象上的````getInitParameter````和````getInitParameterNames````方法访问。另外，通过````FilterConfig````对象可以访问应用的````ServletContext````，因而可以加载资源，可以记录日志，可以在````ServletContext````属性列表里存储状态。过滤器和处于过滤器链末端的 servlet 或者资源必须在同一个请求线程中执行。

### 6.2.4 Web 应用中的过滤器配置

过滤器可以通过本规范8.1.2章节中定义的````@WebFilter````注解声明，或者在部署描述器文件中用````<filter>````元素声明。在该部署描述器元素中，开发者可以声明以下属性：

* ````filter-name````：用于将过滤器映射到一个 servlet 或者 URL 
* ````filter-class````：容器用来确定过滤器类型
* ````init-params````过滤器初始化参数

开发者还可以有选择地位过滤器指定按钮、文字描述以及显示名称等属性用于其它工具操作。容器必须为部署描述器中每个过滤器声明实例化唯一一个该类型的实例。因此，如果部署描述器中声明了两个相同类型的过滤器，则容器将会实例化出两个相同类型的过滤器。

这里是声明过滤器的例子：

````xml
<filter>
  <filter-name>Image Filter</filter-name>
  <filter-class>com.example.ImageServlet</filter-class>
</filter>
````

一旦在部署描述器文件中声明了一个过滤器，装配器就会使用````<filter-mapping>````元素来定义该过滤器将要应用到其上的 servlets 和应用中的静态资源。过滤器可以通过````<servlet-name>````元素与 servlet 建立关联。下面这个例子中，Image Filter 过滤器映射到````ImageServlet````：

````xml
<filter-mapping>
  <filter-name>Image Filter</filter-name>
  <servlet-name>ImageServlet</servlet-name>
</filter-mapping>
````

过滤器可以通过````<url-pattern>````过滤器映射风格关联到 servlets 组和静态资源：

````xml
<filter-mapping>
  <filter-name>Logging Filter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
````

这个例子中 Logging Filter 被应用于 Web 应用中所有的 servlets 和静态资源页面，因为每个请求的 URI 都会匹配上````/*```` URL 模式。

当处理一个采用````<url-pattern>````风格的````<filter-mapping>````元素时，容器必须决定该````<url-pattern>````是否使用本规范第12章“映射请求到 Servlets ”中定义的路径映射规则匹配请求 URI 。

容器创建应用于特定请求 URI 的过滤器链时的顺序如下：

1. 首先，````<url-pattern>````按照这些元素在部署描述器中出现的顺序匹配过滤器映射。
2. 接下来，````<servlet-name>````按照这些元素在部署描述器中出现的顺序匹配过滤器映射。

如果一个过滤器映射元素同时包含````<servlet-name>````和````<url-pattern>````元素，容器必须扩展这个过滤器映射为多个过滤器映射（每个````<servlet-name>````或````<url-pattern>````元素对应一个过滤器映射），同时保留原有````<servlet-name>````和````<url-pattern>````元素的顺序。例如，下面这个过滤器映射：

````xml
<filter-mapping>
    <filter-name>Multiple Mappings Filter</filter-name>
    <url-pattern>/foo/*</url-pattern>
    <servlet-name>Servlet1</servlet-name>
    <servlet-name>Servlet2</servlet-name>
    <url-pattern>/bar/*</url-pattern>
</filter-mapping>
````

等同于：

````xml
<filter-mapping>
    <filter-name>Multiple Mappings Filter</filter-name>
    <url-pattern>/foo/*</url-pattern>
</filter-mapping>
<filter-mapping>
    <filter-name>Multiple Mappings Filter</filter-name>
    <servlet-name>Servlet1</servlet-name>
</filter-mapping>
<filter-mapping>
    <filter-name>Multiple Mappings Filter</filter-name>
    <servlet-name>Servlet2</servlet-name>
</filter-mapping>
<filter-mapping>
    <filter-name>Multiple Mappings Filter</filter-name>
    <url-pattern>/bar/*</url-pattern>
</filter-mapping>
````

关于过滤器链的顺序要求意味着，当请求到来时，容器必须按照下列顺序处理请求：

* 根据本规范随后将要介绍的“映射规范”定义的规则确定目标 Web 资源。
* 如果存在过滤器按照 servlet 名称匹配，同时目标资源对应于一个````<servlet-name>```` 元素，容器就按照匹配到的过滤器在部署描述器中声明的顺序构建过滤器链。过滤器链上的最后一个过滤器对应于最后一个````<servlet-name>````匹配方式的过滤器。而这个过滤器就会直接访问目标 Web 资源。
* 如果存在过滤器采用````<url-pattern>````匹配方式，而````<url-pattern>````根据本规范12.2章节将要介绍的“映射规范”定义的规则匹配到请求 URI ，容器就按照部署描述器中声明的顺序构建该````<url-pattern>````匹配方式的过滤器链。过滤器链最后一个过滤器就是匹配到请求 URI 的最后一个````<url-pattern>````匹配方式的过滤器。该过滤器奖调用````<servlet-name>````匹配方式的过滤器链上的第一个过滤器，如果后者不存在，则直接访问目标 Web 资源。

高性能 Web 容器有所不同，它们可以缓存过滤器链，因而不需要为每个请求都重新构建。

### 6.2.5 过滤器和请求分发器

从 Java Servlet 规范2.4版本以来的一个新特性就是能够将过滤器配置到请求分发器的````forward()````和````include()````方法调用下供调用。

通过在部署描述器中使用新的````<dispatcher>````元素，开发者可以告诉一个过滤器映射在如下情况下他是否希望过滤器应用于请求：

1. 请求直接来自客户端

   通过包含 REQUEST 值的````<dispatcher>````元素说明，或者根本没有````<dispatcher>````元素。

2. 请求正在被一个代表匹配到````<url-pattern>````或者````<servlet-name>````的 Web 组件的请求分发器使用一个````forward()````调用处理中。

   通过包含 FORWARD 值的````<dispatcher>````元素说明。

3. 请求正在被一个代表匹配到````<url-pattern>````或者````<servlet-name>````的 Web 组件的请求分发器使用一个````include()````调用处理中。

   通过包含 INCLUDE 值的````<dispatcher>````元素说明。

4. 请求正在被一个对应于匹配到````<url-pattern>````的错误资源的错误页面机制，在下文“错误处理”中介绍，处理中。

   通过包含 ERROR 值的````<dispatcher>````元素说明。

5. 请求正在被一个异步上下文分发机制，在上文“异步处理”中介绍，调用````dispatch()````方法处理中。

   通过包含 ASYNC 值的````<dispatcher>````元素说明。

6. 或者以上各种情况的任意组合。

例如：

````xml
<filter-mapping>
  <filter-name>Logging Filter</filter-name>
  <url-pattern>/products/*</url-pattern>
</filter-mapping>
````

该过滤器映射将导致 Logging Filter 被 URI 以````/products/...````开头的客户端请求调用，但是并不在配置了````/products/...````路径的请求分发器调用之下。该 Logging Filter 可以被初始的请求分发调用，也可以被重新开始的请求调用。

````xml
<filter-mapping>
  <filter-name>Logging Filter</filter-name>
  <servlet-name>ProductServlet</servlet-name>
  <dispatcher>INCLUDE</dispatcher>
</filter-mapping>
````

这个过滤器映射将导致 Logging Filter 不被请求````ProductServlet````的客户端请求调用，也不在请求分发器的````forward()````方法调用````ProductServlet````之下，但是将被配置了````ProductServlet````名称的请求分发器的````include()````方法调用之下调用.

````xml
<filter-mapping>
  <filter-name>Logging Filter</filter-name>
  <url-pattern>/products/*</url-pattern>
  <dispatcher>FORWARD</dispatcher>
  <dispatcher>REQUEST</dispatcher>
</filter-mapping>
````

该过滤器映射将导致 Logging Filter 被 URI 以````/products/...````开头的客户端请求调用，同时也在配置了````/products/...````路径的请求分发器````forward()````方法调用之下。

````xml
<filter-mapping>
  <filter-name>All Dispatch Filter</filter-name>
  <url-pattern>*</url-pattern>
  <dispatcher>FORWARD</dispatcher
</filter-mapping>
````

该过滤器映射将导致所有的分发过滤器被当通过名称或者路径获取到的请求分发器````forward()````方法调用下调用。

----

# 会话

----

超文本传输协议 HTTP 被设计为无状态的协议。为了创建有效的 Web 应用，将来自特定客户端的请求相互关联起来是非常必要的。随着时间推移，很多会话追踪策略被发展出来。然而开发者直接使用这些策略却往往很困难。

本规范定义了一个简单的````HttpSession````接口，它允许 servlet 容器使用任何用户会话追踪方法，但是并不会使得应用开发者被任何具体的方法绑架。

## 7.1 会话追踪机制

以下章节描述了用户会话追踪方法。

### 7.1.1 Cookies

通过 HTTP cookies 进行会话追踪是最常用的会话追踪机制，因而所有 servlet 容器都必须支持。

容器发送一个 cookie 给客户端。客户端将在后续的请求中附带该 cookie 送回服务器，从而将所有请求明确地关联到一个会话。用于会话追踪的 cookie 的标准名称必须是````JSESSIONID````。容器可以通过具体的配置允许使用定制化的会话追踪 cookie 名称。

所有 servlet 容器必须提供可配置容器是否将会话追踪 cookie 标记为````HttpOnly````。约定俗成的配置必须应用到所有特定配置的上下文之上。如果应用配置了客户化的会话追踪 cookie 名称，如果会话 id 被编码进 URL 中，该名称也将作为 URI 参数的名称。

### 7.1.2 SSL 会话

安全套接层，用于 HTTPS 协议中的加密技术，内建了一套会话追踪机制，可以将来自客户端的多个请求明确标记为同一个会话的组成部分。servlet 容器可以利用该数据定义会话。

### 7.1.3 URL 重写

URL 重写是最普通的会话追踪技术。当客户端不支持 cookie 时，URL 重写就可以被服务器用于会话追踪。URL 重写添加会话 ID 到由容器解释的 URL 路径中将请求关联到一个会话。

该会话 ID 必须作为路径参数被编码进 URL 字符串。参数名称必须是````jsessionid````。下面是一个包含编码路径信息的 URL 的例子：

````html
http://www.example.com/catalog/index.html;jsessionid=1234
````

URL 重写将会话 ID 暴露在日志、浏览器书签、引用页头部、缓存的 HTML 页面以及 URL 地址栏中。在 cookies 或者 SSL 会话机制可用时就不应该采用 URL 重写作为会话追踪机制。

### 7.1.4 会话完整性

当处理来自不支持 cookies 的客户端的 HTTP 请求时，Web 容器必须支持 HTTP 会话。为了满足此要求，Web 容器通常都支持 URL 重写机制。

## 7.2 会话创建

会话只有当它还尚未建立时作为预期会话时才被认为是新会话。因为 HTTP 是一个基于请求响应的协议，直到客户端加入时会话才被认为新建起来。当表示会话已经建立的会话追踪信息已经返回服务端时，客户端就算加入一个会话。在客户端加入会话之前，它都不能假定下一个客户端请求将被服务端认为时会话的一部分。

当以下条件任一为真时会话被认为是新会话：

* 客户端还不知道该会话的存在
* 客户端选择不加入该会话

这些条件定义的场景下，servlet 容器没有任何机制可以将先后到来的两个请求关联起来。

Servlet 开发者设计应用时必须保证可以处理客户端尚未加入、不能加入或者选择不加入会话的情况。

每个会话，都存在一个包含唯一标识符的字符串与之对应，称之为 session id 。其值可以通过调用````javax.servlet.http.HttpSession.getId()````方法获取，会话创建之后其 id 可以通过````javax.servlet.http.HttpServletRequest.changeSessionId()````方法修改。

## 7.3 会话作用域

````HttpSession````对象的作用域必须局限在应用或者 servlet 上下文范围内。潜在的机制中，用于建立会话的 cookie 数据，在不同的上下文中取值可能是相同的，但是对象引用，包括所有对象属性，绝对不能在多个上下文之间共享。

举例说明：如果一个 servlet 使用````RequestDispatcher````调用其他 Web 应用中的 servlet ，为该被调用 servlet 创建并对其可见的任何会话都必须不同于为调用方 servlet 创建并对其可见的会话。

另外，上下文相关的会话当请求进入上下文时必须是可恢复的，无论这些会话创建时它们所关联的上下文是被直接访问还是作为请求分发器的目标而被访问。

## 7.4 绑定属性到会话

Servlet 可以按照名称将对象属性绑定到````HttpSession````实现。任何绑定到会话的对象对属于同一个````ServletContext````的任何其他 servlet 都是可见的，并且像处理请求 id 那样作为同一个会话的一部分。

某些对象当被放进会话或者被从会话中移除时需要发送通知。这些信息可以通过实现了````HttpSessionBindingListener````接口的对象实例获取。该接口定义了以下方法实现上述功能：

* valueBound
* valueUnbound

````valueBound````方法必须在通过````HttpSession````接口的````getAttribute````方法可访问到对象之前调用。而````valueUnbound````方法必须在通过````HttpSession````接口的````getAttribute````方法不再能够访问到对象之后调用。

## 7.5 会话超时

在 HTTP 协议中，当客户端不再活动时并没有什么明确的终止信号发送给服务端。这就意味着唯一可是表示客户端不再活动的机制就是超时时间了。

会话的默认超时时间由 servlet 容器定义，可以通过````ServletContext````接口的````getSessionTimeout````方法，或者````HttpSession````接口的````getMaxInactiveInterval````方法获取。开发者可以通过````ServletContext````接口的````setSessionTimeout````方法，或者````HttpSession````接口的````setMaxInactiveInterval````方法修改会话超时时间，前者时间单位是分钟，后者时间单位是秒。根据定义，如果超时时间被设置为0或者更小，则会话将永不过期。会话将会一直存活到所有使用它的请求都已经退出 servlet 的 service 方法。一旦会话失效，新的请求就绝对不能再看到它。

## 7.6 最后访问时间

````HttpSession````接口的````getLastAccessedTime````方法允许 servlet 确定在当前请求之前会话最近一次被访问的时间。会话被访问，意思是作为会话一部分的请求首次被 servlet 容器处理。

## 7.7 重要的会话语义

### 7.7.1 线程问题

多个 servlets 执行请求线程可以同时访问同一个会话对象。容器必须保证对表示会话属性的那日不数据结构的操作以线程安全的方式执行。开发者也要以线程安全的方式访问会话属性对象。这将在并发访问情况下保护````HttpSession````中的属性对象集合，避免这些属性集合被应用破坏。除非本规范明确说明，来自请求和响应的所有对象都必须假定为非线程安全的。包括但不限于，````ServletResponse.getWriter()````方法返回的````PrintWriter````对象，````ServletResponse.getOutputStream()````方法返回的````OutputSteam````对象。

### 7.7.2 分布式环境

在标记为分布式的应用中，所有作为一个会话组成部分的所有请求都必须被同一个 JVM 依次处理。容器必须能够恰当地使用````setAttribute````或者````putValue````方法处理所有放进````HttpSession````类对象中的对象。施加以下约束以满足这些要求：

* 容器必须接受实现了````Serializable````接口的对象。
* 容器可以选择支持将其它委托对象存储到````HttpSession````中，比如 JavaBeans 组件的引用和事务处理。
* 会话迁移将由容器特定基础设施处理。

当它缺少必要的支持机制以完成存储对象的会话的迁移时，分布式容器必须抛出````IllegalArgumentException````。

分布式容器必须支持必要的机制以完成实现了````Serializable````接口的对象的迁移。

这些约束意味着开发者可以认为在分布式容器中不会存在非分布式容器中额外的并发问题。

容器提供者能够保证扩展性和服务质量，基于可以移动会话对象的能力提供负载均衡和故障转移，从分布式系统的任意活动节点迁移到别的节点。

如果分布式容器持久化或者迁移会话以提供服务质量特性，它们并不受限于使用本地 JVM 序列化机制来序列化````HttpSession````和它们的属性。开发者并不被保证容器将在属性对象上调用它们实现的````readObject````和````writeObject````方法，但是被保证它们属性的````Serializable````闭包将被保留。

会话迁移过程中容器必须通知任何实现````HttpSessionActivationListener````接口的会话属性对象。它们必须通知监听器在会话序列化之前休眠，而在会话反序列化之后重新激活。

应用开发者编写分布式应用时应该注意，因为容器可以运行在不只一个 Java 虚拟机中，开发者不能依赖静态变量来存储应用状态。应用状态应该存储在企业级 Java Bean 组件或者数据库中。

### 7.7.3 客户端语义

cookies 或者 SSL 证书通常都由浏览器进程控制，但是与浏览器的特定窗口无关，基于该事实，来自一个客户端程序多个窗口的请求在 servlet 容器看来就可能是属于同一个会话的。最可能的情况，开发者应该始终假定客户端所有窗口都属于同一个会话。

----

# 注解和可插拔性

----

本章节介绍使用注解和其他保证框架的可插拔性的增强机制，以及在 Web 应用中使用的类库等。

## 8.1 注解和可插拔性

在  Web 应用中，使用注解的类只有当位于````WEB-INF/classes````路径下，或者它们被打包进 jar 文件中的````WEB-INF/lib````路径下时，它们包含的注解才会被处理。

Web 应用的部署描述器文件中````web-app```` 元素包含````metadata-complete````属性。该属性定义是否该部署描述器和任何 web 片段，如果存在，是完备的，或者是否该模块下可用的类文件和同应用一起打包的类文件应该进行注解检查，以确定他们是否包含部署信息。部署信息在这里指的是已经由部署描述器制定的、随后会被类上的注解覆盖的任何信息。

如果````metadata-complete````属性被指定为````true````，部署工具必须忽略任何打包到应用中的类中任何指定这些部署信息的注解。请参考8.2.3章节“从 web.xml、web-fragment.xml 和注解中装配部署描述器”，8.4章节“处理注解和片段”，15.5.1章节“处理 metadata-complete” 以获取更多有关````metadata-complete````处理的详细信息。

如果````metadata-complete````属性没有被指定，或者其值为````false````，则部署工具必须检查应用中包含该注解的类文件。需要注意的是，````metadata-complete````属性的````true````值并不会优先与所有注解，而只是优先于下面这些：

在部署 XSD 中没有对应词的注解，包含````javax.servlet.annotation.HandlesTypes````和所有 CDI 相关注解。这些注解必须在注解扫描过程中被处理，无论````metadata-complete````属性的取值。

当 EJBs 被打包进````.war````文件中，而该````.war````文件包含````ejb-jar.xml````文件，该````ejb-jar.xml````文件中的````metadata-complete````属性确定了那些企业级 Java Beans 的注解的处理。如果不存在````ejb-jar.xml````文件，而````web.xml````文件指定了````metadata-complete````属性的值为````true````，其等效于````ejb-jar.xml````文件中的````metadata-complete````属性为````true````。更多细节可以参考 Enterprise JavaBeans 规范。

下面是````javax.servlet.annotation````包下的注解。所有这些注解都有对应的 Web xsd 涵盖下的部署描述器元数据。

* ````HttpConstraint````
* ````HttpMethodConstraint````
* ````MultipartConfig````
* ````ServletSecurity````
* ````WebFilter````
* ````WebInitParam````
* ````WebListener````
* ````WebServlet````

下列不同路径下的注解同样涵盖于````web.xml````和相关片段之下。

````javax.annotation````包下：

* ````PostConstruct````
* ````PreDestroy````
* ````Resource````
* ````Resources````

````javax.annotation.security````包下：

* ````DeclareRoles````
* ````RunAs````

````javax.annotation.sql````包下：

* ````DataSourceDefinition````
* ````DataSourceDefinitions````

````javax.ejb````包下：

* ````EJB````
* ````EJBs````

````javax.jms````包下：

* ````JMSConnectionFactoryDefinition````
* ````JMSConnectionFactoryDefinitions````
* ````JMSDestinationDefinition````
* ````JMSDestinationDefinitions````

````javax.mail````包下：

* ````MailSessionDefinition````
* ````MailSessionDefinitions````

````javax.persistence````包下：

* ````PersistenceContext````
* ````PersistenceContexts````
* ````PersistenceUnit````
* ````PersistenceUnits````

````javax.resource:````包下：

* ````AdministeredObjectDefinition````
* ````AdministeredObjectDefinitions````
* ````ConnectionFactoryDefinition````
* ````ConnectionFactoryDefinitions````

下列包下的所有注解：

* ````javax.jws````
* ````javax.jws.soap````
* ````javax.xml.ws````
* ````javax.xml.ws.soap````
* ````javax.xml.ws.spi````

所有符合 Servlet 规范的 Web 容器都必须支持接下来的注解。

### 8.1.1 ````@WebServlet````

此注解用于在 web 应用中定义````Servlet````组件。此注解标注在类上，包含被声明````Servlet````的相关元数据。此注解的````urlPatterns```` 或者````value````属性必须存在。其它属性默认设置为可选。推荐的做法是，当注解上只有 url pattern 一个属性时使用````value````，而还有其他属性时使用````urlPatterns````。一个注解上同时使用````value````和````urlPatterns````属性是非法的。````Servlet````的默认名称如果没有专门指定则是类的全限定名。加上注解的````servlet````必须至少指定一个 url pattern 用于部署。如果同一个 servlet 类型在部署描述器中又以另外一个不同的名称声明，则另外一个新的 servlet 实例就必须被实例化。如果相同的 servlet 类通过程序方式 API 以不同的名称被添加到````ServletContext````中，则通过````@WebServlet````注解声明的属性值必须被忽略，指定名称的新的 servlet 实例必须被创建。

标注了````@WebServlet````注解的类都必须继承````javax.servlet.http.HttpServlet````类。

下面是这个注解如何使用的例子。

````java
@WebServlet("/foo")
public class CalculatorServlet extends HttpServlet{
    //...
}
````

````java
@WebServlet(name="MyServlet", urlPatterns={"/foo", "/bar"})
public class SampleUsingAnnotationAttributes extends HttpServlet{
    public void doGet(HttpServletRequest req, HttpServletResponse res){
        //...
    }
}
````

### 8.1.2 ````@WebFilter````

此注解用于在 web 应用中定义一个````Filter````。这个注解标注在类上，包含声明的过滤器的元数据。````Filter````的默认名称如果没有专门指定则就是类的全限定名。其````urlPatterns````、````servletNames````和````value````属性必须被指定。默认设定下其它所有属性是可选的。推荐的做法是，当注解上只有 url pattern 一个属性时使用````value````，而还有其他属性时使用````urlPatterns````。一个注解上同时使用````value````和````urlPatterns````属性是非法的。

标注了````@WebFilter````注解的类都必须实现````javax.servlet.Filter````接口。

下面是此注解使用的例子。

````java
@WebFilter("/foo")
public class MyFilter implements Filter{
    public void doFilter(HttpServletRequest req, HttpServletResponse res){
        //...
    }
}
````

### 8.1.3 ````@WebInitParam````

此注解用于指定任何需要传递给````Servlet````和````Filter````的初始化参数。它是````@WebServlet````和````@WebFilter````注解的一个属性。

### 8.1.4 ````@WebListener````

此注解用于在特定的 web 应用上下文中标注接收各种操作事件的监听器。此注解标注的类必须实现如下接口之一：

* ````javax.servlet.ServletContextListener````
* ````javax.servlet.ServletContextAttributeListener````
* ````javax.servlet.ServletRequestListener````
* ````javax.servlet.ServletRequestAttributeListener````
* ````javax.servlet.http.HttpSessionListener````
* ````javax.servlet.http.HttpSessionAttributeListener````
* ````javax.servlet.htttp.HttpSessionIdListener````

例子：

````java
@WebListener
public class MyListener implements ServletContextListener{
    public void contextInitialized(ServletContextEvent sce){
        ServletContext sc = sce.getServletContext();
        sc.addServlet("myServlet", "Sample servlet", "foo.bar.MyServlet", null, -1);
        sc.addServletMapping("myServlet", new String[]{"/urlpattern/*"});
    }
}
````

### 8.1.5 ````@MultipartConfig````

此注解标注在````Servlet````上时，表示期望到来的请求是````multipart/form-data````类型。对应于该````servlet````的````HttpServletRequest````对象必须通过````getParts````和````getPart````方法使 mime 附件可用，目的是遍历所有的 mime 附件。````javax.servlet.annotation.MultipartConfig````的````location````属性，````<multipart-config>````的````<location>````元素会被解释为绝对路径，默认值就是````javax.servlet.context.tempdir````的值。如果指定了相对路径，就是相对于该````tempdir````而言。必须通过````java.io.File.isAbsolute````来判断到底是绝对路径还是相对路径。

### 8.1.6 其它注解和约定

除了这些注解，所有本规范15.5章节“注解和资源注入”中定义的注解都将可以和这些新注解共同在上下文中工作。

默认情况下，所有应用的````welcome-file-lsit````文件列表中都包含````index.htm(l)````和````index.jsp````文件。部署描述器可以用来覆盖这些默认设定。

当使用注解时，从````WEB-INF/classes````或者````WEB-INF/lib````下的框架 jar 包和类文件中加载监听器和 Servlets 的顺序是未指定的。如果此加载顺序很重要，则可以参考本规范后续关于部署描述器文件的介绍，该顺序只能由部署描述器指定。

## 8.2 可插拔性

### 8.2.1 ````web.xml````的模块化

使用上面定义的注解时，可以有选择地使用````web.xml````。部署描述符被用于覆盖默认值或者通过注解设置的值。如前文所述，如果````web.xml````文件中的````metadata-complete````元素设置为````true````，类文件和 web-fragments 中指定部署信息的注解都将被忽略。这就暗示着应用的所有元数据实际上都是由````web.xml````部署描述器文件指定。

为了更好的可插拔性，同时减少开发者的配置工作，我们引入了 web 模块部署描述器片段（ web fragment ）的概念。一个 web 片段可以是````web.xml````的一部分或者就是其本身，位于类库或者框架 jar 包的````META-INF````目录下。位于````WEB-INF/lib````路径下的不包含````web-fragment.xml````文件的普通 jar 文件同样被认为是一个 web 片段。其中指定的任何注解将按照8.2.3章节中的规则被处理。容器将按照下面的规则挑选并使用配置。

Web 片段是 web 应用的逻辑分片，通过这种方式，应用于应用中的框架能够定义所有的应用组件，而不需要应用开发者在````web.xml````文件中编辑或者添加信息。它包含了几乎所有````web.xml````部署描述器使用的相同的元素。描述器的顶层元素必须是 web-fragment 而且相应的描述器文件名必须是````web-fragment.xml````。````web-fragment.xml````和````web.xml````文件中相关元素的顺序是不同的。更多细节可以参考本规范第14章内容。

如果框架被打包成 jar 文件形式，而且其包含的元数据以部署描述器的形式存在，则````web-fragment.xml````描述器就必须位于 jar 文件的````META-INF/````路径下。

如果一个框架希望它的````META-INF/web-fragment.xml````可以增强应用的````web.xml````，则该框架必须位于应用的````WEB-INF/lib````路径下。为了使得该框架的其它类型的资源对应用可用，该框架必须位于应用的类加载器委托链上的某个位置。换句话说，只有位于应用的````WEB-INF/lib````路径下的 JAR 文件，而不是那些高于类加载委托链的存在，需要基于````web-fragment.xml````文件被扫描。

部署过程中，容器负责扫描上面指定的位置，找到````web-fragment.xml````然后处理它们。命名唯一性需求在只存在单独的````web.xml````文件和同时存在````web-fragment.xml````文件情况下是一样的。

````xml
<web-fragment>
    <servlet>
        <servlet-name>welcome</servlet-name>
        <servlet-class>
            WelcomeServlet
        </servlet-class>
    </servlet>
    <listener>
        <listener-class>
            RequestListener
        </listener-class>
    </listener>
</web-fragment>
````

上面的````web-fragment.xml````文件可以被包含进入框架的 jar 文件的````META-INF/````目录。来自该文件和注解的配置信息被应用的顺序是未定义的。如果对应用来说这个顺序很重要，请参考接下来定义的规则以获得期望的顺序。

### 8.2.2 ````web.xml````和````web-fragment.xml````的顺序

由于此规范允许多个配置文件共同组成应用的配置资源，比如````web.xml````和````web-fragmeng.xml````文件，从若干不同的位置发现和加载它们，那么久必须考虑顺序问题。本章节说明了配置文件作者可以如何声明他们的组件的顺序需求。

````web-fragment.xml````文件可以包含类型为````javaee:java-identifierType````的顶级````<name>````元素。每个````web-fragment.xml````文件中只能有一个````<name>````元素。如果该元素存在，则组件顺序就必须考虑它，除非如下文所述发生重名异常。

两种情况必须被认为允许应用配置资源表达他们的顺序选择。

1. 绝对顺序：````web.xml````中的````<absolute-ordering>````元素，每个````web.xml````文件中只能存在一个该元素。

   a. 这种情况下，应该被按照下述第二种情况处理的顺序选择必须被忽略。

   b. ````web.xml````和````WEB-INF/classes````必须在````absolute-ordering````元素的 web-fragments 列表中的所有成员之前被处理。

   c. 任何````absolute-ordering````元素的直接孩子````<name>````元素都必须被解释为表示它们所指称的 web-fragments 的绝对顺序，无论是否存在，都必须被处理。

   d. ````absolute-ordering````元素可以包含零个或者一个````<others/>````元素。该元素的行为要求下文给出。如果````absolute-ordering````元素不包含````<others/>````元素，任何没有在````<name/>````元素中特别提到的 web-fragment 都必须被忽略。被排除的 jars 中的注解标注的 servlets、过滤器以及监听器都不会被扫描。然而，如果来自被排除的 jar 包的 servlet 、过滤器或者监听器被写入````web.xml````文件或者未被排除的````web-fragment.xml````文件，则除非被别的````metadata-complete````排除，相应的注解都将应用。在被排除的 jar 包的 TLD 文件中发现的````ServletContextListeners````并不能通过编程方式 APIs 配置过滤器和 servlet 。任何这么做的企图都将导致一个````IllegalStateException````异常。如果发现的````ServletContextListeners````是从被排除的 jar 包中加载，则它不会被忽略。与````metadata-complete````设定无关，被````<absolute-ordering>````元素排除的 jars 包中的类不会被任何````ServletContainerInitializer````扫描处理。

   e. 重名异常：如果在遍历````<absolute-ordering>````元素的子元素时，发现包含相同````<name>````元素的多个子元素，则只有第一个出现的会生效。

2. 相对顺序：````web-fragment.xml````文件中的一个````<ordering>````元素。每个````web-fragment.xml````文件中只能有一个````<ordering>````元素

   a. ````web-fragment.xml````文件中可能包含一个````<ordering>````元素，如果包含，则该元素必须包含0个或者一个````<before>````元素和0个或者一个````<after>````元素。这些元素的含义且看下文分解。

   b. ````web.xml````和 WEB-INF/classes 必须在````ordering````元素内列出的所有 web-fragments 之前被处理。

   c. 重名异常：如果在遍历 web-fragments 过程中，发现多个具有相同````<name>````元素的成员被发现，应用必须记录相应的错误日志以帮助解决此问题，同时部署必须失败。比如，修复此问题的一种办法就是为用户使用绝对顺序，此时相对顺序就会被忽略。

   d. 考虑这个简略的例子，3个 web-fragments ````MyFragment1````，````MyFragment2````，````MyFragment3````作为包含一个````web.xml````文件的应用的一部分。

   ````xml
   web-fragment.xml
   <web-fragment>
       <name>MyFragment1</name>
       <ordering><after><name>MyFragment2</name></after></ordering>
       ...
   </web-fragment>
   ````

   ````xml
   web-fragment.xml
   <web-fragment>
       <name>MyFragment2</name>
       ...
   </web-fragment>
   ````

   ````xml
   web-fragment.xml
   <web-fragment>
       <name>MyFragment3</name>
       <ordering><before><others/></before></ordering>
       ...
   </web-fragment>
   ````

   ````xml
   web.xml
   <web-app>
       ...
   </web-app>
   ````

   该例子中，处理顺序将是：

   ````xml
   web.xml
   MyFragment3
   MyFragment2
   MyFragment1
   ````

   上面的例子表明了一些，单并不是全部，如下原则：

   * ````<before>````意味着文件顺序必须在````<name>````元素中指定名称的文件之前。

   * ````<after>````意味着文件顺序必须在````<name>````元素中指定名称的文件之后。

   * 存在一个特殊的````<others/>````元素，它可能被````<before>````或者````<after>````元素包含0次或者一次，或者直接被````<absolute-ordering>````元素包含0次或者一次。该````<others>````元素必须如下处理。

     * 如果````<before>````元素包含一个内部````<others>````，则该文件将被移到有序文件列表的开头。如果````<before><others/>````包含多个文件，则它们都将被移到有序文件列表的开头，不过这些文件组内部顺序则是不确定的。
     * 如果````<after>````元素包含一个内部````<others>````，则该文件将被移到有序文件列表的末尾。如果````<after><others/>````包含多个文件，则它们都将被移到有序文件列表的末尾，不过这些文件组内部顺序则是不确定的。
     * 在````<before>````或者````<after>````元素中，如果存在一个````<others/>````元素，但是并不是它的父元素唯一的````<name>````元素，则同一个父元素的其它子元素必须按照此顺序处理。
     * 如果````<others/>````元素直接出现在````<absolute-ordering>````元素中，运行时就必须保证任何没有明确在````<absolute-ordering>````小节中命名 web-fragments 按照该处理顺序被包含在该处。

   * 如果一个````web-fragment.xml````文件中没有````<ordering>````元素，或者````web.xml````文件中不包含````<absolute-ordering>````元素，则该组件就假定不存在任何顺序依赖。

   * 如果运行时发现循环引用，则必须记录一条日志，同时应用部署必须失败。再者，用户就可以使用````web.xml````文件中的绝对顺序。

   * 上面的例子可以被扩展来展示````web.xml````文件包含一个 ordering 小节的情况。

     ````xml
     web.xml
     <web-app>
         <absolute-ordering>
             <name>MyFragment3</name>
             <name>MyFragment2</name>
         </absolute-ordering>
         ...
     </web-app>
     ````

     这个例子中，元素的处理顺序是：

     ````xml
     web.xml
     MyFragment3
     MyFragment2
     ````

     下面是一些使用相对顺序的例子：

     文件 A：

     ````xml
     <after>
         <others/>
         <name>
             C
         </name>
     </after>
     ````

     文件 B：

     ````xml
     <before>
         <others/>
     </before>
     ````

     文件 C：

     ````xml
     <after>
         <others/>
     </after>
     ````

     文件 D：无顺序。

     文件 E：无顺序。

     文件 F：

     ````xml
     <before>
         <others/>
         <name>
             B
         </name>
     </before>
     ````

     导致的顺序是：

     web.xml，F，B，D，E，C，A。

     文件 <no id> ：

     ````xml
     <after>
         <others/>
     </after>
     <before>
         <name>
             C
         </name>
     </before>
     ````

     文件 B：

     ````xml
     <before>
         <others/>
     </before>
     ````

     文件 C：无顺序。

     文件 D：

     ````xml
     <after>
         <others/>
     </after>
     ````

     文件 E：

     ````xml
     <before>
         <others/>
     </before>
     ````

     文件 F：无顺序。

     导致的顺序将是如下之一：

     * B，E，F，<noid>，C，D
     * B，E，F，<noid>，D，C
     * E，B，F，<noid>，C，D
     * E，B，F，<noid>，D，C
     * E，B，F，D，<noid>，C
     * E，B，F，C，<noid>，D

     文件 A：

     ````xml
     <after>
         <name>
             B
         </name>
     </after>
     ````

     文件 B：无顺序。

     文件 C：

     ````xml
     <before>
         <others/>
     </before>
     ````

     文件 D：无顺序。

     导致的顺序：C，B，D，A。

     也可能是：C，D，B，A 或者 C，B，A，D。    


### 8.2.3 组装来自````web.xml````、````web-fragment.xml````和注解的部署描述符

如果监听器、servlet 和过滤器被调用的顺序对一个应用是很重要的，则必须使用部署描述器文件。同时，如果有必要，上面定义的顺序元素可以被使用。就像上面描述的，当通过注解定义监听器、servlet 和过滤器时，它们被调用的顺序是不确定的。下面是一系列可用于组装应用最终的部署描述器文件的规则集合：

1. 如果监听器、servlets 和过滤器的顺序很重要，则该顺序必须在````web-fragment.xml````文件或者````web.xml````文件中指定。

2. 该顺序将基于它们在部署描述器中定义的顺序，如果存在，则基于````web.xml````中的````absolute-ordering````元素，或者基于````web-fragment.xml````文件中的````ordering````元素。

   a. 匹配到请求的过滤器会按照它们在````web.xml````文件中被声明的顺序被组成过滤器链。

   b. servlets 被初始化，要么在请求处理时懒加载，或者在部署过程中饥饿加载。在后一种情况中，它们会按照它们的````local-on-startup````元素说明的顺序被初始化。

   c. 监听器按照它们在````web.xml````文件中被声明的顺序被调用：

   ​	i. ````javax.servlet.ServletContextListener````的实现类的````contextInitialized````方法按照它们被声明的顺序被调用，````contextDestroyed````方法按照声明顺序的逆序被调用。

   ​	ii. ````javax.servlet.ServletRequestListener````的实现类的````requestInitialized````方法按照它们被声明的顺序被调用，````requestDestroyed````方法按照声明顺序的逆序被调用。

   ​	iii. ````javax.servlet.http.HttpSessionListener````的实现类的````sessionCreated````方法按照它们被声明的顺序被调用，````sessionDestroyed````方法按照声明顺序的逆序被调用。

   ​	iv.````javax.servlet.ServletContextAttributeListener````、````javax.servlet.ServletRequestAttributeListener````以及````javax.servlet.HttpSessionAttributeListener````的实现类的方法在相应的事件发出时被按照它们声明的顺序被调用。

3. 如果 servlet 通过````web.xml````文件中的````enabled````元素标识为不可用，则该 servlet 对````url-pattern````元素来说就是不可用的。

4. 当解析````web.xml````、````web-fragment.xml````以及注解过程中发生冲突时，````web.xml````文件对 web 应用中具有最高的优先级。

5. 如果部署描述器文件中没有指定````metadata-complete````元素，或者被设定为````false````，则有效的应用元数据就是有注解和部署描述器文件综合而来。两者合并的规则如下：

   a. web fragment 中的配置设定被作为参数用于指定主````web.xml````文件中的元素属性，就如同它们都是在同一个````web.xml````文件中那样。

   b. web fragment 中的配置设定被添加到主````web.xml````中的顺序在上面 8.2.2 章节中指定。

   c. 当主````web.xml````中的````metadata-complete````元素属性被设置为````true````时，部署时就会认为该文件中的元数据就是完整的，因而度注解的扫描和对 web fragment 的解析都不会发生。如果````absolute-ordering````和````ordering````元素存在，则会被忽略。当在某个 web fragment 中被设置为````true````之后，````metadata-complete````属性就只会被应用于某个特定 jar 文件中的注解扫描。

   d. 除非````metadata-complete````被设定为````true````，web fragments 都将被合并进入主````web.xml````文件。合并操作发生在相应的 web fragment 中的注解被处理之后。

   e. 使用 web fragment 扩展 ````web.xml````过程中下列情况被认为是出现了配置冲突：

   ​	i. ````<param-name>````相同的多个````<init-param>````元素的````<param-value>```` 不同。

   ​	ii. ````<extension>````相同的多个````<mime-mapping>````元素的````<mime-type>````不同。

   f. 上述配置冲突可以通过以下方式解决：

   ​	i. 主````web.xml````与 web fragment 之间的配置冲突的解决方案是规定````web.xml````中的配置具有更高优先级。

      ii. 两个 web fragment 之间的配置冲突，如果发生冲突的元素在主````web.xml````文件中不存在，将导致一个错误。相关错误信息必须被记录下来，同时应用的部署必须失败。

   g. 上述冲突被解决之后，下列附加规则应该被应用：​

      i. 可能被声明任意多次的元素可以通过````web-fragmensts````被添加到最终的````web.xml````中。比如，具有不同````<param-name>````的````<context-param>````元素会被添加。

      ii. 可能被声明任意多次的元素如果在````web.xml````中指定，则会覆盖````web-fragments````中指定的同名元素的值。

      iii. 如果一个最少可以不出现，最多可以出现一次的元素出现在 web fragment 中，但是并没有出现在主````web.xml````文件中。则该主````web.xml````就会从该 web fragment 中继承该设定。如果该元素同时出现在主````web.xml````文件和 web fragment 中，则主````web.xml````中的配置设定具有更高优先级。比如，如果两者都声明了同一个 servlet ，而且 web fragment 中的声明指定了````<load-on-startup>````元素，但是主````web.xml````中的声明并没有指定该元素，则该````<load-on-startup>````元素就会被用在合并之后的````web.xml````中。

      iv. 如果一个最少可以不出现，最多可以出现一次的元素出现在两个 web fragments，而且指定了不同的属性值，但是又没有出现在主````web.xml````文件中，则被认为是一个错误。比如，如果两个 web fragments 声明了同一个 servlet，但是指定了不同的````<load-on-startup>````元素，同时该 servlet 也在主````web.xml````文件中被声明，但是并没有指定任何````<load-on-startup>````元素，则必须报告一个错误。

      v. ````<welcome-file>````声明可添加。

      vi. 具有相同````<servlet-name>````的````<servlet-mapping>````元素通过````web-fragments````被添加。主````web.xml````文件指定的````<servlet-mapping>````将会覆盖````web-fragments````中具有相同````<servlet-name>````的````<servlet-mapping>````元素值。

      vii. 具有相同````<filter-name>````的````<filter-mapping>````元素通过````web-fragments````被添加。主````web.xml````文件指定的````<filter-mapping>````将会覆盖````web-fragments````中具有相同````<filter-name>````的````<filter-mapping>````元素值。

      viii. 具有相同````<listener-class>````的多个````<listener>````元素会被认为是一个````<listener>````声明。

      ix. 合并产生的````web.xml````被认为是````<distributable>````，仅当主````web.xml````和所有的 web fragments 都被标记为````<distributable>````。

      x. web fragment 中的顶层````<icon>````以及它的子元素，````<display-name>````以及````<description>````元素都会被忽略。

      xi. ````jsp-property-group````是可添加的。推荐，当将静态资源绑定到 jar 文件的````META-INF/resources````目录下时，````jsp-config````元素使用````url-pattern````作为扩展映射的对比。此外，web 片段的 JSP 资源应该在以片段名命名的子目录中，如果存在的话。这样可以防止 web 片段的````jsp-propety-group````影响到应用文件夹根目录中的 JSPs 或者在片段的````META-INF/resources````目录中的 JSPs 。

   h. 对所有的资源引用元素（````env-entry````，````ejb-ref````，````ejb-local-ref````，````service-ref````，````resource-ref````，````resource-env-ref````，````message-destination-ref````，````persistence-context-ref````以及````persistence-unit-ref````）应用下列规则：

      i. 如果所有资源引用元素都位于一个 web 片段中，同时都不在主````web.xml````文件中，该主````web.xml````从该 web 片段中继承这些值。如果元素在两者中都存在，而且具有相同的值，则````web.xml````优先。web 片段中的任何子元素都不会被合并进入主````web.xml````中，除非指定了````injection-target````。比如，如果主````web.xml````和 web 片段都声明了一个````<resource-ref>````元素，其````<resource-ref-name>````相同，则主````web.xml````文件中的````<resource-ref>````元素将会被使用，但是其所有子元素都不会被合并进来，除非如下文描述的那样指定````<injection-target>````。

     ii. 如果一个资源引用元素在两个片段中指定，而并没有出现在主````web.xml````中，同时所有的属性和子元素都是完全相同的，则该资源引用元素将会被合并进入主````web.xml````中。这种情况下，如果两个片段中的属性或者子元素不相同，则会被认为是一个错误。必须报告错误，同时应用部署必须失败。

     iii. 来自片段的具有相同名称的````<injection-target>````元素的资源引用元素将会被合并进入主````web.xml````。

   i. 除了上面说的````web-fragment.xml````的合并规则，当使用资源引用注解（````@Resource````,````@Resources````,````EJB````,````EJBs````,````@WebServiceRef````,````@WebServiceRefs````,````@PersistenceContext````,````@PersistenceContexts````,````@PersitenceUnit````,````PersistenceUnits````）时应用以下规则。

   如果一个资源引用注解被应用于一个类，它等价于定义了一个资源，但是它并不等价于定义一个````injection-target````。这种情况下上述规则就会被应用于````injection-target````元素。

   如果一个资源引用注解别用于一个字段，就等价于在````web.xml````中定义了一个````injection-target````元素。然而，如果部署描述器文件中没有定义````injection-target````元素，则片段中定义的该元素仍然将会被合并进入````web.xml````。

   如果主````web.xml````中存在一个````injection-target````元素，同时也存在一个相同资源名称的资源引用注解，则它就会被认为是资源引用注解的重写。这种情况下，由于部署描述器中定义了````injection-target````，上面定义的规则将应用，同时覆盖资源引用注解的值。

   j. 如果在两个片段中指定了同一个````data-source````元素，而主````web.xml````中没有，同时所有属性和子元素都完全相同，则该````data-source````元素将会被合并进入主````web.xml````中。这种情况下，如果两个片段中元素的属性或者子元素不是完全相同的，则会被认为是一种错误。该错误必须被报告，同时应用的部署必须失败。

   下面的例子展示了各种不同情况的结果。

   ````xml
   <!-- web.xml 没有资源引用定义 -->

   <!-- web-fragment.xml -->
   <resource-ref>
       <resource-ref-name="foo"/>
       ...
       <injection-target>
           <injection-target-class>
               com.example.Bar.class
           </injection-target-class>
           <injection-target-name>
               baz
           </injection-target-name>
       </injection-target>
   </resource-ref>

   <!-- 有效的原数据如下 -->
   <resource-ref>
       <resource-ref-name="foo"/>
       ...
       <injection-target>
           <injection-target-class>
               com.example.Bar.class
           </injection-target-class>
           <injection-target-name>
               baz
           </injection-target-name>
       </injection-target>
   </resource-ref>
   ````


   ````xml
   <!-- web.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
   </resource-ref>

   <!-- web-fragment.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target>
       <injection-target-class>
         com.example.Bar.class
       </injection-target-class>
       <injection-target-name>
         baz
       </injection-target-name>
     </injection-target>
   </resource-ref>

   <!-- web-fragment.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target>
       <injection-target-class>
         com.example.Bar2.class
       </injection-target-class>
       <injection-target-name>
         baz2
       </injection-target-name>
     </injection-target>
   </resource-ref>

   <!-- 生效的元数据 -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target>
       <injection-target-class>
         com.example.Bar.class
       </injection-target-class>
       <injection-target-name>
         baz
       </injection-target-name>
     </injection-target>
     <injection-target>
       <injection-target-class>
         com.example.Bar2.class
       </injection-target-class>
       <injection-target-name>
         baz2
       </injection-target-name>
     </injection-target>
   </resource-ref>
   ````

   ````xml
   <!-- web.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     <injection-target>
       <injection-target-class>
         com.example.Bar3.class
       </injection-target-class>
       <injection-target-name>
         baz3
       </injection-target-name>
     </injection-target>
   </resource-ref>

   <!-- web-fragment.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target>
       <injction-target-class>
         com.example.Bar.class
       </injction-target-class>
       <injection-target-name>
         baz
       </injection-target-name>
     </injection-target>
   </resource-ref>

   <!-- web-fragment.xml -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target-class>
       com.example.Bar2.class
     </injection-target-class>
     <injection-target-name>
       baz2
     </injection-target-name>
   </resource-ref>

   <!-- 生效的元数据 -->
   <resource-ref>
     <resource-ref-name="foo"/>
     ...
     <injection-target>
       <injection-target-class>
       	com.example.Bar3.class
     	</injection-target-class>
     	<injection-target-name>
       	baz3
     	</injection-target-name>
     	<injection-target-class>
       	com.example.Bar.class
     	</injection-target-class>
     	<injection-target-name>
       	baz
     	</injection-target-name>
     	<injection-target-class>
       	com.example.Bar2.class
     	</injection-target-class>
     	<injection-target-name>
       	baz2
     	</injection-target-name>
     </injection-target>
   </resource-ref>
   ````

   web 片段中的````<injection-target>````将会被合并进入主````web.xml````。

   k. 如果主````web.xml````中没有指定任何````<post-construt>````元素，而 web 片段中指定了，则片段中的该元素就会被合并进入主````web.xml````。然而，只要在主````web.xml````中指定一个该元素，片段中的所有该元素就都不会被合并。````web.xml````的作者有责任确保````<post-construct>````列表的完整性。

   l. 如果主````web.xml````中没有指定任何````<pre-destroy>````元素，而 web 片段中指定了，则片段中的该元素就会被合并进入主````web.xml````。然而，只要在主````web.xml````中指定一个该元素，片段中的所有该元素就都不会被合并。````web.xml````的作者有责任确保````<post-construct>````列表的完整性。

   m. 处理完````web-fragment.xml````之后，来自该片段的注解将会被处理以形成有效元数据，然后才开始处理下一个片段。下面的规则被用于注解处理。

   n. 任何没有出现在部署描述器文件中而是通过注解指定的元数据都将被用来增强部署描述器。

     i. ````web.xml````和````web-fragment.xml````中指定的配置优先级高于通过注解指定的配置。
    
     ii. 对通过````@WebServlet````注解定义的 servlet 来说，为了覆盖部署描述器指定的值，部署描述器中的 servlet 名称必须与注解定义的完全一样。
    
     iii. 通过注解定义的 servlets 和 filters 的初始化参数将被部署描述器中同名的初始化参数覆盖。注解和部署描述器中的初始化参数是相加关系。
    
     iv. 部署描述器中为给定名称的 servlet 指定的````url-patterns````将会覆盖注解为该 servlet 指定的。
    
     v. 对通过````@WebFilter````注解定义的 filter 来说，为了覆盖部署描述器指定的值，部署描述器中的 servlet 名称必须与注解定义的完全一样。
    
     vi. 部署描述器中为给定名称的 filter 指定的````url-patterns````将会覆盖注解为该 filter 指定的。
    
     vii. 部署描述器中为 filter 指定的分发类型将会覆盖通过注解指定的。
    
     viii. 下面的例子展示了上面的部分规则。

   一个 Servlet 通过一个注解声明，然后被部署描述器中对应的````web.xml````一同打包。

   ````java
   @WebServlet(urlPatterns="/MyPattern", initParams={@WebInitParam(name="ccc", value="333")})
   public class com.example.Foo extentds HttpServlet{
     ...
   }
   ````

   ````xml
   <!-- web.xml -->
   <servlet>
    	<servlet-class>com.example.Foo</servlet-class>
    	<servlet-name>Foo</servlet-name>
    	<init-param>
    		<param-name>aaa</param-name>
    		<param-value>111</param-value>
    	</init-param>
   </servlet>
   <servlet>
    	<servlet-class>com.example.Foo</servlet-class>
    	<servlet-name>Fum</servlet-name>
    	<init-param>
    		<param-name>bbb</param-name>
    		<param-value>222</param-value>
    	</init-param>
   </servlet>
   <servlet-mapping>
    	<servlet-name>Foo</servlet-name>
    	<url-pattern>/foo/*</url-pattern>
   </servlet-mapping>
   <servlet-mapping>
    	<servlet-name>Fum</servlet-name>
    	<url-pattern>/fum/*</url-pattern>
   </servlet-mapping>
   ````

   由于通过注解声明的 servlet 跟````web.xml````中声明的不同名，则该注解相当于指定了一个新的 servlet，与````web.xml````中声明的并列。等价于：

   ````xml
   <servlet>
    	<servlet-class>com.example.Foo</servlet-class>
    	<servlet-name>com.example.Foo</servlet-name>
    	<init-param>
    		<param-name>ccc</param-name>
    		<param-value>333</param-name>
   </servlet>
   ````

   如果上面的````web.xml````文件修改为：

   ````xml
   <servlet>
   	<servlet-class>com.example.Foo</servlet-class>
   	<servlet-name>com.example.Foo</servlet-name>
   	<init-param>
   		<param-name>aaa</param-name>
         	<param-value>111</param-value>
   	</init-param>
   </servlet>
   <servlet-mapping>
   	<servlet-name>com.example.Foo</servlet-name>
   	<url-pattern>/foo/*</url-pattern>
   </servlet-mapping>
   ````

   则最终生效的部署描述器等价于：

   ````xml
   <servlet>
   	<servlet-class>com.example.Foo</servlet-class>
   	<servlet-name>com.example.Foo</servlet-name>
   	<init-param>
   		<param-name>aaa</param-name>
   		<param-value>111</param-value>
   	</init-param>
   	<init-param>
   		<param-name>ccc</param-name>
   		<param-value>333</param-value>
   	</init-param>
   </servlet>
   <servlet-mapping>
   	<servlet-name>com.example.Foo</servlet-name>
   	<url-pattern>/foo/*</url-pattern>
   </servlet-mapping>
   ````

### 8.2.4 类库共享 / 运行时可插拔性

除了支持片段和注解的使用，其它强制性需求中的一条是，我们应该不仅能够将绑定到````WEB-INF/lib````中的组件作为插件，还能够将框架共享的包作为插件，包括可以将类似 JAX-WS、JAX-RS 以及 JSF 等构建在容器之上的组件作为插件。````ServletContainerInitializer````允许向下面描述的那样处理这种使用场景。

````ServletContainerInitializer````类通过 jar 服务 API 被找到。对每个应用来说，当应用启动时刻由容器创建一个````ServletContainerInitializer````实例。框架提供的````ServletContainerInitializer````实现必须被包含在````META-INF/services````目录下的 jar 文件中，文件名为````javax.servlet.ServletContainerInitializer````，作为 jar 服务 API，它指向````ServletContainerInitializer````的实现。

除了````ServletContainerInitializer````，我们还有一个注解````HandlesTypes````。该注解用在````ServletContainerInitializer````实现类上表示对某种类型感兴趣，这种类型可能拥有某些在````HandlesTypes````注解的值中指定的注解，或者该类型的父类型继承或实现了那些类中的某一个。````HandlesTypes````注解的应用不依赖````metadata-complete````的设定。

当检查一个应用中的类是否匹配````ServletContainerInitializer````实现类上的````HandlesTypes````注解指定的任一约束时，如果某些应用可选的 JAR 包缺失，容器可能会遭遇类加载问题。因为容器没有办法判定这些类型加载失败是否会导致应用无法正常工作，它就必须忽略这些类，同时提供配置选项以记录这些信息。

如果````ServletContainerInitializer````实现类上并没有````@HandlesTypes````注解，或者没有任何匹配到该注解指定的````HandlesType````的类型，则它将为每个应用被调用一次，其中````Set````参数值为````null````。这将允许初始化器基于应用中的可用资源决定是否应该初始化一个 servlet 或者过滤器。

````ServletContainerInitializer````实现类的````onStartup````方法将被调用，当应用启动而任何 servlet 监听器事件都尚未发出之前。

````ServletContainerInitializer````实现类的````onStartup````方法被调用时，传入的````Set````参数是继承或者实现了初始化器表现出对通过````@HandlesTypes````注解指定的类或者被那些类注解的类的关注。

下面有个具体的例子说明这是如何运作的。

现在介绍 JAX-WS web services 运行时。

JAX-WS 运行时实现通常不会默认绑定到每个 war 包中。该实现可以绑定一个````ServletContainerInitializer````实现类，同时容器将通过 services API 搜索之。

````java
@HandlesTypes(WebService.class)
JAXWSServletContainerInitializer implements ServletContainerInitializer {
    public void onStartup(Set<Class<?>> c, ServletContext ctx) throws ServletException {
        //JAX-WS 特定代码放在这里，用于初始化运行时和配置映射等。
        ServletRegistration reg = ctx.addServlet("JAXWSServlet", "com.sun.webservice.JAXWSServlet");
        reg.addServletMappings("/foo");
    }
}
````

框架的 jar 文件也可以被绑定在````web-inf/lib````目录下的 war 包中。如果````ServletContainerInitializer````实现类被绑定进入````WEB-INF/lib````目录下应用的 jar 文件中，它的````onStartup````方法就只会在绑定到的应用的启动过程中被调用一次。另一种情况，如果````ServletContainerInitializer````实现类位于````WEB-INF/lib````目录之外的 JAR 文件中，但是仍然能够被运行时服务发现机制搜索到，则它的````onStartup````方法就会在每次应用启动时被调用。

````ServletContainerInitializer````接口的实现类将被运行时服务发现机制或者容器特定的某种相同语义的类似机制发现。无论如何，来自 web fragment JAR 文件的````ServletContainerInitializer````服务如果从绝对顺序中排除则必须被忽略，同时这些服务被发现的顺序必须遵循应用的类加载委派模型。

   ## 8.3 JSP 容器可插拔性

````ServletContainerInitializer````以及编程式注册特性使得提供一个 servlet 和 JSP 容器的清楚的区别成为可能，servlet 容器的职责是仅仅处理````web.xml````和````web-fragment.xml````资源，同时将标签类库描述符资源的转化委派给 JSP 容器。

首先，一个 web 容器必须为所有监听器声明扫描 TLD 资源。在 servlet 3.0 及更高版本，该职责可以被委派给 JSP 容器。内置在 servlet 容器中的 JSP 容器可以提供自己的````ServletContainerInitializer````实现，为所有 TLD 资源搜索````ServletContext````传入它的````onStartup````方法，为监听器声明扫描这些资源，注册相应的监听器到````ServletContext````。

另外，在 servlet 3.0 之前，JSP 容器曾经必须为任何````jsp-config````相关配置扫描应用的部署描述器文件。在 servlet 3.0 及更高版本中，servlet 容器必须可以通过````ServletContext.getJspConfigDescriptor````方法访问来自应用的````web.xml````和````web-fragment.xml````部署描述器文件的任何````jsp-config````相关配置。

任何在 TLD 中的````ServletContextListeners````，通过编程方式注册，受限于它们提供的功能。任何调用它们之上````ServletContext````API 方法的企图都将导致一个````UnsupportedOperationException````异常。

进一步地，兼容 servlet 3.0 及以上版本的 servlet 容器必须提供一个````ServletContext````属性，该属性名为````javax.servlet.context.orderedLibs````，其值类型为````java.util.List<java.lang.String>````，其值包含````ServletContext````表示的应用的````WEB-INF/lib````目录下的 JAR 文件名列表，按照它们 web fragment 名称排序，可能存在排除的情况，如果片段 jar 包被从````absolute-ordering````中排除，或者其值为````null````如果应用没有指定任何绝对或者相对顺序。

   ## 8.4 处理注解和片段

   Web 应用可以同时包含注解、````web.xml````以及````web-fragment.xml````等部署描述器。如果没有部署描述器，或者存在部署描述器，但是````metadata-complete````属性没有被设置为````true````，则应用中存在的注解、````web.xml````以及````web-fragment.xml````等部署描述器都必须被处理。下表描述了在各种情况下是否应该处理注解、````web.xml````以及````web-fragment.xml````等部署描述器：

| 部署描述器                | metadata-complete | process annotations and web fragment |
| :------------------- | ----------------- | ------------------------------------ |
| web.xml 2.5          | yes               | no                                   |
| web.xml 2.5          | no                | yes                                  |
| web.xml 3.0 or later | yes               | no                                   |
| web.xml 3.0 or later | no                | yes                                  |

----

   # 请求分发

----

   构建 Web 应用时，将请求处理过程转发给别的 servlet 或者将别的 servlet 的输出包含在响应中是非常有用的。````RequestDispatcher````接口提供了该特性的实现机制。

   当请求的异步处理可用时，````AsyncContext````允许用户将请求转发回 servlet 容器。

   ## 9.1 获取````RequestDispatcher````

   通过下面两个方法可以从````ServletContext````中获取实现了````RequestDispatcher````接口的对象：

   * ````getRequestDispatcher````
   * ````getNamedDispatcher````

   ````getRequestDispatcher````方法使用一个字符串类型的参数，该参数描述````ServletContext````作用域内的一个路径。该路径必须相对于````ServletContext````的根目录，同时是以"/"开头，或者是空。该方法使用此路径来寻找 servlet ，根据第12章“映射请求到 servlets”，用````RequestDispatcher````对象包装它，然后返回结果对象。如果根据给定的路径找不到 servlet，则方法给出一个````RequestDispatcher````用于返回该路径内容。

````getNamedDispatcher````方法使用一个字符串类型的参数表示````ServletContext````所知的 servlet 名称。如果发现一个 servlet ，则用````RequestDispatcher````对象将其包装并返回该对象。如果规定名称并没有对应的 servlet ，则此方法返回````null````。

为了允许使用相对于当前请求（而不是````ServletContext````的根目录）的相对路径获取````RequestDispatcher````对象，````getRequestDispatcher````方法放在````ServletRequest````接口中。

该方法的行为类似于````ServletContext````中的同名方法。容器使用请求对象中的信息将给定的相对于当前请求的相对路径转化成为完整路径。例如，在根目录为"/"的上下文中，一个请求````/garden/tools.html````，通过````ServletRequest.getRequestDispatcher("header.html")````获取的请求分发器对象将和通过````ServletContext.getRequestDispatcher("/garden/header.html")````获取的对象行为完全一样。

### 9.1.1 请求分发路径中的查询字符串

````ServletContext````接口和````ServletRequest````接口提供的使用路径信息创建````RequestDispatcher````对象的方法允许路径附带查询字符串信息。例如，开发者可以通过下面代码获取````RequestDispatcher````：

````java
String path = "/raisins.jsp?orderno=5";
RequestDispatcher rd = context.getRequestDispatcher(path);
rd.include(request, response);
````

用于创建````RequestDispatcher````的路径查询参数指定的参数拥有相比于传入 servlet 的同名参数更高的优先级。````RequestDispatcher````相关参数的作用域仅限于````include````或者````forward````方法调用。

## 9.2 使用````RequestDispatcher````

为了使用请求分发器，servlet 调用````RequestDispatcher````接口的````include````方法或者````forward````方法。这些方法的参数要么是通过````javax.servlet.Servlet````接口的````service````方法传入的````request````或者````response````参数，要么是在2.3章节中介绍的请求和响应包装器类的子类。如果是后者，该包装器实例必须包装容器传入````service````方法的请求或者响应对象。

容器提供者应该保证将请求向目标 servlet 分发的动作发生在与原始请求同一个 JVM 的同一个线程内。

## 9.3 Include 方法

````RequestDispatcher````接口的````include````方法可以在任何时候被调用。该方法的目标 servlet 拥有请求对象的全部访问权限。但是对响应对象的使用则是有限制的。它只能向响应对象中的````ServletOutputStream````或者````Writer````写入信息，以及通过向响应缓冲区之后吸入内容，或者直接调用````ServletResponse````接口的````flushBuffer````方法来提交响应。它不能设置响应头部，或者调用任何能够影响响应头部的方法，调用````HttpServletRequest.getSession()````和````HttpServletRequest.getSession(boolean)````方法将发生异常。任何修改响应头部的企图都将被忽略，调用````HttpServletRequest.getSession()````和````HttpServletRequest.getSession(boolean)````方法，这些方法调用将导致添加 Cookie 响应头部，如果响应已经被提交，则必须抛出````IllegalStateException````。

如果默认 servlet 就是````RequestDispatcher.include()````方法的目标，同时请求的资源不存在，则默认 servlet 必须抛出````FileNotFoundException````。如果该异常没有被捕获并粗粒，则响应尚未提交，则响应状态码就必须设置为500。

### 9.3.1 包含的请求参数

除了通过````getNamedDispatcher````方法获取的 servlet ，别的 servlet 通过````RequestDispatcher````的````include````方法调用的 servlet ，都拥有它被调用时所在的路径的访问权限。

下列请求属性必须设定：

````java
javax.servlet.include.request_uri
javax.servlet.include.context_path
javax.servlet.include.servlet_path
javax.servlet.include.mapping
javax.servlet.include.path_info
javax.servlet.include.query_string
````

被包含的 servlet 这些属性可以通过请求对象的````getAttribute````方法访问，同时它们的值必须等于请求 URI 、上下文路径、servlet 路径、路径信息以及被包含的 servlet 的查询字符串。如果后续有请求被包含，则这些属性就会被包含进来的请求属性覆盖。如果被包含的 servlet 是通过````getNamedDispatcher````方法获取，则这些属性就不能被设置。

## 9.4 Forward 方法

````RequestDispatcher````接口的````forward````方法可以被调用，调用者 servlet 仅当输出尚未被提交给客户端时可以调用该方法。如果响应缓冲区中的输出数据尚未提交，则该内容在目标 servlet 的````service````方法被调用之前必须被清除。如果响应已经被提交，则必须抛出````IllegalStateException````异常。

暴露给目标 servlet 的请求对象的路径元素必须表达用于获取````RequestDispatcher````的路径。

唯一的例外就是通过````getNamedDispatcher````方法获取````RequestDispatcher````，这种情况下，请求对象的路径元素必须表示原始请求的路径。

````RequestDispatcher````接口的````forward````正常返回之前，响应内容必须被发送和提交，同时被容器关闭，除非请求进入异步模式。如果````RequestDispatcher.forward()````方法发生错误，则该异常会反向传播，穿过所有调用方过滤器和 servlets ，最终返回容器。

### 9.4.1 查询字符串

请求分发机制在转发和包含请求的同时负责聚合查询字符串参数。

### 9.4.2 转发请求参数

除了通过````getNamedDispatcher````方法获取的 servlet ，别的 servlet 通过````RequestDispatcher````的````forward````方法调用的 servlet ，都拥有它被调用时所在的路径的访问权限。

下列请求属性必须被设置：

````java
javax.servlet.forward.request_uri
javax.servlet.forward.context_path
javax.servlet.forward.servlet_path
javax.servlet.forward.mapping
javax.servlet.forward.path_info
javax.servlet.forward.query_string
````

这些属性的值必须等于在请求对象上调用````HttpServletRequest````的````getRequestURI````、````getContextPath````、````getServletPath````、````getPathInfo````、````getQueryString````方法的返回值，传递给调用链上第一个 servlet 对象，该对象接收来自客户端的请求。

这些属性可以通过请求对象上的````getAttribute````方法从被转发的 servlet 访问。注意，这些属性必须永远表示初始请求中的信息，即使是在多次转发和存在后续 includes 调用的情况下。

如果被转发的 servlet 通过````getNamedDispatcher````方法获取，这些属性就不能被设置。

## 9.5 错误处理

如果作为请求转发目标的 servlet 抛出运行期异常或者受检查的异常，````ServletException````或者````IOException````异常，它应该被传递给调用方 servlet 。所有其它异常应该被包装成````ServletException````，同时异常的根原因设置为初始异常，这种异常也不应该被传播。

## 9.6 获取异步上下文

实现了````AsyncContext````接口的对象可以通过````startAsync````方法从````ServletRequest````中获取。一旦你拥有了一个````AsyncContext````，就可以使用它要么通过````complete()````方法完成请求处理，要么使用下面介绍的````dispatch````方法之一。

## 9.7 Dispatch 方法

使用下列方法可以从````AsyncContext````分发请求：

* ````dispatch(path)````

  使用一个字符串参数的````dispatch````方法，该字符串参数表示````ServletContext````范围内的一个路径。该路径必须相对于````ServletContext````的根路径，并以'/'开头。

* ````dispatch(servletContext, path)````

  使用一个字符串参数的````dispatch````方法，该字符串参数表示给定````ServletContext````范围内的一个路径。该路径必须相对于````ServletContext````的根路径，并以'/'开头。

* ````dispatch()````

  无参方法，使用初始 URI 作为路径。如果````AsyncContext````通过````startAsync(ServletRequest, ServletReponse)````方法被初始化，同时请求被作为````HttpServletRequest````实例被传递，则转发的目标就是`````HttpServletRequest.getRequestURI()````方法返回的 URI 。否则，如果该转发就是容器的最后一次，则转发目标就是请求的 URI 。

````AsyncContext````接口的以上几个转发方法可以被等待异步事件发生的应用调用。如果````AsyncContext````的````complete()````方法已经被调用，就必须抛出````IllegalStateException````异常。各种分发方法立即返回并且放弃提交响应。

暴露给目标 servlet 的请求对象的路径元素必须表示````AsyncContext.dispatch````指定的路径。

### 9.7.1 查询字符串

请求分发机制在分发请求的同时负责聚合查询字符串。

### 9.7.2 被分发的请求参数

通过````AsyncContext````的````dispatch````方法被调用的 servlet 拥有初始请求路径的访问权限。

下列请求属性必须被设置：

```java
javax.servlet.async.request_uri
javax.servlet.async.context_path
javax.servlet.async.servlet_path
javax.servlet.async.mapping
javax.servlet.async.path_info
javax.servlet.async.query_string
```

这些属性的值必须等于在请求对象上调用````HttpServletRequest````的````getRequestURI````、````getContextPath````、````getServletPath````、````getPathInfo````、````getQueryString````方法的返回值，传递给调用链上第一个 servlet 对象，该对象接收来自客户端的请求。

这些属性可以通过请求对象上的````getAttribute````方法从被分发的 servlet 访问。注意，这些属性必须永远表示初始请求中的信息，即使是在多次分发的情况下。

----

# Web 应用

----

一个 Web 应用是一系列 servlets 、HTML 页面、类以及其它资源的集合，它们共同构成 Web 服务器上的完整应用。Web 应用可以被打包并运行在各个供应商提供的各种容器中。

## 10.1 Web 服务器上的 Web 应用

Web 应用位于 Web 服务器上特定路径下。例如，catalog 应用可能位于````http://www.example.com/catalog````路径。所有以该路径开头的请求都会被路由到表示该应用的````ServletContext````。

servlet 容器能够建立规则以自动产生 Web 应用。比如，````~user/````映射可以被用于映射到位于````/home/user/public_html/````的应用。

默认情况下，任何时候 Web 应用实例都必须只运行在一个虚拟机上，除非部署描述器文件中将该应用标志为分布式的。标志为分布式的应用必须遵循更多约束规则集合限制。这些限制规则遍布此规范始终。

## 10.2 与 ServletContext 的关系

容器必须强制保证 Web 应用和````ServletContext````的一一对应关系。````ServletContext````对象实际上提供了一个 servlet 以及 servlet 视角的应用视图。

## 10.3 Web 应用元素

Web 应用可以包含以下几种元素：

* Servlets
* JSP 页面
* 通用类
* 静态文件（HTML，图片，声音等）
* 客户端 Java applets ，beans，类
* 描述性元信息，将以上各种元素绑定在一起

 ## 10.4 部署层级结构

本规范定义了一个层级结构用于部署和打包目的，该层级结构存在于开发文件系统中，在压缩文件中，或者以其它形式存在。推荐，但不是必须，servlet 容器支持该结构作为运行时表现形式。

## 10.5 目录结构

Web 应用以文件夹层级结构的形式存在。该层级结构的根就是作为应用组成部分的文件夹根目录。比如，对于在容器中上下文路径为````/catalog````的应用，应用层级结构根目录中的````index.html````文件，或者````WEB-INF/lib````中 JAR 文件中````META-INF/resources````目录下包含的````index.html````文件，可以用于满足请求````/catalog/index.html````。如果上述两个位置都存在````index.html````文件，则必须使用位于应用根目录下的那个。请求 URL 映射到上下文路径的规则在12章中介绍。因为应用的上下文路径句诶桑了应用内容的 URL 命名空间，容器必须拒绝应用定义可能导致 URL 命名空间冲突的上下文路径。这是有可能发生的。比如，试图部署第二个具有相同上下文路径的应用。由于请求匹配到资源的过程是大小写敏感的，所以检测潜在命名空间冲突的过程也必须是大小写敏感方式。

应用文件夹中的特殊存在名为````WEB-INF````。该目录包含了不在应用根目录中的应用有关的所有内容。大部分````WEB-INF````节点并不是应用的公开文件夹树的一部分。除了````WEB-INF/lib````目录下的 JAR 文件的````META-INF/resources````目录下的静态资源和 JSP 包，````WEB-INF````目录下的其它文件都不能直接被用于向客户端提供服务。然而，该目录下的内容对于 servlet 是可见的，servlet 可以调用````ServletContext````的````getResource````或者````getResourceAsStream````方法访问它们。这些文件还可以通过````RequestDispatcher````调用暴露出来。因此，如果开发者需要访问 servlet 代码，或者应用指定的配置信息，而有不希望直接讲这些文件暴露给客户端，就可以把这些文件放在````WEB-INF````目录下。由于请求匹配到资源是大小写明感的，客户端请求````/WEB-INF/foo````或者````/WEb-iNf/foo````，都不应该得到应用的````WEB-INF````目录下的内容返回。

````WEB-INF````目录下的内容如下：

* ````/WEB-INF/web.xml```` 部署描述器
* ````/WEB-INF/classes```` servlet 和通用类文件夹，此文件夹中的类必须对应用的类加载器可用。
* ````/WEB-INF/lib/*.jar```` Java JAR 文件，这些文件包含 servlets 、beans 、静态资源以及打包进 JAR 文件的 JSP，以及其它对应用很有用的通用类。应用的类加载器必须可以从所有这些压缩文件中加载类。

应用的类加载器必须首先从````WEB-INF/classes````目录加载类，然后是````WEB-INF/lib````目录下的 JAR 文件。同时，除了打包进    JAR 文件的静态资源，任何访问````WEB-INF/````目录下资源的客户端请求都必须返回````SC_NOT_FOUND(404)````状态的响应。

### 10.5.1 应用目录结构的例子

下面是例子 Web 应用中所有文件的清单：

````
/index.html
/howto.jsp
/feedback.jsp
/images/banner.gif
/images/jumping.gif
/WEB-INF/web.xml
/WEB-INF/lib/jspbean.jar
/WEB-INF/lib/catalog.jar!/META-INF/resources/catalog/moreOffers/books.html
/WEB-INF/classes/com/mycorp/servlets/MyServlet.class
/WEB-INF/classes/com/mycorp/util/MyUtils.class
````

## 10.6 Web 应用压缩文件

Web 应用可以通过标准 Java 压缩工具被签名并打包成为 Web ARchive 格式文件（WAR）。例如，一个用于问题跟踪的应用可能被以````issuetrack.war````的形式发布。

当被打包为该形式之后，````META-INF````文件夹将存在其中，包含打包工具使用的重要信息。该文件夹内容不能被容器直接提供给客户端请求，但是对 servlet 代码是可见的，servlet 可以通过在````ServletContext````上调用````getResource````和````getResourceAsStream````方法访问。同时，任何访问````META-INF/````目录下资源的客户端请求都必须返回````SC_NOT_FOUND(404)````状态的响应。

## 10.7 部署描述器

部署描述器包含以下几种类型的配置和部署信息：

* ````ServletContext````初始化参数
* 会话配置
* Servlet/JSP 定义
* Servlet/JSP 映射
* MIME 类型映射
* 欢迎页面列表
* 错误信息页面
* 安全

### 10.7.1 对扩展的依赖

当大量应用都用到相同的代码或者资源时，典型的做法是将这些内容作为库文件安装进容器中。这些文件通常是普通的标准 API ，因此可以任意使用而不牺牲其可移植性。只被一个或者少数几个应用使用的文件将被作为应用的一部分而对应用可见。容器必须为这些文件提供响应的文件目录。该目录下的文件必须对所有 Web 应用都是可用的。对于不同的容器这个路径不尽相同。容器用来加载这些库文件的类加载器必须与处于同一个 JVM 中的所有应用使用的类加载器一样。该类加载器实例必须在应用的类加载器的父类加载器链上。

应用开发者必须知道哪些扩展被安装到了容器内，容器需要知道需要依赖这些类库文件中的哪些 servlets 以保持可移植性。

依赖以上形式扩展的应用开发者必须在 WAR 文件中提供一个````META-INF/MANIFEST.MF````实体用于列出所有需要的扩展。该实体内容格式应该遵循标准 JAR manifest 文件格式。在应用部署过程中，容器必须采用准确版本的扩展，确定扩展版本的规则由 Optional Package Versioning 机制定义。

````http://docs.oracle.com/javase8/docs/technotes/guides/extensions/versioning.html````

容器也必须能够识别 WAR 包的````WEB-INF/lib````路径下的类库 JAR 文件内的 manifest 实体内容中声明的依赖。

如果容器无法满足上述方式声明的依赖，则它应该通过包含准确信息的错误信息页面来拒绝该应用。

### 10.7.2 Web 应用类加载器

容器用于从 WAR 包中加载 servlet 的类加载器必须允许开发者通过正常的 Java SE 语法，使用````getResource````方法从 WAR 包中的类库文件中加载任意类型的资源。正如 Java EE 许可证文件中描述的，尽管 servlet 容器并不是 Java EE 产品的一部分，但是同样不能允许应用覆盖 Java SE 平台的类，比如````java.*````和````javax.*````命名空间下的类。容器不应该允许应用覆盖或者访问容器的实现类。推荐做法，应用的类加载器实现应该可以做到，打包进 WAR 包的类和资源可以在容器级别的类库文件中的类和资源之前被加载。一个实现必须保证对所有部署在容器内的应用，一个````Thread.currentThread.getContextClassLoader()````方法调用必须返回一个实现类本章节规范的````ClassLoader````实例。进一步的，该````ClassLoader````实例必须是专属于每个部署好的应用的。容器需要在让任何回调（包括监听器回调）进入应用之前，按照上面的描述设置线程上下文````ClassLoader````实例，同时一旦回调返回就将其设置回初始````ClassLoader````。

## 10.8 替换应用

服务器应该可以在不重启容器的情况下将应用更新为新版本。当一个应用被更新，容器应该提供一个健壮的方法用于保存应用中的会话数据。

## 10.9 错误处理

### 10.9.1 请求属性

Web 应用必须能够做到，当错误发生时，可以利用其它资源用于产生错误响应的内容体。这些资源的规范在部署描述器中描述。

如果错误处理器是 servlet 或者 JSP 页面，则：

* 由容器创建的初始的未包装的请求和响应对象被传入这个 servlet 或者 JSP 页面。
* 请求路径和属性被设置，就像指向错误资源的````RequestDispatcher.forward````方法被执行后一样。
* 下面表中的请求属性必须被设置。

| Request Attributes                 | Type                |
| ---------------------------------- | ------------------- |
| javax.servlet.error.status_code    | java.lang.Integer   |
| javax.servlet.error.exception_type | java.lang.Class     |
| javax.servlet.error.message        | java.lang.String    |
| javax.servlet.error.exception      | java.lang.Throwable |
| javax.servlet.error.request_uri    | java.lang.String    |
| javax.servlet.error.servlet_name   | java.lang.String    |

这些属性允许 servlet 基于状态码、异常类型、错误消息，被传播的异常对象、错误发生的 servlet（调用````getRequestURI````方法） 处理的请求的 URI 以及发生错误的 servlet 的逻辑名称等，产生特定的内容。

规范2.3版本介绍的异常对象属性列表中，异常对象和错误信息属性是冗余的，保留它们是为了保持对早期版本的兼容性。

### 10.9.2 错误页面

为了允许开发者自定义由 servlet 产生并返回 Web 客户端的错误信息，部署描述器定义了一系列错误页面描述。语法允许资源的配置呗容器返回，要么当 servlet 或者过滤器基于特定的状态码调用响应对象上的````sendError````方法，要么 servlet 产生一个异常或者错误然后传递给容器。

如果响应对象上的````sendError````方法被调用，容器就查阅应用声明的错误页面列表，基于状态码语法寻找匹配目标。如果找到匹配页面，容器就会把对应资源返回。

servlet 或者过滤器在处理请求过程中可以抛出以下异常：

* 运行时异常或者错误
* ````ServletException````或者它的子类
* ````IOException````或者它的子类

Web 应用可以使用````exception-type````元素声明错误页面。这种情况下，容器通过比较被抛出的异常和使用````exception-type````元素定义的错误页面列表匹配异常类型。匹配的结果在容器返回的资源中由位置实体表示。类层级中最精确的匹配会胜出。

如果没有````error-page````声明包含````exception-type````适合类层级匹配，而抛出的异常是````ServletException````或者其子类，容器会抽取包装后的异常，就像````ServletException.getRootCause````方法定义的那样。随后修改错误页面声明，再次尝试匹配错误页面声明，不过这次用的是包装过的异常。

在部署描述器中使用````exception-type````元素定义的错误页面声明，必须保证其异常类型类名的唯一性。同样的，在部署描述器中使用````status-code````元素定义的错误页面声明，必须保证其状态码的唯一性。

在部署描述器中的错误页面声明不包含````exception-type````元素和````status-code````元素，则此错误页面就是默认错误页面。

这里描述的错误页面机制在通过````RequestDispatcher````进行的调用或者````filter.doFilter````方法被调用时发生错误的情况下不会插手。此时，使用该````RequestDispatcher````的 servlet 或者过滤器就有机会处理产生的异常。

如果 servlet 产生的错误并没有被上述错误页面机制处理，则容器必须保证发送状态500的响应。

默认 servlet 和容器可以使用````sendError````方法发送4xx和5xx状态响应，因此错误页面机制可以被调用。它们使用````setStatus````方法发送2xx和3xx状态码响应，此时错误页面机制就不会被调用。

如果应用采用了异步操作，则应用就需要处理所有它创建的线程中的所有错误。容器可以处理通过````AsyncContext.start````创建的线程中发生的错误。在````AsyncContext.dispatch````方法过程中发生的错误的处理可以参考“````dispatch````方法执行过程中发生的所有错误和异常都必须被容器捕获并处理”章节。

### 10.9.3 错误过滤器

错误页面机制作用于容器创建的初始未包装和未过滤的请求和响应对象。6.2.5章节“过滤器和请求分发器”中描述的机制可以被用于指定过滤器在错误响应产生之前对请求或响应进行处理。

## 10.10 欢迎文件

Web 应用开发者可以在 Web 应用部署描述器中定义一个名为欢迎文件的部分 URIs 有序列表。关于这个列表的部署描述器语法在部署描述器规范中描述。

这种机制的目的是允许部署器指定一个部分 URIs 的有序列表，当请求的 URI 对应于 WAR 文件的一个目录实体，而并没有映射到 Web 组件时，容器用它来拼装 URI 。这种请求被称为有效部分请求。

举例说明这个机制的使用：

定义一个欢迎文件````index.html````，然后 URL 像是````host:port/webapp/directory````的请求，其中的````directory````是 WAR 包里的一个空目录，并不对应于 servlet 或者 JSP 页面，将会返回````host:port/webapp/dirctory/index.html````。

如果容器接收到一个有效部分请求，它必须检查部署描述器中定义的欢迎文件列表。欢迎文件列表是一个对应于部分 URLs 的有序列表，这些部分 URL 既不以‘/’开头也不以‘/’结尾。Web 服务器必须按照部署描述器中指定的顺序拼装每个欢迎文件，检查 WAR 包中的静态资源是否能够映射到该部分请求 URI 。如果没有发现匹配对象，服务器必须为部分请求再次按照部署描述器中指定的顺序拼装欢迎文件，然后检查是否有 servlet 映射到该请求 URI 。容器必须将该请求发送到 WAR 包中第一个匹配到的资源。容器可以讲请求发送到欢迎资源，通过 forward 、redirect 或者容器特定的机制，区别于直接来自请求。

如果按照上述过程没有找到匹配的欢迎文件，容器可以按照它能够找到的合适的方式处理请求。这就意味着，对于某些配置可以返回一个目录列表，对其它资源的请求则返回404状态码响应。

考虑如下的 Web 应用：

* 部署描述器列出如下欢迎文件：

````xml
<welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>default.jsp</welcome-file>
</welcome-file-list>
````

WAR 包中的静态资源如下：

````
/foo/index.html
/foo/default.jsp
/foo/orderform.html
/foo/home.gif
/catalog/default.jsp
/catalog/products/shop.jsp
/catalog/products/register.jsp
````

* URI 为````/foo````的请求将被 redirect 到````/foo/.````URI
* URI 为````/foo/````的请求将被返回为````/foo/index.html````
* URI 为````/catalog````的请求将被 redirect 到````/catalog/.````URI
* URI 为````/catalog/````的请求将被返回为````/catalog/default.jsp````
* URI 为````/catalog/index.html````的请求将导致一个````404 not found````
* URI 为````/catalog/products````的请求将被 redirect 到````/catalog/products/.````URI
* URI 为````/catalog/products/````的请求将被传递给默认 servlet ，如果有的话。否者，将得到一个````404 not found````，这将导致返回目录列表，包含````shop.jsp````和````register.jsp````，或者是容器定义的其它行为。参考12.2章节“映射规范”中定义的默认 servlet 。
* 上述所有的静态内容都可以被打包进 JAR 文件，连同上述打包进 JAR 文件中````META-INF/resources````目录中的内容。然后该 JAR 文件就能被包含进入应用的````WEB-INF/lib````目录。

## 10.11 Web 应用环境

Servlet 容器，并不是 Java EE 技术规范的一部分，我们鼓励而不强制要求其实现满足15.2.2章节中描述的应用环境的功能性要求。如果它们的实现并为完全满足该要求，对于部署于其中的应用，容器应当提供相应的警告机制。

## 10.12 Web 应用部署

当一个 web 应用被部署到容器中，在该应用开始处理客户端请求之前，下列步骤必须被按照顺序执行。

* 为部署描述器中每个````<listener>````元素实例化一个事件监听器实例
* 为实现了````ServletContextListener````的监听器实例调用其````contextInitialized()````方法
* 为部署描述器中每个````<filter>````元素实例化一个过滤器实例，然后调用每个过滤器实例的````init()````方法
* 按照````<load-on-startup>````元素定义的顺序为所有包含````<load-on-startup>````元素的每个````<servlet>````元素实例化一个 servlet 实例，同时调用每个 servlet 实例的````init()````方法

## 10.13 包含部署描述器 web.xml

web 应用不一定要包含 web.xml 文件，如果应用中没有任何 servlet、过滤器或者监听器组件，也没有用注解声明这些组件，就不需要该文件。换句话说，如果应用只包含静态文件或者 JSP 页面，则并不需要 web.xml 文件。

----

# 应用生命周期事件

----

## 11.1 介绍

应用事件机制给与应用开发者更大的控制力，包括对于````ServletContext````和````HttpSession````以及````ServletRequest````的生命周期的控制，允许更好的代码分解，以及更高效地管理应用中的资源。

## 11.2 事件监听器

应用事件监听器实现了一个或者多个 servlet 事件监听器接口。在应用部署过程中这些事件监听器被实例化并注册到容器中。它们由开发者在 WAR 包中提供。

Servlet 事件监听器支持````ServletContext````、````HttpSession````以及````ServletRequest````对象中的状态发生变化时发出的事件通知。Servlet 上下文监听器用于管理应用中处于 JVM 层面的资源和状态的管理。HTTP 会话监听器用于管理来自同一个客户端或者用户的一系列请求相关的资源和状态。Servlet 请求监听器用于管理整个 servlet 请求生命周期中的状态。异步监听器用于管理异步处理超时或者完成等事件。

可以有多个监听器在监听同一个类型的事件，开发者可以指定容器对每种事件类型以何种顺序调用其监听器实例。

### 11.2.1 事件类型和监听器接口

事件类型与监控它们的监听器接口如下：

servlet 上下文事件

| 事件类型 | 描述                                 | 监听器接口                                    |
| ---- | ---------------------------------- | ---------------------------------------- |
| 生命周期 | Servlet 上下文刚被创建，已经对首个请求可用，或者即将被关闭。 | ````javax.servlet.ServletContextListener```` |
| 属性变化 | Servlet 上下文属性被添加、删除或者替换。           | ````javax.servlet.ServletContextAttributeListener```` |

HTTP 会话事件

| 事件类型  | 描述                                | 监听器接口                                    |
| ----- | --------------------------------- | ---------------------------------------- |
| 生命周期  | ````HttpSession````已经被创建，不可用，或者超时 | ````javax.servlet.http.HttpSessionListener```` |
| 属性变化  | ````HttpSession````中的属性被添加、删除或者替换 | ````javax.servlet.http.HttpSessionAttributeListener```` |
| id 变化 | ````HttpSession````的 id 已经改变      | ````javax.servlet.http.HttpSessionIdListener```` |
| 会话迁移  | ````HttpSession````被激活或者冻结        | ````javax.servlet.http.HttpSessionActivationListener```` |
| 对象绑定  | 对象被绑定到````HttpSession````或者被从其上解绑 | ````javax.servlet.http.HttpSessionBindingListener```` |

Servlet 请求事件

| 时间类型 | 描述                                  | 监听器接口                                    |
| ---- | ----------------------------------- | ---------------------------------------- |
| 生命周期 | Web 组件开始处理请求                        | ````javax.servlet.ServletRequestListener```` |
| 属性变化 | ````ServletRequest````上的属性新增、删除或者替换 | ````javax.servlet.ServletRequestAttributeListener```` |
| 异步事件 | 异步处理超时、连接终止或者完成                     | ````javax.servlet.AsyncListener````      |

有关 API 的细节请参考 API 参考文档。

### 11.2.2 使用监听器的例子

为了举例说明事件体系的使用，考虑一个简单的 Web 应用，包含一系列使用数据库的 servlet 。开发者已经提供了一个 servlet 上下文监听器类用于管理数据库连接。

1. 当应用启动时，监听器类被通知。应用开始使用数据库，同时将数据库连接保存到 servlet 上下文中。
2. 在整个 Web 应用活动期间，应用中的 servlet 按需访问数据库连接。
3. 当 Web 服务器被关闭时，或者应用被从服务器上删除，监听器被通知到，然后数据库连接被关闭。

## 11.3 监听器类配置

### 11.3.1 监听器类规范

应用开发者提供的监听器类实现在````javax.servlet````API 中的一个或者多个监听器接口。每个监听器类都必须有一个公开的无参构造器。监听器类被打包进 WAR 包，要么在````WEB-INF/classes````路径下压缩包实体中，要么处于````WEB-INF/lib````目录下的 JAR 文件中。

### 11.3.2 部署声明

监听器类在应用的部署描述器中用````listener````元素声明。它们的类名按照将要被调用的顺序排列。与其它监听器不同，````AsyncListener````类型的监听器只能被通过编程方式注册（连同````ServletRequest````）。

### 11.3.3 监听器注册

容器在应用处理第一个请求之前创建每个监听器类实例并注册它用于监听通知事件。容器根据实现的接口以及出现在部署描述器中的顺序注册监听器实例。在应用执行过程中，监听器通常会按照注册顺序被调用，但是并不绝对。比如，````HttpSessionListener.destroy````就会被逆序调用。更多细节参见8.2.3章节。

### 11.3.4 关闭时的通知

当应用关闭时，监听器会被按照它们的声明顺序被逆序通知，首先通知会话监听器，然后通知上下文监听器。会话监听器必须在上下文监听器呗应用关闭事件通知到之前被会话无效事件通知到。

## 11.4 部署描述器举例

下面的例子说明如何在部署描述器中注册两个 servlet 上下文生命周期监听器和一个````HttpSession````监听器。

假定````com.example.MyConnectionManager````和````com.example.MyLoggingModule````都实现了````java.servlet.ServletContextListener````接口，同时````com.example.MyLoggingModule````另外还实现了````java.servlet.http.HttpSessionListener````接口。开发者希望````com.example.MyConnectionManager````可以在````com.example.MyLoggingModule````之前被 servlet 上下文生命周期时间通知到。下面就是该应用的部署描述器：

````xml
<web-app>
    <display-name>MyListeningApplication</display-name>
    <listener>
        <listener-class>com.example.MyConnectionManager</listener-class>
    </listener>
    <listener>
        <listener-class>com.example.MyLoggingModule</listener-class>
    </listener>
    <servlet>
        <display-name>RegistrationServlet</display-name>
    </servlet>
</web-app>
````

## 11.5 监听器实例和线程

容器必须保证在应用开始处理第一个请求之前完成所有监听器类的实例化。容器必须维护每个监听器实例的引用直到最后一个请求被应用服务完成。

````ServletContext````和````HttpSession````对象的属性变化必须同步发生。容器并不强制要求保证同步通知响应的属性监听器类实例。维护该状态的监听器类应该保证数据的完整性，同时应当明确地处理这种情况。

## 11.6 监听器异常

监听器内部的逻辑代码可以在执行过程中抛出异常。一些监听器通知发生在应用中其它组件的调用树之下。比如，一个 servlet 设定一个会话属性，而对应的会话监听器抛出了一个未经处理的异常。容器必须允许未处理的异常被错误页面机制处理。如果没有为该异常指定对应的错误页面，容器必须保证发送一个500状态码的响应。这种情况下该事件下其它监听器都不会被调用。

某些异常不是发生在应用中其它组件的调用栈之下。比如，一个````SessionListener````接收到一个会话超时事件通知，然后抛出了一个未处理的异常，或者一个````ServletContextListener````在处理 servlet 上下文初始化事件通知过程中抛出一个未处理的异常，再或者一个````ServletRequestListener````处理请求对象初始化或者析构事件通知过程中抛出一个未处理的异常。这种情况下，开发者没有机会处理异常。容器可以对接下来的请求统统返回状态码500响应，表示出现了应用错误。

开发者如果希望当监听器发生异常之后后续还能正常处理请求，则必须保证监听器在通知事件处理方法中自行处理该异常。

## 11.7 分布式容器

在分布式容器中，````HttpSession````实例的作用域局限于特定 JVM 服务的会话请求，````ServletContext````对象作用域就是容器所在的 JVM 。分布式容器不强制要求将 servlet 上下文事件或者````HttpSession````事件传播给别的 JVM 。监听器类实例作用域局限于每个 JVM 中的每个部署描述器。

## 11.8 会话事件

监听器类提供给开发者一种在应用中追踪会话的机制。会话追踪在某些情况下非常有用，比如判断会话实效是因为容器标记该会话超时，还是因为应用组件调用了````invalidate````方法。该区别可以直接由使用监听器和````HttpSession````接口方法决定。

----

# 映射请求到 Servlets

----

本章节中描述的映射技术被 Web 容器用于将客户端请求映射到 servlets 。

## 12.1 URL 路径使用

收到客户端i请求后，容器决定将其转发给某个应用。被选中的应用必须拥有最长的匹配到请求 URL 的前缀的上下文路径。匹配到的 URL 部分就是请求映射到 servlet 时的上下文路径。请求 URL 被以 UTF-8 进行字符串编码，实现可以提供容器提供商指定的配置用于改变此编码，或者采用更有效的编码来对请求 URI 的路径和查询字符串进行编码。注意，URL 之后剩余部分的编码可以配置，细节参见3.12章节“请求数据编码”。

容器接下来必须基于下面描述的路径映射过程来定位处理请求的 servlet 。

用于映射到 servlet 的路径是来自请求对象的 URL 减去上下文路径和路径参数之后的结果。URL 路径映射以此执行以下规则。找到首个成功的匹配就不会继续尝试匹配。

1. 容器将尝试发现一个请求路径到 servlet 路径的精确匹配，成功则选中该 servlet 。
2. 容器将递归尝试匹配最长路径前缀。该过程就是通过沿着路径树目录搜索，采用“/”作为路径分隔符。最长匹配决定了 servlet 选择。
3. 如果 URL 路径的最后一段包含一个扩展名，比如````.jsp````，则容器将尝试基于该扩展名匹配一个 servlet 来处理该请求。扩展名作为路径的最后一段，位于````.````字符之后。
4. 如果上述三条规则都未能匹配到 servlet ，容器将尝试基于被请求的资源提供合适的内容。如果应用中定义了所谓的“默认” servlet ，则其将被使用。许多容器都明确提供了默认 servlet 用于提供内容。

容器必须以大小写敏感的方式对路径进行字符串匹配。

## 12.2 映射规范

在应用的部署描述器文件中，下列语法用于定义映射：

* 以 "/" 字符开头、以 "/*" 后缀结尾的的字符串用于路径映射。
* 以 "*." 前缀开头的字符串被用作扩展映射。
* 空字符串 “” 是一个特殊 URL 模式，精确映射到应用的上下文根目录。比如，形如````http://host:port/<context-path>/````的请求。这种情况下，路径信息就是 “/” ，而 servlet 路径和上下文路径都是空字符串 “”。
* 只有一个 “/” 字符的字符串表示所谓的“默认” servlet 。这种i情况下，该 servlet 的路径就是请求 URL 减去上下文路径和路径信息，此时路径信息为空。
* 其它所有字符串都仅仅用于精确匹配。

如果有效的````web.xml````（合并所有应用片段和注解信息之后）包含任何可以映射到多个 servlet 的 url-pattern ，则应用部署必须失败。

### 12.2.1 隐式映射

如果容器拥有一个内部 JSP 容器，则````*.jsp````扩展名就会被映射到其上，同时允许 JSP 页面在真正需要时才执行。这种映射称为隐式映射。如果````*.jsp````映射被应用定义了，则该定义就拥有比隐式映射更高的优先级。

本规范允许容器拥有更多其它的隐式映射，只要保证显式映射优先级更高。例如，一个````*.shtml````的隐式映射可以被映射到服务器上的某些内置功能。

### 12.2.2 映射集合举例

考虑下面的映射集合：

| 路径模式               | Servlet  |
| ------------------ | -------- |
| ````/foo/bar/*```` | servlet1 |
| ````/baz/*````     | servlet2 |
| ````/catalog````   | servlet3 |
| ````*.bop````      | servlet4 |

将导致如下行为：

| 请求路径                         | 处理请求的 Servlet |
| ---------------------------- | ------------- |
| ````/foo/bar/index.html````  | servlet1      |
| ````/foo/bar/index.html````  | servlet1      |
| ````/baz````                 | servlet2      |
| ````/baz/index.html````      | servlet2      |
| ````/catalog````             | servlet3      |
| ````/catalog/index.html````  | 默认 servlet    |
| ````/catalog/racecar.bop```` | servlet4      |
| ````/index.bop````           | servlet4      |

注意，````/catalog/index.html````和````/catalog/racecar.bop````的情况下，对应于````/catalog````的 servlet 不会被使用，因为它不是最精确匹配。

## 12.3 运行时映射发现

每个映射都会导致对应的 servlet 被激活，无论是否涉及到 servlet 过滤器。所有的映射都必须是能够通过 servlet 映射 API  在运行时被发现。

### 12.3.1 运行时 Servlet 映射发现

````HttpServletRequest````上的````getHttpServletMapping()````方法返回一个````HttpServletMapping````实现，提供了映射信息，该映射导致当前 Servlet 被调用。请参考相关规范获取进一步信息。当和被转发或者包含的请求参数在一起时，````HttpServletMapping````对已经被包含进````ServletContext.getNamedDispatcher()````方法调用的 servlet 不可用。

----

# 安全

----

Web 应用被应用开发者创建，然后被传输给应用部署者安装到运行环境中。应用开发者与部署者和部署环境沟通相关的安全需求。这些信息通过应用的部署描述器明确声明，或者在应用代码中用注解声明，或者通过````ServletRegistration.Dynamic````接口的````setServletSecurity````方法以程序方式声明。

本章描述容器的安全机制，相关接口、部署描述器、注解以及编程方式等声明应用的安全需求。

## 13.1 介绍

Web 应用包含的资源可以被很多用户访问。这些资源通常会穿越开放而缺乏保护的网络，例如因特网。在这种环境下，应用通常都会需要安全机制。

尽管实现细节和服务质量保证各有不同，容器拥有的满足应用安全需求的机制和基础设施通常都有如下共性：

* 身份认证：相互沟通的实体相互之间证明自己基于指定的身份已经获取资源的访问授权。
* 资源访问控制：资源访问主题局限于某些用户或者程序的集合，以实现完整性控制、保密或者可用性约束等。
* 数据完整性：证明数据传输过程中没有被第三方篡改。
* 保密或者数据私密性：保证数据只对已经或者访问授权的用户是可用的。

## 13.2 声明式安全

声明式安全意思是以一种应用外部形式表达应用的安全模型或者安全需求，包括角色，访问控制，以及认证需求。应用中的部署描述器文件是声明式安全的主要载体。

部署者将应用的逻辑安全需求映射到特定运行环境的安全策略的表达。在运行时，servlet 容器使用安全策略表达来保证身份认证和鉴权。

应用于应用静态内容部分的安全模型和应用到 servlet 和过滤器的安全策略都在接收客户端请求的应用内部。安全模型不会起作用，当 servlet 使用````RequestDispatcher````来调用静态资源或者使用````forward````或者````include````。

## 13.3 编程式安全

编程式安全用于安全名感的应用，这种应用中单纯的声明式去安全不足以表达应用的安全模型。编程式安全由````HttpServletRequest````接口的以下方法组成：

* ````authenticate````
* ````login````
* ````logout````
* ````getRemoteUser````
* ````isUserInRole````
* ````getUserPrincipal````

````login````方法允许应用处理用户名和密码集合，就像另外一种基于表单的登录接口。

````authenticate````方法允许应用驱动容器对来自无约束的请求上下文的请求的调用者进行身份认证。

````logout````方法使得应用可以重置请求发起者的身份。

````getRemoteUser````方法返回远程调用者的名字，在这里就是请求发起者。该方法由容器对请求使用。

````isUserInRole````方法决定发起请求的远程用户是否属于某个特定安全角色。

````getUserPrincipal````方法决定发起请求的远程用户的主体名称，返回对应于远程用户的````java.security.Principal````对象。调用````Principal````上的````getName````方法将会由````getUserPrincipal````返回远程用户的名称。这些 API 允许 servlet 基于由此获取的信息进行业务逻辑决策。

如果没有已经认证过身份的用户，则````getRemoteUser````方法返回````null````，````isUserInRole````方法永远返回````false````，````getUserPrincipal````方法返回````null````。

````isUserInRole````方法使用一个作为应用中角色的引用的字符串类型的参数。调用该方法使用的每个独立的角色引用，都需要在部署描述器文件中声明一个对应的同名安全角色引用元素。每个安全角色引用都应该包含一个角色链接子元素，其值就是应用内置的角色引用链接到的应用安全角色的名字。容器通过角色名字使用这些安全角色引用以确定用户属于哪个安全角色。

例如，将安全角色引用 “FOO” 映射到名为 “manager” 的安全角色的语法如下：

````xml
<security-role-ref>
    <role-name>FOO</role-name>
    <role-link>manager</role-link>
</security-role-ref>
````

这种情况下，如果属于 “manager” 安全角色的用户调用的 servlet 调用````isUserInRole("FOO")````，结果将为````true````。

如果被用于````isUserInRole````方法调用的角色引用并没有匹配的````security-role-ref````存在，容器必须测试用户是否属于角色名称等于用于该方法调用的角色引用的安全角色。

角色名称 "*" 永远不应该被作为````isUserInRole````方法的参数。任何这样的尝试都必须返回````false````。如果被测试的安全角色的角色名称是 “**”，而应用又没有声明一个角色名为 “\*\*” 的安全角色，````isUserInRole````方法必须返回````true````。

如果用户已经经过身份认证，则````getRemoteUser````和````getUserPrincipal````方法将都返回非空值。否则，容器必须检测用户是否属于应用的角色。

````security-role-ref````元素声明将应用使用的角色引用通知给部署者，同时必须为这些元素定义相应的映射。

## 13.4 编程式安全策略配置

本章节定义用于配置容器强制的安全约束的注解和 API 。

### 13.4.1 ````@ServletSecurity````注解

此注解提供了定义访问控制约束的另一种方式，等效于通过部署描述器中````security-constraint````元素实现的声明方式，或者通过````ServletRegistration````接口的````setServletSecurity````方法实现的编程方式。容器必须支持在实现了````javax.servlet.Servlet````接口的类及其子类上使用本注解。

````java
package javax.servlet.annotation;

@Inherited
@Documented
@Target(value=TYPE)
@Retention(value=RUNTIME)
public @interface ServletSecurity{
    HttpConstraint value();
    HttpMethodConstraint[] httpMethodConstraints();
}
````

| 元素                            | 描述                                       | 默认                      |
| ----------------------------- | ---------------------------------------- | ----------------------- |
| ````value````                 | 定义了应用于不在````httpMethodConstraints````方法返回的方法数组中的方法的保护措施 | ````@HttpConstraint```` |
| ````httpMethodConstraints```` | HTTP 方法特定约束数组                            | {}                      |

````@HttpConstraint````

此注解与````@ServletSecurity````注解共同使用，表示安全约束将被应用于所有那些````@HttpMethodConstraint````没有与````@ServletSecurity````注解共同出现 HTTP 协议方法。

当一个返回所有默认值的````@HttpConstraint````注解与至少一个返回其他所有默认值的````@HttpMethodConstraint````注解组合出现的特殊情况下，该````@HttpConstraint````注解表示没有安全约束将被应用于任何其它安全约束将要应用于的 HTTP 协议方法。这个例外的目的是保证这种未特别说明的````@HttpConstraint````使用方式不会对将显式建立无包含访问机制的方法产生安全约束，这样它们就不会被别的安全约束覆盖掉。

````java
package javax.servlet.annotation
@Documented
@Retention(value=RUNTIME)
  public @interface HttpConstraint {
  ServletSecurity.EmptyRoleSemantic value();
  java.lang.String[] rolesAllowed();
  ServletSecurity.TransportGuarantee transportGuarantee();
}
````

| 元素                         | 描述                                      | 默认值    |
| -------------------------- | --------------------------------------- | ------ |
| ````value````              | 仅当````rolesAllowed````返回一个空数组时应用的默认授权语义 | PERMIT |
| ````rolesAllowed````       | 包含已授权角色的名称的数组                           | {}     |
| ````transportGuarantee```` | 请求到达时所属连接必须满足的数据保护需求                    | NONE   |

````@HttpMethodConstraint````

此注解与````@ServletSecurity````注解共同使用，表示对特定 HTTP 协议消息的安全约束。

````java
package javax.servlet.annotation
@Documented
@Retention(value=RUNTIME)
public @interface HttpMethodConstraint {
  ServletSecurity.EmptyRoleSemantic value();
  java.lang.String[] rolesAllowed();
  ServletSecurity.TransportGurantee transportGurantee();
}
````

| 元素                         | 描述                                      | 默认值    |
| -------------------------- | --------------------------------------- | ------ |
| ````value````              | HTTP 协议方法名称                             |        |
| ````emptyRoleSemantic````  | 仅当````rolesAllowed````返回一个空数组时应用的默认授权语义 | PERMIT |
| ````rolesAllowed````       | 包含已授权角色的名称的数组                           | {}     |
| ````transportGuarantee```` | 请求到达时所属连接必须满足的数据保护需求                    | NONE   |

````@ServletSecurtiy````注解可以被指定到（也就是说，针对性地用于）某个````Servlet````实现类，同时其值可以被子类继承，继承规则按照 ````@Inherited````元数据定义的规则进行。每个````Servlet````实现类中最多只能有一个````@ServletSecurity````注解实例，而且该注解绝对不能被指定到（也就是说，针对性用于）一个 Java 方法。

当一个或者多个````@HttpMethodConstraint````注解在````@ServletSecurity````注解内定义时，每个````@HttpMethodConstraint````定义相应的````security-constraint````应用于由````@HttpMethodConstraint````注解标记的 HTTP 协议方法。除非，其````@HttpConstraint````返回所有默认值，同时它所包含的至少一个````@HttpMethodConstraint````返回其它的默认值，则````@ServletSecurity````定义的另一个````security-constraint````被用于所有那些相应的````@HttpMethodConstraint````没有被定义的 HTTP 协议方法。

在可移植部署描述器文件中定义的````security-constraint````元素对该约束中出现的所有````url-pattern````都是权威的。

当可移植部署描述器文件中的````security-constraint````包含的````url-pattern````完全符合映射到一个注解了````@ServletSecurity````的类的模式时，该注解必须保证不影响 Servlet 容器施加到该模式上的约束。

当可移植部署描述器文件中定义了元素````metadata-complete=true````，则````@ServletSecurity````注解就不会应用到任何映射到部署描述器文件中添加了该注解的类的````url-patterns````上。

````@ServletSecurity````注解不会应用于通过````ServletContext````接口的````addServlet(String, Servlet)````方法创建的````ServletRegistration````的````url-patterns````，除非````Servlet````是通过````ServletContext````接口的````createServlet````方法创建的。

除了上面列出的例外情况，当一个 Servlet 类添加了````@ServletSecurity````注解，该注解定义的安全约束就会应用到所有映射到该 Servlet 映射到的类的所有````url-patterns````上。

当一个类并没有被````@ServletSecurity````注解，则该类映射到的 servlet 的访问策略就基于可用的````security-constraint````元素建立，如果真的有的话，在对应的可移植部署描述器文件中，或者基于这些约束排除所有这些元素，如果存在的话，通过````ServletRegistration````接口的````setServletSecurity````方法为目标 servlet 以程序方式建立。

#### 13.4.1.1 例子

下面的例子展示了````@ServletSecurity````注解的使用：

````java
// 对所有 HTTP 方法，都没有约束
@ServletSecurity
public class Example1 extends HttpServlet {
    
}
````

````java
// 对所有 HTTP 方法，没有身份认证约束、保密传输要求
@ServletSecurity(@HttpConstraint(transportGuarantee = TransportGurantee.CONFIDENTIAL))
public class Example2 extends HttpServlet {
    
}
````

````java
// 所有 HTTP 方法，所有的访问都拒绝
@ServletSecurity(@HttpConstraint(EmptyRoleSemantic.DENY))
public class Example3 extends HttpServlet {
    
}
````

````java
// 对所有的 HTTP 方法，身份认证约束要求属于角色 R1
@ServletSecurity(@HttpConstraint(rolesAllowed = "R1"))
public class Example4 extends HttpServlet {
    
}
````

````java
// 对 GET 和 POST 方法，身份认证约束要求属于角色 R1，对于 POST 方法，需要保密传输。其它方法没有约束。
@ServletSecurity(httpMethodConstraints = {
    @HttpMethodConstraint(value = "GET", rolesAllowed = "R1"),
    @HttpMethodConstraint(value = "POST", rolesAllowed = "R1",
    transportGuarantee = TransportGurantee.CONFIDENTIAL)
})
public class Example5 extends HttpServlet {
    
}
````

````java
// 对 GET 方法，没有约束，其它方法的身份认证约束要求属于角色 R1
@ServletSecurity(value = @HttpConstraint(rolesAllowed = "R1"),
                httpMethodConstraints = @HttpMethodConstraint("GET"))
public class Example6 extends HttpServlet {
    
}
````

````java
// 对 TRACE 方法，所有访问都拒绝，其它方法，身份认证约束需要属于角色 R1
@ServletSecurity(value = @HttpConstraint(rolesAllowed = "R1"),
                httpMethodConstraints = @HttpMethodConstraint(value="TRACE",
                emptyRoleSemantic = EmptyRoleSemantic.DENY))
public class Example7 extends HttpServlet {
    
}
````

#### 13.4.1.2 映射 @ServletSecurity 到安全约束

本节描述将````@ServletSecurity````注解映射到与它等价的````security-constraint````元素表示的过程。它被作为基础设施增强提供，使用容器现有的````security-constraint````增强机制。Servlet 容器提供的对````@ServletSecurity````注解的增强，必须于容器提供的等价，作用于本章节定义的````security-constraint````元素。

````@ServletSecurity````注解被用于定义一个方法无关的````@HttpConstraint````连同 0 个或者多个````@HttpMethodConstraint````列表。如果没有定义 HTTP 方法约束，则该方法无关的约束就会被应用于所有 HTTP 方法。

当没有包含````@HttpMethodConstraint````元素时，一个````@ServletSecurity````注解对应于一个单独的````security-constraint````元素，该元素包含的````web-resource-collection````不包含````http-method````元素，将会作用于所有 HTTP 方法。

下面的例子描述了一个没有包含````@HttpMethodConstraint````注解的````@ServletSecurity````注解作为一个单独的````security-constraint````元素的表现形式。由对应的 servlet 定义的````url-pattern````元素将被包含在````web-resource-collection````中，同时其中包含的````auth-constraint````和````user-data-constraint````元素的存在性和取值将都由````@HttpConstraint````注解的映射的值确定。

映射不包含````@HttpMethodConstraint````的````@ServletSecurity````

````java
@ServletSecurity(@HttpConstraint(rolesAllowed = "Role1"))
````

````xml
<security-constraint>
    <web-resource-collection>
        <url-pattern>...</url-pattern>
    </web-resource-collection>
    <auth-constraint>
        <role-name>Role1</role-name>
    </auth-constraint>
</security-constraint>
````

当一个或者多个````@HttpMethodConstraint````元素被指定，则方法无关约束对应于一个单独````security-constraint````包含一个````web-resource-collection````，对每个在````@HttpMethodConstraint````元素中命名的 HTTP 方法，它都包含在````@HttpMethodConstraint````元素中。如果方法无关约束返回所有的默认值而至少有一个````@HttpMethodConstraint````不这样做时，包含````http-method-omission````元素的````security-constraint````绝不能被创建。每个````@HttpMethodConstraint````对应于另外的````security-constraint````包含一个````web-resource-collection````包含一个````http-method````元素命名对应的 HTTP 方法。

下面的例子展示了包含一个````@HttpMethodConstraint````的````@ServletSecurity````注解映射到两个安全约束元素的过程。由相应的 servlet 定义的````url-pattern````元素将会被包含在两个约束的````web-resource-collection````中，同时，其中包含的````auth-constraint````和````user-data-constraint````元素的存在与否和值都取决于相应的````@HttpConstraint````和````@HttpMethodConstraint````注解的映射。

包含````@HttpMethodConstraint````的````@ServletSecurity````注解的映射：

````java
@ServletSecurity(value=@HttpConstraint(rolesAllowed = "Role1"),
                httpMethodConstraints = @HttpMethodConstraint(value = "TRACE",
                emptyRoleSemantic = EmptyRoleSemantic.DENY))
````

````xml
<security-constraint>
    <web-resource-collection>
        <url-pattern>...</url-pattern>
        <http-method-omission>TRACE</http-method-omission>
    </web-resource-collection>
    <auth-constraint>
        <role-name>Role1</role-name>
    </auth-constraint>
</security-constraint>
<security-constraint>
    <web-resource-collection>
        <url-pattern>...</url-pattern>
        <http-method>TRACE</http-method>
    </web-resource-collection>
    <auth-constraint/>
</security-constraint>
````

#### 13.4.1.3 ````@HttpConstraint````和````@HttpMethodConstraint````映射到 XML

本节描述将````@HttpConstraint````和````@HttpMethodConstraint````注解值（定义来使用在````@ServletSecurity````中）映射到对应的````auth-constraint````和````user-data-constraint````表示形式。这些注解共享了一个通用模型来表达等价的````auth-constraint````和````user-data-constraint````元素在可移植的部署描述器文件中使用。该模型由以下三个元素组成：

* ````emptyRoleSemantic````

  授权语义，要么是````PERMIT````要么是````DENY````，当没有角色被````rolesAllowed````命名时应用。此元素的默认值是````PERMIT````，同时，````DENY````不被支持与非空的````rolesAllowed````列表的组合。

* ````rolesAllowed````

  包含已授权角色名称的列表。当该列表为空，意味着依赖````emptyRoleSemantic````的值。在被允许的角色列表中包含的角色名"\*"没有特殊含义。当特殊角色名称"\*\*"出现在````rolesAllowed````中，表示用户身份认证独立于角色。此元素的默认值是一个空列表。

* ````transportGuarantee````

  数据保护需求，要么是````NONE````要么是````CONFIDENTIAL````，请求到达时所在连接必须满足的条件。此元素等价于包含对应值的````transport-guarantee````的````user-data-constraint````。此元素的默认值是````NONE````。

下面的例子展示了上面描述的````@HttpConstraint````模型与 web.xml 文件中的````auth-constraint````和````user-data-constraint````元素之间的对应关系。

````xml
emptyRoleSemantic=PERMIT, rolesAllowed={}, transportGuarantee=NONE
<!-- 等价于 -->
no constraints
````

````xml
emptyRoleSemantic=PERMIT, rolesAllowed={}, transportGuarantee=CONFIDENTIAL
<!-- 等价于 -->
<user-data-constraint>
    <transport-guarantee>CONFIDENTIAL</transport-guarantee>
</user-data-constraint>
````

````xml
emptyRoleSemantic=PERMIT, rolesAllowed={Role1}, transportGuarantee=NONE
<!-- 等价于 -->
<auth-constraint>
    <security-role-name>Role1</security-role-name>
</auth-constraint>
````

````xml
emptyRoleSemantic=PERMIT, rolesAllowed={Role1}, transportGuarantee=CONFIDENTIAL
<!-- 等价于 -->
<auth-constraint>
    <security-role-name>Role1</security-role-name>
</auth-constraint>
<user-data-constraint>
    <transport-guarantee>CONFIDENTIAL</transport-guarantee>
</user-data-constraint>
````

````xml
emptyRoleSemantic=DENY, rolesAllowed={}, transportGuarantee=NONE
<!-- 等价于 -->
<auth-constraint/>
````

````xml
emptyRoleSemantic=DENY, rolesAllowed={}, transportGuarantee=CONFIDENTIAL
<!-- 等价于 -->
<auth-constraint/>
<user-data-constraint>
    <transport-guarantee>CONFIDENTIAL</transport-guarantee>
</user-data-constraint>
````

### 13.4.2 ServletRegistration.Dynamic 的 setServletSecurity

````setServletSecurity````方法可以被用在````ServletContextListener````中，来定义将应用到由````ServletRegistration````定义的映射上的安全约束。

````java
Collection<String> setServletSecurity(ServletSecurityElement arg);
````

````javax.servlet.ServletSecurityElement````参数类似于在````@ServletSecurity````注解的````ServletSecurity````接口的构造器和模型中。这样一来，定义在 13.4.1.2 章节中的映射，类似应用于从包含````HttpConstraintElement````和````HttpMethodConstraintElement````值的````ServletSecurityElement````到等价的````security-constraint````表示形式的映射。

````setServletSecurity````方法返回（可能为空）可移植的部署描述器文件中的````security-constraint````元素的确切目标的URL 模式（因此不受调用的影响）。

此方法抛出````IllegalStateException````，如果从其中获取````ServletRegistration````的````ServletContext````已经被初始化。

当可移植部署描述器文件中的````security-constraint````包含的````url-pattern````是````ServletRegistration````映射到的模式的精确匹配，对````ServletRegistration````上的````setServletSecurity````方法的调用必须不影响容器强加到该模式上的约束。

除了上面列出的例外同时包括当 Servlet 类被注解为````@ServletSecurity````，当````ServletRegistration````上的````setServletSecurity````方法被调用时，它将建立应用于该注册的````url-pattern````上的安全约束。

## 13.5 角色

安全角色是一个由应用开发者或者装配者定义的用户的逻辑分组。当应用被部署后，角色将被部署者映射到运行环境中的负责人或者分组。

servlet 容器强制声明式或者编程式安全，基于负责人属性将负责人与进入的响应关联起来。可能会通过以下两种方式之一实现：

1. 在操作环境中部署者已经将一个安全角色映射到一个用户群组。该用户群组中的负责人发出的请求都会携带相应的安全属性。负责人属于该安全角色，仅当负责人属于该用户群组时。
2. 在一个安全策略域中部署者已经将一个安全角色映射到一个负责人姓名。这种情况下，负责人姓名就是他发出的请求携带的安全属性。该负责人属于该安全角色，仅当其姓名与安全角色映射到的姓名相同。

## 13.6 身份认证

一个 web 客户端可以认证一个用户使用以下一种机制：

* HTTP Basic Authentication
* HTTP Digest Authentication
* HTTPS Client Authentication
* Form Based Authentication

### 13.6.1 HTTP Basic Authentication

基本身份认证机制，基于用户名和密码，是 HTTP/1.0 规范中定义的身份认证机制。web 服务器请求 web 客户端认证用户。作为请求的一部分，web 服务器传递````realm````，其中的用户将要被认证。客户端从用户处获取用户名和密码并将它们传输给服务器。接下来服务器将在特定的````realm````中认证该用户。

这种认证机制并不是一种安全认证协议。用户的密码只是简单地经过 base64 编码之后就被发送，而且目标服务器也没有被认证。额外的保护措施可以减缓某些问题：安全传输机制 HTTPS 或者网络层面的安全性，类似于 IPSEC 协议或者 VPN 策略，被应用于某些部署场景。

### 13.6.2 HTTP Digest Authentication

类似于 Basic Authentication，HTTP Digest Authentication 认证用户也是基于用户名和密码。不过，不同的是，它并不会通过网络发送用户密码。这种认证机制中，客户端发送一个密码的单向加密的散列值，以及附加数据。尽管密码并没有通过网络发送，HTTP Digest 认证仍然需要完整的文本格式的密码等价可用于认证容器，因而它可以通过计算期望的摘要来验证接收认证器。Servlet 容器应该支持 HTTP_DIGEST 认证。

### 13.6.3 基于表单的身份认证

登录页面的观感不能使用浏览器内建的身份认证机制被改变。本规范介绍一种强制的基于表单的身份认证机制来允许开发者控制登录页面的观感。

web 应用部署描述器文件包含登录表单和错误页面的入口。登录表单必须包含可供输入用户名和密码的字段，相应的字段名必须是````j_username````和````j_password````。

当用户试图访问受保护的网络资源时，容器就会检查用户的身份认证信息。如果用户通过认证而且被授权访问该资源，则被请求的资源就是活动的，它的引用将被返回。如果用户没有通过认证，则下面的步骤将会发生：

1. 关联安全约束的登录表单被发送给客户端，URL 路径和触发身份认证的 HTTP 协议方法都被容器保存。
2. 用户被要求填写登录表单，包括用户名和密码。
3. 客户端将表单提交回服务端。
4. 容器尝试基于表单包含的信息认证用户身份。
5. 如果身份认证失败，请求就会转发或者重定向到错误页面，同时响应状态码被设定为 200。错误页面包含身份认证失败信息。
6. 如果身份认证成果，客户端请求被重定向到服务端保存的资源 URL 路径。
7. 当重定向请求和通过认证的请求到达容器，容器恢复请求和 HTTP 协议方法，同时检查用户信息以确认他是否属于可以访问该资源的已授权角色。
8. 如果用户已被授权，请求就会被容器接受并处理。

第 7 步中的重定向请求的 HTTP 协议方法，可能不同于触发身份认证的请求所用的协议方法。本质上，随着第 6 步中的重定向，表单认证器必须处理重定向请求，即使该请求使用的协议方法并不强制进行身份认证。为了提高重定向请求使用的 HTTP 协议方法的可预测性，容器应该使用 303(SC_SEE_OTHER) 状态码进行请求转发，除非通信对方是 HTTP 1.0 用户代理，这种情况下应该使用 302 状态码。

当通过未受保护的传输通道进行传输时，基于表单的身份认证具有与基本身份认证机制类似的缺陷。

当触发身份认证的请求通过安全传输通道传输，或者登录页面添加了````CONFIDENTIAL````的````user-data-constraint````，则登录页面必须通过安全传输通道发送给客户端，然后通过安全传输通道提交给服务端。

登录页面应该添加````CONFIDENTIAL````的````user-data-constraint````，同时，该安全约束应该被每个包含身份认证需求的````security-constraint````所包含。

````HttpServletRequest````接口的````login````方法提供了一种另外的含义，来允许应用控制它的登录页面的观感。

#### 13.6.3.1 登录表单

基于表单的登录和基于 URL 的会话追踪对实现来说是有问题的。基于表单的登录只应该被用于会话通过 cookies 或者 SSL 会话信息进行维护的场景。

为了确保认证过程正确无误，登录表单的动作必须永远都是````j_security_check````。这样一来，无论资源是否要求服务器指定外部表单的动作字段，登录表单都将工作。登录表单应该为密码表单字段指定属性````autocomplete="off"````。

下面是个登录表单的例子：

````html
<form method="POST" action="j_security_check">
    <input type="text" name="j_username">
    <input type="password" name="j_password" autocomplete="off">
</form>
````

如果因为一个 HTTP 请求而进行基于表单的登录，初始请求的参数必须被容器保留以供使用，如果身份认证成功，就将请求转发到被请求的资源。

如果使用表单登录的用户通过了身份认证并创建了会话，则该会话直到用户注销时才会超时实效，用户注销意味着后续的请求必须导致用户的重新身份认证。注销的作用域和身份认证时相同的：例如，如果容器支持单点登录，就像兼容 Java EE 技术的 web 容器，用户需要为所有驻留在该容器中的 web 应用进行身份重认证。

### 13.6.4 HTTPS Client Authentication

终端用户使用 HTTPS (SSL 上的 HTTP) 是一种很强的身份认证机制。这种机制需要客户端处理 Public Key Certificate (PKC)。目前，PKCs 在电商应用和浏览器中的单点登录中都非常有用。

### 13.6.5 附加的容器身份认证机制

Serlvet 容器应该提供公共接口用于集成和配置附加的 HTTP 消息层身份认证机制供给代表已部署的应用的容器使用。这些接口应该供包括容器提供商在内的其它团队使用（包括应用开发者、系统管理员以及系统集成商等）。

为了方便附加容器身份认证机制的移植实现和集成，推荐所有的 Servlet 容器都实现 Servlet 容器的 Java 身份认证 SPI（Service Provider Interface）（比如 JSR 196）。该 SPI 可以在如下位置下载：http://www.jcp.org/en/jsr/detail?id=196

## 13.7 身份认证信息的服务端跟踪

作为潜在的安全标识（比如用户和用户组）在运行环境中角色将映射其上，都是环境相关的，而不是应用相关的。我们期望它是：

1. 使登录机制和策略成为 web 应用部署环境的一个属性。
2. 能够使用相同的身份认证信息表示同一个容器中的所有应用的认证原则，同时，
3. 只有当安全策略边界被突破时才需要进行用户身份的重认证。

因此，Servlet 容器必须在容器层面（而不是在 web 应用层面）追踪身份认证信息。这就允许一个 web 应用的已认证用户访问容器管理的其它资源，只要该资源允许同一个安全标识访问。

## 13.8 指定安全约束

安全约束是一种指令式方式来定义的对 web 内容的保护策略。一个安全约束涉及到授权和/或用户数据关于 HTTP 对 web 资源操作的约束。一个安全约束，表现为部署描述器文件中的````security-constraint````，由以下元素组成：

* web 资源集合（部署描述器文件中的````web-resource-collection````）
* 授权约束（部署描述器文件中的````auth-constraint````）
* 用户数据约束（部署描述器文件中的````user-data-constraint````）

一个安全约束应用到的 HTTP 操作和 web 资源（比如，被限制的请求）被一个或者多个 web 资源集合标识。一个 web 资源集合由以下元素组成：

* URL 模式（部署描述器文件中的````url-pattern````）
* HTTP 方法（部署描述器文件中的````http-method````或者````http-method-omission````元素）

一个授权约束建立了一种强制性需求，要求执行受限制请求的用户进行身份认证和具有属于命名的授权角色的身份。一个用户必须是至少一个可执行受限制请求的命名角色的成员。特殊角色名为“\*”代表在部署描述器文件中定义的所有角色。特殊角色名“\*\*”表示所有已认证的用户，独立于角色。当特殊角色名“\*\*”出现在一个授权约束中时，表示所有认证用户，独立于角色，都被授权执行受限制的请求。一个无角色名的授权约束表示受限制的请求在任何情况下都不能被执行。一个授权约束由以下元素组成：

* 角色名（部署描述器文件中的````role-name````）

用户数据约束建立了一种强制约束，要求受限制的请求只能通过受保护的传输层连接被接收。要求的保护的强度由传输保证的值来定义。传输保证值````INTEGRAL````被用来建立一个内容完整性要求。传输保证值````CONFIDENTIAL````用于建立保密性的要求。传输保证值“NONE”表示容器必须接受受限制的请求，无论该请求是否来自受保护的连接。容器可以在响应中强行加入保密性传输保证值````INTEGRAL````。用户数据约束由下列元素组成：

* 传输保证（部署描述器文件中的````transport-guarantee````）

  如果没有授权约束施加到请求之上，容器必须在不对用户身份认证做任何要求的情况下接受请求。如果没有用户数据约束施加到请求之上，容器必须接受来自受保护和不受保护的连接的请求。

### 13.8.1 组合约束

为了将约束组合起来，一个 HTTP 方法被称为是在一个````web-resource-collection````中发生，当在该集合中没有命名任何 HTTP 方法，或者该集合特定的 HTTP 方法名称在一个包含的````http-method````元素中，或者该集合包含一个或者多个````http-method-omission````元素，其中没有一个命名了 HTTP 方法。

当一个 url-pattern 和 HTTP 方法对发生在组合中（比如，在````web-resource-collection````内部），在多个安全约束中，约束（施加在 pattern 和方法上的）通过组合各个单独的约束来定义。当出现相同的 pattern 和方法时，约束组合的规则如下：

命名角色或者通过名称“\*”暗示的角色授权约束的组合应该实现以各个单独约束的角色名称的并集作为最终的许可角色。一个命名角色"\*"的授权约束应该与命名或者暗示角色的授权约束相组合，以许可任何已认证的用户，而不考虑角色。不包含授权约束的安全约束应该与命名或者暗示角色的授权约束组合，以许可未认证访问。特殊情况，没有命名角色的授权约束应该与任何其它约束组合，用来覆盖它们的影响和导致的访问阻碍。

应用于普通````url-pattern````和````http-method````的````user-data-constraints````的组合应该得到各个单独的约束许可的连接类型的并集作为可接受连接类型。不包含````user-data-constraint````的安全约束应该与其它````user-data-constraint````组合来使得未受保护的连接类型成为可接受的连接类型。

### 13.8.2 例子

下面的例子展示了约束组合的情形以及它们组合之后实现的可应用约束。假定部署描述器文件中包含下列安全约束：

````xml
<security-constraint>
    <web-resource-collection>
        <web-resource-name>precluded methods</web-resource-name>
        <url-pattern>/*</url-pattern>
        <url-pattern>/acme/wholesale/*</url-pattern>
        <url-pattern>/acme/retail/*</url-pattern>
     	<http-method-omission>GET</http-method-omission>
     	<http-method-omission>POST</http-method-omission>
    </web-resource-collection>
    
    <auth-constraint/>
    
</security-constraint>

<security-constraint>
	<web-resource-collection>
		<web-resource-name>wholesale</web-resource-name>
     	<url-pattern>/acme/wholesale/*</url-pattern>
     	<http-method>GET</http-method>
     	<http-method>PUT</http-method>
    </web-resource-collection>
    <auth-constraint>
     	<role-name>SALESCLERK</role-name>
    </auth-constraint>
</security-constraint>

<security-constraint>
	<web-resource-collection>
     	<web-resource-name>wholesale 2</web-resource-name>
     	<url-pattern>/acme/wholesale/*</url-pattern>
     	<http-method>GET</http-method>
     	<http-method>POST</http-method>
    </web-resource-collection>
    <auth-constraint>
     	<role-name>CONTRACTOR</role-name>
    </auth-constraint>
    <user-data-constraint>
     	<transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
</security-constraint>

<security-constraint>
	<web-resource-collection>
     	<web-resource-name>retail</web-resource-name>
     	<url-pattern>/acme/retail/*</url-pattern>
     	<http-method>GET</http-method>
     	<http-method>POST</http-method>
    </web-resource-collection>
    <auth-constraint>
     	<role-name>CONTRACTOR</role-name>
     	<role-name>HOMEOWNER</role-name>
    </auth-constraint>
</security-constraint>
````

这个假想的部署描述器翻译之后得到的约束定义如下表所示：

| url-pattern       | http-method                  | permitted roles       | supported connection types |
| ----------------- | ---------------------------- | --------------------- | -------------------------- |
| /*                | all methods except GET, POST | 访问阻止                  | 无限制                        |
| /acme/wholesale/* | all methods except GET, POST | 访问阻止                  | 无限制                        |
| /acme/wholesale/* | GET                          | CONTRACTOR SALESCLERK | 无限制                        |
| /acme/wholesale/* | POST                         | CONTRACTOR            | CONFIDENTIAL               |
| /acme/retail/*    | all methods except GET, POST | 访问阻止                  | 无限制                        |
| /acme/retail/*    | GET                          | CONTRACTOR HOMEOWNER  | 无限制                        |
| /acme/retail/*    | POST                         | CONTRACTOR HOMEOWNER  | 无限制                        |

### 13.8.3 请求处理

当 Servlet 容器接收到请求时，它应该使用“URL 路径的使用”中描述的算法来选择请求 URI 最佳匹配的 url-pattern 上定义的约束（如果存在的话）。如果没有选择到约束，容器就应该接受该请求。否则，容器应该确定请求的 HTTP 方法在选定的模式上是受限制的。如果不是，则该请求应该被接受。否则，该请求必须满足 url-pattern 上应用于该 HTTP 方法的约束。可以被接受并可以被分发给相关 servlet 的请求必须满足以下规则：

1. 接收到请求的连接的特性必须满足约束定义的它所支持的连接类型中的至少一个。如果不满足这条规则，容器应该拒绝该请求并将其转发到 HTTPS 端口。
2. 请求的身份认证特性必须满足约束定义的任何认证和角色要求。如果此规则不满足，访问就会被阻止（被没有命名角色的身份认证约束阻止），该请求应该作为 forbidden 被拒绝，同时，一个 403（SC_FORBIDDEN）状态码响应应该被返回给用户。如果访问被限制为许可角色，而请求尚未经过身份认证，则该请求应该作为未授权而被拒绝，同时返回 401（SC_UNAUTHORIZED）状态码响应应该被返回以触发后续的身份认证。如果访问被限制为许可角色，而其身份认证标识并不是这些许可角色的成员，该请求就应该作为 forbidden 而被拒绝，同时 403（SC_FORBIDDEN）状态码响应应该被返回给用户。

### 13.8.4 未覆盖的 HTTP 协议方法

````security-constraint````模式提供了列举出（包含遗漏的）在````security-constraint````中定义的保护需要被应用到的 HTTP 协议方法。当 HTTP 方法被列举在一个````security-constraint````内部，该约束定义的保护机制就只会应用于该列表中的方法。我们所说的 HTTP 方法不是由所谓“未覆盖” HTTP 方法列表定义的。未覆盖的 HTTP 方法在所有请求 URL 上都是不受保护的，对那些 URL 来说，````url-pattern````和````security-constraint````是最佳匹配。

当 HTTP 方法没有在````security-constraint````中被列出，则由该约束定义的保护机制就会施加到所有 HTTP（扩展）方法上。这种情况下，作为````security-constraint````最佳匹配的````url-pattern````上的所有请求 URL 都没有未覆盖的 HTTP 方法。

下面的例子展示了 HTTP 协议被作为未覆盖的三种方式。方法是否为非覆盖的方法的决定是在所有应用于该````url-pattern````的约束都按照 13.8.1 章节中描述的规则组合完成之后才做出的。

1. 一个````security-constraint````在````http-method````元素中命名一个或者多个 HTTP 方法。所有其它 HTTP 方法就都是未覆盖的。

   ````xml
   <security-constraint>
   	<web-resource-collection>
    		<web-resource-name>wholesale</web-resource-name>
    		<url-pattern>/acme/wholesale/*</url-pattern>
    		<http-method>GET</http-method>
   	</web-resource-collection>
   	<auth-constraint>
    		<role-name>SALESCLERK</role-name>
   	</auth-constraint>
   </security-constraint>
   ````

   除了````GET````之外所有的 HTTP 方法都是未覆盖的。

2. 一个````security-constraint````在````http-method-omission````元素中命名一个或者多个 HTTP 方法。则所有命名的 HTTP 方法就都是未覆盖的。

   ````xml
   <security-constraint>
   	<web-resource-collection>
    		<web-resource-name>wholesale</web-resource-name>
    		<url-pattern>/acme/wholesale/*</url-pattern>
    		<http-method-omission>GET</http-method-omission>
   	</web-resource-collection>
   	<auth-constraint/>
   </security-constraint>
   ````

   ````GET````方法是未覆盖的。所有其它方法都被排除的````auth-constraint````覆盖。

3. 包含````@HttpConstraint````的````@ServletSecurity````注解返回所有默认值，同时它包含至少一个````@HttpMethodConstraint````返回所有默认值之外的值。所有不在````@HttpMethodConstraint````中命名的 HTTP 方法都被该注解标识为未覆盖的。类似于第一种情况，等效于使用````ServletRegistration````接口的````setServletSecurity````方法，将产生类似的结果。

   ````java
   @ServletSecurity((httpMethodConstraints = {
    @HttpMethodConstraint(value = "GET", rolesAllowed = "R1"),
    @HttpMethodConstraint(value = "POST", rolesAllowed = "R1",
    transportGuarantee = TransportGuarantee.CONFIDENTIAL)
    })
   public class Example5 extends HttpServlet {
   }
   ````

   除了````GET````、````POST````之外所有的 HTTP 方法都是未覆盖的。

#### 13.8.4.1 安全约束配置规则

目标：确保受约束的 URL 模式上的所有的 HTTP 方法都受到希望的安全保护（也就是说，被安全约束覆盖）。

1. 不在约束中命名 HTTP 方法：这种情况下，为 URL 模式定义的安全保护将施加到所有 HTTP 方法上。
2. 如果你不能遵循规则1，添加````<deny-uncovered-http-method>````同时声明（使用````<http-method>````元素，或者别的等价的注解）受约束的 URL 模式上将要允许的所有 HTTP 方法（收到安全保护）。
3. 如果你不能遵循规则2，则在每个受约束的 URL 模式上声明约束来覆盖所有 HTTP 方法。使用````<http-method-omission>````元素或者````HttpMethodConstraint````注解来表示除了由````<http-method>````或者````HttpMethodConstraint````命名的之外的所有 HTTP 方法。使用注解时，使用````HttpConstraint````注解定义将要施加到所有其它 HTTP 方法上的安全语义，同时配置````EmptyRoleSemantic=DENY````来确保所有其它 HTTP 方法都被拒绝。

#### 13.8.4.2 处理未覆盖的 HTTP 方法

在应用部署过程中，容器必须通知部署者来自为应用定义的约束的组合的安全约束配置中存在未覆盖的 HTTP 方法。给出的信息必须指出该未覆盖的 HTTP 协议方法，以及被覆盖的 HTTP 方法所对应的 URL 模式。这种通知可以通过将需要的信息作为日志打印出来实现。

当应用的````web.xml````文件中设定了````deny-uncovered-http-methods````标志，容器必须拒绝任何 HTTP 协议方法，当它使用请求 URL 对应的最佳匹配 url-pattern 上施加的安全约束覆盖了该请求的 HTTP 方法。被拒绝的请求应该被作为 forbidden 而被拒绝，同时返回 403（SC_FORBIDDEN）状态码响应。

为了实现未覆盖的 HTTP 方法的拒绝，部署系统应该建立附加的排除 auth-constraints，为了覆盖受约束的 url-pattern 上未覆盖的 HTTP 方法。

当一个应用的安全配置不包含未覆盖的方法，````deny-uncovered-http-methods````标志就必须不影响最终生效的应用的安全配置。

将````deny-uncovered-http-methods````标志应用于安全配置包含未覆盖方法的应用时，可以，某些情况下，拒绝必须为应用程序执行的资源访问。这种情况下，应用的安全配置应该完整，这样所有未覆盖的方法就都被适当的约束配置覆盖。

应用开发者应该定义安全约束配置，不遗留任何 HTTP 方法，同时他们应该设置````deny-uncovered-http-methods````标志以确保他们的应用不会依赖于通过未覆盖的 HTTP 方法进行的资源访问。

Servlet 容器可以提供一个配置选项来选择是否允许或者拒绝未覆盖方法的默认行为。这个选项可以被配置在应用粒度或者更大粒度。注意，该选项的默认值````DENY````可能导致某些应用失败。

## 13.9 默认策略

默认的，访问资源并不需要身份认证。身份认证只有当包含最匹配请求 URI  的````url-pattern````的安全约束联合施加一个````auth-constraint````（命名角色）到请求的 HTTP 方法上之时才是需要的。类似的，受保护的传输通常也不是必需的，除非应用于请求的安全约束联合施加一个````user-data-constraint````(伴随一个受保护的````transport-guarantee````)于请求的 HTTP 方法之上。

## 13.10 登录和注销

容器会在讲请求分发给 servlet 引擎之前建立请求调用者的身份标识。该调用者身份标识将在整个请求处理过程中保持不变，或者直到应用在请求上成功地调用了````authenticate````,````login````或者````logout````。对异步请求来说，调用者身份标识在初始分发时建立，保持不变直到请求彻底处理完成或者应用在请求上成功地调用了````authenticate````,````login````或者````logout````。

在请求处理过程中登录进入一个应用，精确地意味着请求包含一个合法的非空调用者身份标识，该标识可以通过调用请求上的````getRemoteUser````或者````getUserPrincipal````来确定。这两个方法任何一个返回````null````值都表示调用者在请求处理过程中尚未登录进入应用。

容器可以创建 HTTP Session 对象来跟踪登录状态。如果开发者在用户尚未认证时创建会话，然后容器认证该用户，则登录之后对开发者代码可见的会话对吸纳高必须就是在登录之前创建的那个，这样才能保证会话信息不丢失。

----

# 部署描述器

----

本章节详述 Java Servlet 规范必需的 Web 容器对部署描述器的支持。部署描述器在应用开发者、应用装配者和部署者之间传递 Web 应用的元素和配置信息。

对于 Java Servlet v2.4 以及更高版本，部署描述器文件定义为一个 XML 概要文件。

为了保持向下兼容性，任何按照更早版本规范编写的部署描述器文件必须在当前版本规范中仍然可用。实际的 XSD 文件参见````<http://xmlns.jcp.org/xml/ns/javaee/>````。

## 14.1 部署描述器元素

所有 servlet 容器中 Web 应用的部署描述器都必须支持以下类型的配置和部署信息：

* ````ServletContext````初始化参数
* 会话配置
* Servlet 声明
* Servlet 映射
* 应用生命周期监听器类
* 过滤器定义和过滤器映射
* MIME 类型映射
* 欢迎页面列表
* 错误页面
* 位置和编码映射
* 安全配置，包含登录配置、安全约束、拒绝未覆盖的方法、安全角色、安全角色引用以及运行为

## 14.2 部署描述器处理规则

本节列出了一些容器和开发者处理应用的部署描述器时必须遵循的通用规则。

* Web 容器必须为部署描述器中元素内容文本节点删除所有的首尾空白字符，空白字符在 XML 1.0 中定义(````http://www.w3.org/TR/2000/WD-xml-2e-20000814````)。

* 部署描述器必须符合相应规范。处理 Web 应用的容器和工具拥有很宽泛的选项来检查 WAR 包的合法性。包含检查包含在其中的部署描述器文件的合法性。

  另外，推荐的做法是，处理 Web 应用的容器和工具应该提供某种水平的语义校验。比如，应该校验一个安全约束中的角色引用在部署描述器文件中是否存在一个同名的安全角色定义。

  对于不合乎规范的 Web 应用，容器和工具应该以描述性的错误信息通知开发者。高端应用服务器供应商被鼓励提供这种独立于容器的工具形式的合法性校验机制。

* ````web-app````的子元素在本规范中可以是任意顺序的。由于 XML 规范的约束，````distributable````、````session-config````、````welcome-file-list````、````jsp-config````、````login-config````以及````locale-encoding-mapping-list````等元素的多样性从 "可选择的" 变化为 “0或者更多”。当部署描述器中包含多于一个````session-config````、````jsp-config````或者````login-config````元素，容器必须以描述性的错误信息通知开发者。容器必须将````welcome-file-list````和````locale-encoding-mapping-list````中的元素联系起来，如果它们出现了多次。多次出现的````distributable````必须被像它只出现一次时同样处理。

* 部署描述器文件中指定的 URI 路径被假定为 URL-解码 形式。当 URL 包含````CR(#xD)````或者````LF(#xA)````时，容器必须以描述性的错误信息通知开发者。容器必须允许包括空格在内的所有其它字符出现在 URL 中。

* 容器必须尝试规范化部署描述器中的路径。例如，形如````/a/../b````的路径必须被翻译成为````/b.````。部署描述器中以````../````开头或者被解析后以````../````开头的路径都是非法的。

*  指向相对于 WAR 包的根路径的资源的URI 路径，或者映射相对于 WAR 包根路径的路径，除非特殊说明，应该都以````/.````开头。

* 值为枚举类型的元素，其值是大小写敏感的。

## 14.3 部署描述器

此修订版规范的部署描述器文件参见````http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd````。

## 14.4 部署描述器图示

本章节举例说明部署描述器元素。图表中没有展示属性。参考部署描述器规范以获取更多细节。

1. ````web-app````元素

   此元素是 Web 应用部署描述器文件的根元素。此元素包含接下来介绍的元素。此元素包含一个必需属性````version````，用来指定部署描述器文件遵循的规范版本。此元素的所有子元素可以任意顺序出现。

   ![web-app 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181231192603885-6255564.png)

2. ````description````元素

   此元素用于提供一个对父元素的文本描述。此元素不仅可以出现在````web-app````元素下，还可以出现在其它元素下。它包含一个可选的属性````xml:lang````用于表示该描述使用何种语言。该属性的默认值是英语````en````。

3. ````display-name````元素

   此元素包含一个简短的名称供工具显示。此显示名称不需要保证唯一性。此元素包含一个可选属性````xml:lang````用于指定语言。

4. ````icon````元素

   此元素包含小按钮和大按钮元素，为小按钮指定文件名，为大按钮指定图片文件。此元素由 GUI 工具用于表示父元素。

5. ````distributable````元素

   此元素表示该 Web 应用被实现为可以部署到分布式的 servlet 容器中。

6. ````context-param````元素

   此元素包含应用的 servlet 上下文初始化参数声明。

7. ````filter````元素

   过滤器元素在应用中声明一个过滤器。在````filter-mapping````元素中使用引用的````filter-name````值该过滤器被映射到一个 servlet 或者一个 URL 模式。过滤器能够访问运行时在部署描述器文件中通过````FilterConfig````接口声明的初始化参数。````filter-name```` 元素是过滤器的逻辑名称。在 Web 应用中过滤器名称必须是唯一的。````filter-name````元素内容必须非空。````filter-class````是过滤器对应类型的全限定类型名称。````init-param````元素包含过滤器初始化参数名值对。可选的````async-supported````元素，如果被指定，则表示该过滤器支持异步请求处理。

   ![filter 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181231200742979-6258063.png)

8. ````filter-mapping````元素

   此元素被容器用于决定哪些过滤器将以何种顺序被应用于请求。````filter-name````的值必须是部署描述器文件中声明的一个过滤器。匹配到的请求可以被通过````url-pattern````或者````servlet-name````指定。

   ![filter-mapping 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181231201652480-6258612.png)

9. ````listener````元素

   此元素表示一个应用监听器 bean 的部署属性。子元素````listener-class````声明一个类必须被注册成为一个 Web 应用监听器 bean 。其值时该监听器类的全限定类名。

   ![listener 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181231202058729-6258858.png)

10. servlet元素

  此元素用于声明一个 servlet 。它包含 servlet 需要声明的数据。jsp-file元素包含应用中的 JSP 文件的完整路径，以/开头。如果一个jsp-file元素中指定了load-on-startup元素，则该 JSP 文件应该被预编译并加载。servlet-name元素包含了 servlet 的权威名称。应用中的每个 servlet 名称必须是唯一的。servlet-name元素内容必须非空。servlet-class元素包含 servlet 的全限定类名。run-as元素指定了组件执行时所用的 id 。它包含可选的description元素，以及由role-name元素指定的安全角色名称。load-on-startup表示该 servlet 在应用启动时就应该被实例化，并且其init()方法被调用。该元素内容必须时一个整数，表示该 servlet 被加载的顺序。如果该值是一个复数，或者没有该原色，容器就能够以任意顺序加载该 servlet 。如果该值是正数或者0，则容器必须在应用被部署时加载并初始化该 servlet 。容器必须保证按照指定的加载顺序号由小到大依次加载 servlet 。容器可以按照load-on-startup的值确定 servlet 的顺序。security-role-ref元素声明在组件或者部署组件的代码中的安全角色引用。它包含一个可选的description，安全角色名称role-name用在这里，同时，还有一个可选指向安全角色的的链接role-link。如果没有指定安全角色，部署者必须选择一个合适的安全角色。可选的````async-supported````元素，当它被指定时，表示 Servlet 可以支持异步请求处理。如果 servlet 支持文件上传功能和````mime-multipart````请求处理，可以通过部署描述器文件中的````multipart-config````元素来提供。该元素可以用来指定文件的存储位置、上传文件的最大尺寸、最大请求尺寸以及超过哪个阈值之后文件将会被写入磁盘。

  ![servlet 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105002917443-6619357.png)

11. ````servlet-mapping````元素

   本元素定义了一个 servlet 到一个 URL 模式的映射。

   ![servlet-mapping 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105002803410-6619283.png)

12. ````session-config````元素

   本元素为所在的 Web 应用定义会话参数。子元素````session-timeout````为所在应用中创建的所有会话定义默认超时时间。指定的超时时间必须表示为整数分钟数。如果超时时间是0或者更小，则容器需要保证会话的默认行为是永不超时。如果此元素没有指定，则容器必须自己设置默认超时时间。

   ![session-config 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105002707549-6619227.png)

13. ````mime-mapping````元素

    此元素定义了一个扩展到一种 mime 类型的映射。````extension````元素包含了一个扩展的文字描述，比如````txt````。

    ![mime-mapping 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105121714838-6661835.png)

14. ````welcome-file-list````元素

    此元素包含一个欢迎文件的有序列表。````welcome-file````子元素包含了作为默认欢迎文件的文件名。比如````index.html````。

    ![welcome-file-list 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105121946316-6661986.png)

15. ````error-page````元素

    此元素包含一个错误码或者一种异常类型到应用中相应资源的映射。不过，````error-code````或者````exception-type````元素在指定默认错误页面时可以忽略。````exception-type````子元素包含一个 java 异常类型的全限定类名。````location````子元素包含相应资源相对于应用根路径的位置。该位置的取值必须以````/````开头。

    ![error-page 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105123059980-6662660.png)

16. ````jsp-config````元素

    此元素用于为应用中的 JSP 文件提供全局配置信息。它包含两个字元素，````taglib````和````jsp-property-group````。````taglib````元素可以被用于为应用中的 JSP 页面使用的标签库提供信息。更多详情参见 JSP v2.1 规范。

    ![jsp-config 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105125027480-6663827.png)

17. ````security-constraint````元素

    此元素用于将一个或者多个 web 资源集合与安全约束关联起来。子元素````web-resource-collection````标识安全约束将被应用到的该应用中一个资源子集和作用于那些资源的 HTTP 方法。````auth-constraint````元素表示被许可访问此资源集合的用户角色。这里使用的````role-name````必须要么对应于为此应用定义的某个````security-role````元素的````role-name````，要么是特殊的保留角色名````*````用来表示应用中的所有角色。如果````*````和角色名称都出现，则容器就认为是所有角色。如果没有定义角色，所有用户都不被允许访问````security-constraint````元素描述的资源。容器在确定访问权限时对角色名进行大小写敏感的匹配。````user-data-constraint````表示当数据在客户端和容器之间传输时应该被子元素````transport-guarantee````如何保护。````transport-guarantee````元素的合法取值是````NONE````,````INTEGRAL````,````CONFIDENTIAL````其中之一。

    ![security-constraint 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105205640658-6693000.png)

18. ````deny-uncovered-http-methods````元素

    此元素用于表示容器尚未覆盖的 http 方法是否会被拒绝。对每个目标是 security-constraint 的 url-pattern ，此元素导致所有指向该 url-pattern 的未被（security-constraint）覆盖 HTTP 方法被拒绝。

19. ````login-config````元素

    此元素用来配置应该使用的身份认证方法，该应用使用的领域名称，表单登陆机制需要使用的属性。子元素````auth-method````配置应用使用的身份认证机制。该元素内容必须是````BASIC````,````DIGEST````,````FORM````,````CLIENT-CERT````或者容器提供商特定的认证机制。````realm-name````表示用于为应用选择的认证机制的领域名称。````form-login-config````指定用于表单登录的登录和错误页面。如果使用的不是表单登录，则该元素会被忽略。

    ![login-config 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105213145133-6695105.png)

20. ````security-role````元素

    此元素定义一个安全角色。其子元素````role-name````指明该安全角色的名字。该名字必须遵循````NMTOKEN````的词汇规则。

    ![security-role 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190105215013871-6696214.png)

21. ````env-entry````元素

    此元素声明一个应用的环境入口。子元素````env-entry-name````包含一个部署组件的环境入口的名称。JNDI 名称都是相对于````java:comp/env````上下文的。该名称在一个部署组件中必须是唯一的。````env-entry-type````包含应用代码所期待的环境入口值的完全限定的 Java 类型。子元素````env-entry-value````指明部署组件的环境入口的值。该值必须是````String````类型，可用于指定类型的只有一个字符串类型参数的构造器，或者只是一个单独的字符，类型是````java.lang.Character````。可选的````injection-target````元素被用于定义被命名的资源向字段或者 JavaBeans 属性的注射。````injection-target````指定资源应该被注入其中的一个类和它的名字。````injection-target-class````指定资源注射目标的全限定类名。````injection-target-name````指定在指定类中的目标。该目标首先作为 JavaBean 属性名被查找。如果没有找到，就以字段名被查找。初始化类过程中通过调用目标属性的 set 方法或者为该名称字段赋值，指定的资源将被注射进入目标。如果环境入口的````injection-target````被指定，则````env-entry-type````可以被忽略，否则必须匹配到注射目标类型。如果没有指定````injection-target````，则````env-entry-type````就是必需的。

    ![env-entry 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190107224920567-6872560.png)

22. ````ejb-ref````元素

    此元素声明一个企业级 bean 的 home 引用。````ejb-ref-name````指定用在部署组件代码中的名称，该名称引用的就是该企业级 bean 。````ejb-ref-type````是被引用的 bean 的类型，是````Entity````或者````Session````。````home````定义被引用的 bean 的 home 接口的全限定名。````remote````定义被引用的 bean 的 remote 接口的全限定名。````ejb-link````指定一个 EJB 引用链接到该 bean 。除了这些元素，````injection-target````元素可被用于定义命名的企业级 bean 向组件字段或者属性的注射。

    ![ejb-ref 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190107225037008-6872637.png)

23. ````ejb-local-ref````元素

    此元素声明企业级 JAVA Bean 的本地路径引用。````local-home````定义了企业级 JAVA Bean 的本地路径接口的全限定名。````local````定义了企业级 JAVA Bean 的本地接口的全限定名。

    ![ejb-local-ref 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110201628236-7122588.png)

24. ````service-ref````元素

    此元素声明 Web service 的引用。````service-ref-name````声明模块内用于寻找 Web service 的组件的逻辑名称。推荐的做法是所有的服务引用名由````/service/````开头。````service-interface````定义客户端依赖的 JAX-WS Service 接口的全限定名。大多数情况下，该值将是````javax.xml.rpc.Service````。JAX-WS 生成的服务接口类可以同时被指定。````wsdl-file````元素包含一个 WSDL 文件的 URI 地址。该地址是相对于模块根目录的相对路径。````jaxrpc-mapping-file````包含描述该应用使用的 Java 接口与````wsdl-file````中描述的 WSDL 之间的 JAX-WS 映射关系文件的名称。该文件名是模块文件中的一个相对路径。````service-qname````元素声明被提及的特定 WSDL 服务元素。没有声明````wsdl-file````则不需要指定。````port-component-ref````元素声明一个将 Service Endpoint Interface 解析成 WSDL 端口的容器的客户端依赖。将 Service Endpoint Interface 关联到特定的端口组件是可选的。这个只是用于容器调用````Service.getPort(Class)````方法时。````handler````元素声明一个端口组件的处理器。处理器可以通过````HandlerInfo````接口访问````init-param````名值对。如果````port-name````没有指定，处理器久假定关联到所有服务端口。更过细节详见 JSR-109 规范````http://www.jcp.org/en/jsr/detail?id=109````。不作为 Java EE 规范实现一部分的那些容器不需要支持此元素。

    ![service-ref 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110204216880-7124137.png)

25. ````resource-ref````元素

    此元素包含部署组件对外部资源的引用声明。````res-ref-name````指定资源管理器连接工厂引用名称。相对于````java:comp/env````上下文的是一个 JNDI 名称。该名称在部署文件中必须是唯一的。````res-type````元素指定数据源的类型。该类型是数据源需要实现的全限定 Java 类或者接口的类型。````res-auth````指定是否部署组件代码是否负责资源管理，或者是否容器将代表部署组件负责资源管理。在后一种情况下，容器将使用部署者提供的信息。````res-sharing-scope````指定是否通过给定的资源管理器连接工厂引用获取的连接可以被共享。该值，如果被指定，必须要么是````Shareable````要么是````Unshareable````。可选的````injection-target````元素用于定义命名资源向字段或者 JavaBeans 属性的注射。

    ![resource-ref 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110210147505-7125307.png)

26. ````resource-env-ref````元素

    此元素包含部署组件中与部署组件环境中的资源相关联的管理对象的引用。````resource-env-ref````元素指定资源环境引用的名称。该值是部署组件代码中使用的环境入口名称，相对于````java:comp/env````上下文的是一个 JNDI 名称，该值在部署组件中必须是唯一的。````resource-env-ref-type````指定资源环境引用的类型。它是 Java 语言中类或者接口的全限定名。可选的````injection-target````元素用于定义命名资源向字段或者 JavaBeans 属性的注射。````resource-env-ref-type````必须被指定，除非当目标类型被使用时指定了注射目标。如果两个都被指定，该类型就必须与注射目标相兼容。

    ![resource-env-ref 元素接口](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110211239791-7125960.png)

27. ````message-destination-ref````元素

    此元素包含一个部署组件的消息目的地引用的声明，该消息目的地关联于部署组件环境中的资源。````message-destination-ref-name````元素指定消息目的地引用的名称，其值时部署组件代码使用的环境入口的名称。相对于````java:comp/env````上下文的是一个 JNDI 名称，在企业级 beans 或者部署文件的 ejb-jar 文件中该值必须是唯一的。````message-destination-type````指定该目的地的类型。该类型由目的地需要实现的接口的类型决定。````message-destination-usage````指定该引用说明的消息目的地的使用。该值表示是否消息来自消息目的地、向目的地发送。装配器利用这些与消息生产者关联的信息将它与消费者联系起来。````message-destination-link````关联一个消息目的地引用或者关于消息目的地的消息驱动的 bean 。装配器设置该值以反映应用中的消息生产者和消费者之间的消息流。该值必须是在同一个部署文件中消息目的地的````message-destination-name````，或者是同一个 Java EE 应用单元的其它部署文件中。或者，该值可以由一个路径名称组成，该路径指定一个部署文件，包含被````message-destination-name````引用的消息目的地，它与该路径名通过````#````连接或者分隔。该路径名相对于包含引用该消息目的地的部署组件的部署文件。这就允许多个同名的消息目的地可以有各自的唯一标识符。可选的````injection-target````元素用于定义命名资源向字段或者 JavaBeans 属性的注射。该消息目的地类型必须指定，除非注射目标被指定，如果目标类型被使用。如果两者都被指定，则该类型必须与注射目标相兼容。

    ````xml
    <message-destination-ref>
        <message-destination-ref-name>
            jms/StockQueue
        </message-destination-ref-name>
        <message-destination-type>
            javax.jms.Queue
        </message-destination-type>
        <message-destination-usage>
            Consumes
        </message-destination-usage>
        <message-destination-link>
            CorporateStocks
        </message-destination-link>
    </message-destination-ref>
    ````

    ![message-destination-ref 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110214836290-7128116.png)

28. ````message-destination````元素

    此元素指定一个消息目的地。此元素描述的逻辑目的地被部署者映射到一个物理目的地。````message-destination-name````元素指定消息目的地的名称。该名称在部署文件中的所有消息目的地名称中必须是唯一的。

    ````xml
    <message-destination>
        <message-destination-name>
            CorporateStocks
        </message-destination-name>
    </message-destination>
    ````

    ![message-destination 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110215428595-7128468.png)

29. ````locale-encoding-mapping-list````元素

    此元素包含区域和编码之间的映射关系，由子元素````locale-encoding-mapping````指定。

    ````xml
    <locale-encoding-mapping-list>
        <locale-encoding-mapping>
            <locale>ja</locale>
            <encoding>Shift_JIS</encoding>
        </locale-encoding-mapping>
    </locale-encoding-mapping-list>
    ````

    ![locale-encoding-mapping-list 元素结构](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20190110220336807-7129016.png)

30. ````default-context-path````元素

    此元素提供了一个 web 应用的默认上下文路径。此元素的空值必须导致 web 应用被部署到容器的根目录下。否则，默认上下文路径必须以````/````开头但是不能以````/````结尾。Servlet 容器提供者可以提供的配置选项允许指定一个值用于覆盖此处指定的值。

31. ````request-character-encoding````元素

    此元素提供一个应用的默认请求字符编码方式。

32. ````response-character-encoding````元素

    此元素提供一个应用的默认响应字符编码方式。

## 14.5 例子

以下是部署描述器文件中的定义的使用举例。

### 14.5.1 一个基本例子

````xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee web-app_4_0.xsd"
         version="4.0">
    <display-name>A Simple Application</display-name>
    <context-param>
        <param-name>Webmaster</param-name>
        <param-value>webmaster@example.com</param-value>
    </context-param>
    <servlet>
        <servlet-name>catalog</servlet-name>
        <servlet-class>com.example.CatalogServlet</servlet-class>
        <init-param>
            <param-name>catalog</param-name>
            <param-value>Spring</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>catalog</servlet-name>
        <url-pattern>/catalog/*</url-pattern>
    </servlet-mapping>
    <session-config>
        <session-timeout>30</session-timeout>
    </session-config>
    <mime-mapping>
        <extension>pdf</extension>
        <mime-type>application/pdf</mime-type>
    </mime-mapping>
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
    </welcome-file-list>
    <error-page>
        <error-code>404</error-code>
        <location>/404.html</location>
    </error-page>
</web-app>
````

### 14.5.2 一个安全的例子

````xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee web-app_4_0.xsd"
         version="4.0">
    <display-name>A Secure Application</display-name>
    <servlet>
        <servlet-name>catalog</servlet-name>
        <servlet-class>com.example.CatalogServlet</servlet-class>
        <init-param>
            <param-name>catalog</param-name>
            <param-value>Spring</param-value>
        </init-param>
        <security-role-ref>
            <role-name>MGR</role-name>
            <!-- role name used in code -->
            <role-link>manager</role-link>
        </security-role-ref>
    </servlet>
    <security-role>
        <role-name>manager</role-name>
    </security-role>
    <servlet-mapping>
        <servlet-name>catalog</servlet-name>
        <url-pattern>/catalog/*</url-pattern>
    </servlet-mapping>
    <security-constraint>
        <web-resource-collection>
            <web-resource-name>SalesInfo</web-resource-name>
            <url-pattern>/salesinfo/*</url-pattern>
            <http-method>GET</http-method>
            <http-method>POST</http-method>
        </web-resource-collection>
        <auth-constraint>
            <role-name>manager</role-name>
        </auth-constraint>
        <user-data-constraint>
            <transport-guarantee>CONFIDENTIAL</transport-guarantee>
        </user-data-constraint>
    </security-constraint>
</web-app>
````

----

# 与其它规范相关的需求

----

本章列出包含在同时包含其它 Java 技术的完整产品中的 web 容器的需求。

下面章节中提到的 Java EE 指的不仅仅是完整的 Java EE 平台规范，同时还包括任何包含 Servlet 支持的其它任何技术规范，比如 Java EE Web 规范。有关规范的更多信息参见 Java EE 平台规范文档。

## 15.1 会话

分布式 servlet 容器作为 Java EE 实现的一部分，必须支持必要的机制来保证可以在不同 JVM 之间迁移其它 Java EE 对象。

## 15.2 Web 应用

### 15.2.1 Web 应用类加载器

作为 Java EE 产品一部分的 Servlet 容器不应该允许应用覆盖 Java SE 或者 Java EE 平台类，比如那些````java.*````和````javax.*````命名空间中的类，那些在 Java SE 或者 Java EE 不允许被修改的内容。

### 15.2.2 Web 应用环境

 Java EE 定义一个命名环境来允许应用很容易地访问资源和外部信息，而不需要关于外部信息的命名或者组织的显式信息。

因为 servlets 是一种 Java EE 技术的集成组件类型，部署描述器文件中已经提供了规则来给出信息来允许 servlet 获取资源和企业级 beans 应用。包含这些信息的部署描述元素有：

* ````env-entry````
* ````ejb-ref````
* ````ejb-local-ref````
* ````resource-ref````
* ````resource-env-ref````
* ````service-ref````
* ````message-destination-ref````
* ````persistence-context-ref````
* ````persistence-unit-ref````

开发者使用这些元素类描述某些对象，比如 web 应用需要被注册在运行时 web 容器的 JNDI 命名空间内的那些对象。

Java EE 环境的需求是关于配置 Java EE 规范第 5 章中描述的环境。

作为 Java EE 兼容性技术实现的一部分的 servlet 容器必须支持这种语法。参考 Java EE 规范以获取更多信息。这种类型的 servlet 容器必须支持查找这些对象以及对这些对象的调用，当在一个由 servlet 容器管理的线程上执行时。这种类型的 servlet 容器应该支持这种行为，当在由开发者创建的线程上执行时，但是目前这还不是强制需求。这些要求将会被加入下个版本的规范中。开发者需要谨慎依赖这种应用创建线程的能力，因为它们是不可移植的。

### 15.2.3 Web 模块上下文根 URL 的 JNDI 名称

Java EE 平台规范定义了一个标准的全局 JNDI 命名空间和一系列的相关命名空间映射到各种不同作用域的 Java EE 应用。这些命名空间可以被应用可移植地获取组件和资源的引用。本章节定义 JNDI 名称，通过它，web 应用的根 url 被强制需要被注册。

web 应用的上下文根目录预定义的````java.net.URL````资源的名称遵循以下语法：

````xml
<!-- 全局命名空间中 -->
java:global[/<app-name>]/<module-name>!ROOT
<!-- 应用特定命名空间中 -->
java:app/<module-name>!ROOT
````

参考 8.1.1 （组件创建）章节和 8.1.2（应用装配）获取确定应用名称和模块名称的规则。

只有当应用打包成为````.ear````文件时````<app-name>````才是有用的。

````java:app````前缀允许 Java EE 应用中执行的组件访问应用特定的命名空间。````java:app````名称允许企业级应用内部的模块引用同一个企业级应用中的其它模块的上下文根路径。````<module-name>````是````java:app```` url 的一个必需语法部分。

上述 URL 可以被用在下列应用中：

如果一个 web 应用被独立部署，其````module-name````是````myWebApp````。则该 URL 能够被注入其它 web 模块：

````
@Resource(lookup="java:global/myWebApp!ROOT")
URL myWebApp;
````

当打包成名为````myApp````的````.ear````文件后，可以被如下使用：

````
@Resource(lookup="java:global/myApp/myWebApp!ROOT")
URL myWebAPP;
````

## 15.3 安全

本节描述附加的安全需求，当 web 容器呗包含进入一个产品，该产品同时还包含 EJB，JACC 和／或者 JASPIC。接下来的章节列出了这些需求。

### 15.3.1 EJB 调用中安全标识的传递

安全标识，或者准则，在对企业级 bean 的调用中必须被提供。从 web 应用发起的对企业级 bean 的调用的默认模式中，web 用户的安全标识会被传递给 EJB 容器。

其它场景下，web 容器被要求允许不为 web 容器或者 EJB 容器所知的 web 用户发起调用：

* Web 容器被要求支持未经过容器身份认证的客户端访问 web 资源。这是 Internet 上通常的 web 资源的访问模式。
* 应用代码可以被作为基于调用者标识的信号和定制数据的唯一的处理器。

这些场景下，web 应用的部署描述器可以指定一个````run-as````元素。当为一个 Servlet 指定一个````run-as````角色，Servlet 容器必须传递一个准则映射到该角色，并作为从 Servlet 到 EJB 的所有调用中的安全标识，包含来自 Servlet 的````init````和````destroy````方法的调用。该安全角色名称必须是为该 web 应用定义的安全角色名中的一个。

因为 web 容器作为 Java EE 平台的一部分运行，````run-as````元素的使用必须支持同一个 Java EE 应用中的 EJB 组件的调用，还要支持部署在其它 Java EE 应用中的 EJB 组件的调用。

### 15.3.2 容器授权需求

在 Java EE 产品中，或者包含 Java 认证 SPI 支持的产品中，所有的 Servlet 容器必须实现 JASPIC 规范中的 Servlet 容器规范。JASPIC 规范下载地址：https://www.jcp.org/en/jsr/detail?id=196

## 15.4 部署

本节描述包含对 JSP 和／或 Web Services 支持的Java EE 技术兼容容器和产品的部署描述器、打包和部署描述器处理需求。

### 15.4.1 部署描述器元素

存在于 web 应用部署描述器中的下列附加元素满足支持 JSP 技术或者作为 Java EE 应用服务器一部分的 web 容器的需求。对那些只希望支持 servlet 规范的容器，这些都不是强制性要求：

* ````jsp-config````
* 声明资源引用的语法（````env-entry````，````ejb-ref````，````ejb-local-ref````，````resource-ref````，````resource-env-ref````）
* 指定消息目的地的语法（````message-destination````，````message-destination-ref````
* Web service 的引用（````service-ref````）
* 持久化上下文引用（````persistence-context-ref````）
* 持久化单元引用（````persistence-unit-ref````）

这些元素的语法目前都在 JSP 规范 2.2 版本和 Java EE 规范中定义。

### 15.4.2 JAX-WS 组件的打包和部署

Web容器可以选择支持运行的组件，这些组件是为了实现 JAX-RPC 和/或 JAX-WS 规范所定义的Web服务端点而编写的。嵌入到 Java EE 兼容实现中的 Web 容器必须支持 JAX-RPC 和 JAX-WS web service 组件。本节描述了包含在同时支持 JAX-RPC 和 JAX-WS 的产品中的 Web 容器的打包和部署模型。

JSR-109 https://jcp.org/en/jsr/detail?id=109 定义了 Web service 接口和相关的 WSDL 描述以及相关的类的打包模型。它为支持 JAX-WS 和 JAX-RPC 的 Web 容器定义了一种机制，以便链接到实现此 Web 服务的组件。JAX-WS 或 JAX-RPC Web service 实现组件使用由 JAX-WS 和/或 JAX-RPC 规范定义的 API，该规范定义了与启用 JAX-WS 和/或 JAX-RPC 的Web 容器的契约。它被打包到 WAR 文件中。Web service 开发者使用普通的````<servlet>````声明进行这种组件的声明。

启用 JAX-WS 和 JAX-RPC 的 Web 容器必须支持开发人员使用 Web 部署描述符为端点实现组件定义以下信息，使用与使用 servlet 元素的 HTTP Servlet 组件相同的语法。用于指定端点信息的子元素以下列方式指定：

* ````servlet-name````元素定义一个逻辑名称，可以被用于在 WAR 包中其它 web 组件中定位此端点描述。
* ````servlet-class````元素提供该端点实现的 Java 类的全限定名。
* ````description````元素可以被用于描述该组件，同时可以被显示在工具中。
* ````load-on-startup````元素指定相对于容器中其它 web 组件的初始化顺序。
* ````security-role-ref````元素可以被用于测试已认证的用户是否属于一个逻辑安全角色。
* ````run-as````元素可以被用于覆盖被该组件传递给被调用的 EJB 的标识。

任何开发者为 Web 组件定义的 servlet 初始化参数都可以被容器忽略。另外，支持 JAX-WS 和 JAX-RPC 的 web 组件继承了传统的 web 组件机制来定义下列信息：

* 使用 servlet 映射技术将组件映射到 web 容器的 URL 命名空间。
* web 组件的授权约束使用安全约束。
* 使用过滤器映射技术实现 servlet 过滤器使用来提供底层的字节流支持用来操作 JAX-WS 和／或 JAX-RPC 消息。
* 与组件相关的所有 HTTP 会话的超时特性。
* 指向存储在 JNDI 命名空间中的 Java EE 对象的链接。

所有以上需求都可以通过使用可插拔机制来满足，该机制在 8.2 章节中定义。

### 15.4.3 部署描述器处理规则

作为符合 Java EE 技术的实现的一部分的容器和工具需要根据 XML 模式验证部署描述符的结构正确性。建议进行验证，但不适用于不属于 Java EE 技术兼容实现的 Web 容器和工具。

## 15.5 注解和资源注入

Java 元数据规范（JSR-175）是 J2SE 5.0 及更高版本的一部分，它提供了一种在 Java 代码中指定配置数据的方法。 Java 代码中的元数据也称为注解。在 Java EE 中，注解用于在 Java 代码中声明对外部资源和配置数据的依赖性，而无需在配置文件中定义该数据。

本节描述符合 Java EE 技术的 Servlet 容器中注解和资源注入的行为。本节扩展了标题为“资源，命名和注入”的 Java EE 规范第 5 节。

必须在以下容器托管类上支持注解，这些类实现以下接口并在 Web 应用部署描述符中声明，或者使用第 8.1 节“注解和可插入性”中定义的注解或以编程方式添加。

支持注解和资源注入的组件和接口：

| 组件类型  | 类实现以下接口                                               |
| --------- | ------------------------------------------------------------ |
| Servlets  | javax.servlet.Servlet                                        |
| Filters   | javax.servlet.Filter                                         |
| Listeners | javax.servlet.ServletContextListener<br />javax.servlet.ServletContextAttributeListener<br />javax.servlet.ServletRequestListener<br />javax.servlet.ServletRequestAttributeListener<br />javax.servlet.http.HttpSessionListener<br />javax.servlet.http.HttpSessionAttributeListener<br />javax.servlet.http.HttpSessionIdListener<br />javax.servlet.AsyncListener |
| Handlers  | javax.servlet.http.HttpUpgradeHandler                        |

并不强制 web 容器为不在上表中的类中的注解执行资源注入。

必须在调用任何生命周期方法和使组件实例可用于应用程序之前注入引用。

在 web 应用中，使用资源注入的类只有在位于````WEB-INF/classes````目录下时它们的注解才会被处理，或者它们被打包在 jar 文件的````WEB-INF/lib````目录下。容器可以选择处理在应用的 classpath 中其它位置的类中的资源注入注解。

### 15.5.1 metadata-complete 处理

web 应用的部署描述器文件的````web-app````元素包含一个````metadata-complete````属性。````metadata-complete````属性定义了````web.xml````部署描述器是否是完整的，或者部署过程中是否应该考虑所使用原数据的其它来源。原数据可以来自````web.xml````文件、````web-fragment.xml````文件、目录````WEB-INF/classes````下类文件中的注解以及````WEB-INF/lib````目录下的 jar 文件中类上的注解。如果````metadata-complete````设置为````true````，则部署工具只会检查````web.xml````文件，而必须忽略诸如````@WebServlet````、````@WebFilter````和````@WebListener````等出现在应用中类文件中的注解，同时必须忽略被打包进入````WEB-INF/lib````目录下的 jar 文件的````web-fragment.xml````部署描述器文件。如果````metadata-complete````属性没有出现或者被设置为````false````，部署工具就必须检查类文件和````web-fragment.xml````文件来获取元数据，如前所述。

````web-fragment.xml````文件在````web-fragment````元素上包含````metadata-complete````属性。该属性定义该````web-fragment.xml````部署描述器文件对给定的分片是否是完备的，或者是否应该在有关的 jar 文件中扫描注解。如果````metadata-complete````被设定为````true````，部署工具就只需要检查该````web-fragment.xml````文件，而必须忽略诸如````@WebServlet````、````@WebFilter````和````@WebListener````等出现在片段中类文件中的注解。如果````metadata-complete````属性不存在或者呗设置为````false````，部署工具就必须检查类文件以获取元数据。

以下是符合 Java EE 技术的 Web 容器所需的注解。

### 15.5.2 @DeclareRoles

此注解用来定义包含应用的安全模型的安全角色。此注解在类上指定，并用于定义可以在带注解的类的方法内测试的角色（即，通过调用````isUserInRole````）。无需使用````@DeclareRoles````注解显式声明因在````@RolesAllowed````中使用而被隐式声明的角色。````@DeclareRoles````注解只能被用在实现了````javax.servlet.Servlet````接口的类或者它们的子类中。

下面的例子展示了此注解的使用方法：

````@DeclareRoles````注解的例子：

````java
@DeclareRoles("BusinessAdmin")
public class CalculatorServlet {
    //...
}
````

等价于````web.xml````中以下内容：

````xml
<web-app>
    <security-role>
        <role-name>BusinessAdmin</role-name>
    </security-role>
</web-app>
````

此批注不用于将应用程序角色重新链接到其他角色。当需要这种链接时，可以通过在关联的部署描述符中定义适当的````security-role-ref````来完成。

当````isUserInRole````方法调用来自被注解的类，将测试与类调用相关联的调用者标识的角色成员身份，该角色名称与````isCallerInRole````的参数相同。如果已为参数````role-name````定义了````security-role-ref````，则会在映射到````role-name````的角色过程中测试调用方的成员资格。

有关````@DeclareRoles````注解的更多详细信息，请参阅 Java 平台规范（JSR 250）第2.12节中通用注解的描述。

### 15.5.3 @EJB 注解

企业级 JavaBeans 3.2（EJB）组件可以使用````@EJB````注解从 web 组件引用。````@EJB````注解提供了与部署描述器文件中的````ejb-ref````或者````ejb-local-ref````元素等价的功能。添加了````@EJB````注解的字段被注入相应的 EJB 组件的引用。

例如：

````java
@EJB
private ShoppingCart myCart;
````

这个例子中 EJB 组件````myCart````的引用被作为私有字段````myCart````的值被注入，这种注入在声明该注入的类变成可用状态之前完成。

````@EJB````注解的更多细节请参考 EJB 3.2 规范（JSR 345）的 11.5.1 章节。

### 15.5.4 @EJBs 注解

此注解允许多个````@EJB````注解声明在同一个资源上。

例子：

````java
@EJBs({@EJB(Calculator), @EJB(ShoppingCart)})
public class ShoppingCartServlet {
    //...
}
````

上面的例子中 EJB 组件````ShoppingCart````和````Calculator````对````ShoppingCartServlet````成为可用的。该````ShoppingCartServlet````必须仍然通过 JNDI 查找引用，不过 EJBs 不需要在````web.xml````文件中声明。

### 15.5.5 @Resource 注解

此注解用来声明一个资源的引用，比如数据源，Java 消息服务（JMS）目的地，或者环境入口等。此注解等价于在部署描述器文件中声明````resource-ref````、````message-destination-ref````、````env-ref````或者````resource-env-ref````元素。

此注解放在类、方法或者字段上。容器负责此注解声明的资源的引用同时将其映射到适当的 JNDI 资源。参考 Java EE 规范文档的第 5 章以获取更多细节。

例子：

````java
@Resource
private javax.sql.DataSource catalogDS;

public getProductsByCategory() {
    // get a connection and execute the query
    Connection conn = catalogDS.getConnection();
    //...
}
````

这个例子中，一个 servlet、过滤器或者监听器声明一个类型为````javax.sql.DataSource````的字段````catalogDS````，由此这个数据源的引用被容器在该组件对应用可用之前注入进来。该数据源的 JNDI 映射由字段名````catalogDS````和类型````javax.sql.DataSource````得出。此外，该````catalogDS````资源不再需要在部署描述器文件中定义。

此注解的语义的更多细节在 Java 平台规范（JSR 250）中 2.3 章节普通注解部分介绍，同时在 Java EE 7 规范 5.2.5 章节中介绍。

### 15.5.6 @PersistenceContext 注解

此注解为引用的持久化单元指定容器管理的实体管理器。

例子：

````java
@PersistenceContext (type=EXTENDED)
EntityManager em;
````

更多细节参考 Java Persistence API v2.1（JSR 338）10.5.1 章节。

### 15.5.7 @PersistenceContexts 注解

此注解允许多个````@PersistenceContext````注解被声明在一个资源上。更多细节参考 Java Persistence API v2.1（JSR 338）10.5.1 章节。

### 15.5.8 @PersistenceUnit 注解

此注解为 servlet 中声明的 Enterprise Java Bean 组件提供了对实体管理器工厂的引用。实体管理器工厂绑定到单独的 persistence.xml 配置文件，如 EJB 3.2 规范（JSR 345）的第 11.10 节中所述。

例子：

````java 
@PersistenceUnit
EntityManagerFactory emf;
````

更多细节参考 Java Persistence API v2.1（JSR 338）10.5.2 章节。

### 15.5.8 @PersistenceUnits 注解

此注解允许多个````@PersistenceUnit````注解声明在同一个资源上。更多细节参考 Java Persistence API v2.1（JSR 338）10.5.2 章节。

### 15.5.10 @PostConstruct 注解

此注解是在不接受任何参数的方法上声明的，并且不得抛出任何已检查的异常。返回值必须为````void````。必须在完成资源注入之后并且在调用组件上的任何生命周期方法之前调用该方法。

例子：

````java
@PostConstruct
public void postConstruct() {
    //...
}
````

所有支持依赖注入的类都必须支持````@PostConstruct````注解，并且即使该类没有请求注入任何资源也会调用它。如果该方法抛出未经检查的异常，则该类必须不能投入使用，并且不能调用该实例上的任何方法。

有关更多详细信息，请参阅 Java EE 规范第 2.5 节和 Java Platform 规范的公共注解部分 2.5 章节。

### 15.5.11 @PreDestroy 注解

此注解用在容器管理的组件的方法上。该方法在组件被容器移除之前被调用。

例子：

````java
@PreDestroy
public void cleanup() {
    // clean up any open resources
}
````

使用````@PreDestroy````注解的方法必须返回````void````，并且不得抛出已检查的异常。该方法可以是公共的，受保护的，包私有的或私有的。该方法不能是静态的，但它可能是````final````的。

有关更多详细信息，请参阅 JSR 250 第 2.6 节。

### 15.5.12 @Resources 注解

````@Resources````注解充当多个````@Resource````注解的容器，因为 Java MetaData 规范不允许在同一注解目标上使用相同名称的多个注解。

例子：

````java
@Resources ({
    @Resource(name="myDB" type=javax.sql.DataSource),
    @Resource(name="myMQ" type=javax.jms.ConnectionFactory)
})
public class CalculatorServlet {
    //...
}
````

在上面的示例中，JMS 连接工厂和数据源通过````@Resources````注解提供给````CalculatorServlet````。

此注解的语义在 Java Platform 规范（JSR 250）第2.4节的通用注解中进一步详细说明。

### 15.5.13 @RunAs 注解

此注解等同于部署描述符中的````run-as````元素。 此注解只能在实现````javax.servlet.Servlet````接口或其子类的类中定义。

例子：

````java
@RunAs("Admin")
public class CalculatorServlet {
    @EJB private ShoppingCart myCart;
    
    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        //...
        myCart.getTotal();
        //...
    }
}
````

等价于````web.xml````文件中以下部分：

````xml
<servlet>
    <servlet-name>CalculatorServlet</servlet-name>
    <run-as>Admin</run-as>
</servlet>
````

上面的示例显示了在调用````myCart.getTotal( )````方法时，servlet 如何使用````@RunAs````注解将安全标识“Admin”传递到 EJB 组件。有关传递标识的更多详细信息，请参见第 15.3.1 节“EJB 调用中的安全标识的传递”。

有关更多详细信息，请参阅 Java Platform 规范的公共注解部分 2.7 章节。

### 15.5.14 @WebServiceRef 注解

````@WebServiceRef````注解以与部署描述符中的````resource-ref````元素相同的方式提供对 Web 组件中的 Web 服务的引用。

例子：

````java
@WebServiceRef private MyService service;
````

例子中 web service “MyService” 的引用将被注入声明此注解的类。

此注解的行为和更多细节参考 JAX-WS 规范（JSR 224）第 7 章。

### 15.5.15 @WebServiceRefs 注解

此注解允许在单个资源上声明多个````@WebServiceRef````注解。 JAX-WS 规范（JSR 224）第7节进一步详细说明了此注解的行为。

### 15.5.16 针对 Java EE 需求的上下文和依赖注入

在支持 Java EE 上下文和依赖注入（CDI）并且启用了 CDI 的产品中，实现必须支持使用 CDI 托管 bean。 Servlet，过滤器，监听器和 HttpUpgradeHandler 必须支持 CDI 注入和拦截器的使用，如 Java EE 7 平台规范的章节 EE.5.24 “支持依赖注入”中所述。