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

  实例化给定的 AsyncListener 。返回的 AsyncListener 实例在通过下面将要说到的 addListener  方法注册到 AsyncContext 之前可以被进一步盯着。作为参数的 AsyncListener 必须定义一个无参构造器用来实例化。此方法支持任何 AsyncListener 适用的注解。

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

![image-20181223193212373](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/servlet/image-20181223193212373-5564732.png)


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

   d. ````absolute-ordering````元素可以包含零个或者一个````<others/>````元素。该元素的行为要求下文给出。如果````absolute-ordering````元素不包含````<others/>````元素，任何没有在````<name/>````元素中特别提到的 web-fragment 都必须被忽略。被排除的 jars 中的注解标注的 servlets、过滤器以及监听器都不会被扫描。





   ### 8.2.3 组装来自````web.xml````、````web-fragment.xml````和注解的部署描述符



   ### 8.2.4 类库共享/运行时可插拔性





   ## 8.3 JSP 容器可插拔性



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
* ​