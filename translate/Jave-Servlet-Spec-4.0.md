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
  - 5.7  响应对象闭包
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

> 1.1  Servlet 是什么？

servlet 是一种基于 Java 的 Web 组件，由容器管理，产生动态内容。类似于其他基于 Java 的组件，servlet 也是平台无关的 Java 类，被编译称为跨平台的中间代码之后可以被任何支持 Java 的 Web 服务器动态加载并运行。容器，有时也称为 servlet 引擎，作为 Web 服务器的扩展提供对 servlet 的支持。servlets  通过容器实现的请求/响应范式与 Web 客户端互动。

> 1.2  Servlet 容器是什么？

servlet 容器作为 Web 服务器或者应用服务器的一部分，通过发送请求和响应提供网络服务。同时负责解码 MIME 请求数据和编码 MIME 类型的响应数据。servlet 整个生命周期都被容器持有和管理。

servlet 容器可以被内建进 Web 服务器，或者通过本地扩展 API 作为扩展插件安装。当然，也可以内建进或者安装进具有 Web 功能的应用服务器。

所有的 servlet 容器都必须支持 HTTP 作为请求响应协议，其他类似的请求-响应协议，例如 HTTPS (HTTP over SSL) 也可以支持。必须支持的 HTTP 协议规范版本有 HTTP/1.1 和 HTTP/2 。对于 HTTP/2，容器必须支持 “h2” 和 "h2c" 协议标识符 （在3.1章节中 HTTP/2 RFC 中规定）。这就隐含表明所有的容器都必须支持 ALPN。根据 RFC(HTTP/1.1 缓存) 所述，容器可以实现某种缓存机制，它可以在将来自客户端的请求分发到 servlet 之前修改请求，可以在将响应发送给客户端之前修改它，当然也可以根据 RFC 7234 规范直接响应请求而不把它们分发到 servlet 。

容器可以在 servlet 执行环境中布置安全约束。在 J2SE v1.3 及以上版本或者 Java EE v1.3 或以上版本环境中，这种安全约束必须采用 Java 平台定义的认证体系架构。例如某些应用服务器会限制线程对象的创建以避免对容器的其他组件产生消极影响。

此版本 servlet 容器需要的最低语言版本是 Java SE 8 。

> 1.3  例子

下面是一个典型的事件序列：

1. 客户端（比如 Web 浏览器）发起一个 HTTP 请求以访问 Web 服务器；
2. 请求被 Web 服务器接收到然后交接给 servlet 容器。容器可能和 Web 服务器运行在同一台主机的同一个进程内，可能在同一台主机的不同进程内，当然也可能运行在不同主机上；
3. 根据配置文件，容器确定应该调用哪个 servlet 处理请求，然后以请求对象和响应对象作为参数调用之；
4. 通过请求对象，servlet 可以找出远程用户信息、请求方法以及其他相关数据。执行它被赋予的程序逻辑之后，产生的数据被发回给客户端。servlet通过响应对象将结果数据发送给客户端。
5. 一旦完成请求的处理，servlet 容器确认响应数据已经完整发送，就将控制权交还给 Web 服务器。

> 1.4  Servlet 与其他技术的比较

从功能来看， servlet 提供了提供了比通用网关接口 CGI 更高一层的抽象，但是要比 JSF 之类的 web 框架的抽象层次要低一些。

servlets 相比于其他服务器扩展机制有以下优点：

- 由于采用了不同点处理模型，通常要比 CGI 脚本快。
- 采用了很多 Web 服务器都支持的标准 API 。
- 继承了 Java 语言的所有优点，包括部署简单和平台无关性。
- 可以方便地使用 Java 平台提供的大量 API 。

> 1.5  与 Java EE 平台的关系

Java Servlet API v4.0 是 Java EE 8 的一部分必要 API 。为了运行在 Java EE 环境中，容器以及部署在其中的 servlet 必须满足 Java EE 规范所描述的其他需求。

> 1.6  与 2.5 版本规范的区别

> 1.6.1  配置注解  

Servlet 2.5 中， metadata-complete 属性只是在部署过程中影响注解的扫描，而且也没有 web-fragments 的概念。在 servlet 3.0 之后，metadata-complete 属性会在部署过程中影响到所有指定部署信息的注解，同时还有 web-fragments 。部署描述符的版本绝对不能影响容器扫描应用中的注解。本规范的任何版本的实现都必须扫描所有该配置所支持的注解，除非指定了 metadata-complete 属性。

# Servlet 接口

----

Servlet 接口是 Java Servlet API 的核心抽象。所有的 servlets 都必须直接或者间接实现该接口。Java Servlet API 中已经实现了 Servlet 接口的两个类是 GenericServlet 和 HttpServlet 。大多数情况下，开发者可以继承 HttpServlet 来实现自己的 servlets 。

> 2.1  请求处理方法

基本的 Servlet 接口定义了处理客户端请求的 service 方法。每个请求到来，容器将它路由到某个 servlet 实例，该方法就会被调用。

为了处理并发请求，开发者需要将 servlet 设计成可多线程执行，也就是同一时刻可以有多个线程同时执行 service 方法。

通常容器会在多线程中执行 service 方法来处理对同一个 servlet 的多个并发请求。

> 2.1.1  HTTP 特定的请求处理方法

HttpServlet 抽象子类在基本的 Servlet 接口基础上添加了被  service 接口调用的方法，用于处理基于 HTTP 的请求。

- doGet 处理 HTTP GET 请求
- doPost 处理 HTTP POST 请求
- doPut 处理 HTTP PUT 请求
- doDelete 处理 HTTP DELETE 请求
- doHead 处理 HTTP HEAD 请求
- doOptions 处理 HTTP OPTIONS 请求
- doTrace 处理 HTTP TRACE 请求


通常，开发基于 HTTP 的 servlet 的开发者仅仅只会关注 doGet 和 doPost 方法。其他几个方法是供那些对 HTTP 协议非常熟悉的开发者使用。

> 2.1.2   附加方法

doPut 和 doDelete 方法允许 Servlet 开发者支持那些支持此类特性的 HTTP/1.1 客户端。doHead 方法是 doGet 方法的一种特殊形式，它仅仅返回 doGet 产生的响应的头部。doOptions 方法返回 servlet 都支持哪些 HTTP 方法。doTrace 方法产生的响应包含了所有的 TRACE 请求的头部实例。

CONNECT 方法不支持，因为它是作用于代理以及被绑定到服务访问点上的 Servlet API 。

> 2.1.3  条件 GET 支持

HttpServlet 抽象类定义的 getLastModified 方法支持条件 GET 操作。条件 GET 操作请求的资源，只有在某个时刻之后被修改过的情况下才会被返回给客户端。在适当的场景下，实现该方法可以改善网络资源的利用率。

> 2.2  实例个数

声明 servlet ，无论是通过注解还是部署描述符，都可以控制容器如何提供 servlet 实例。

因为默认情况下， servlet 并不是生存在分布式环境中，因此容器必须为每个 servlet 声明产生唯一的实例。然而，由于 servlet 实现了 SingleThreadModel 接口，容器可以初始化多个实例以应对大量的请求，每个请求将被分配给某个特性的实例处理。

如果 servlet 作为应用的一部分部署，而部署描述符又明确说明是分布式部署，那么容器可以为每个 Java 虚拟机提供唯一的 servlet 实例。然而，如果 servlet 实现了 SingleThreadModel 接口，容器就可以为每个虚拟机提供多个 servlet 实例。

> 2.2.1  关于 Single Thread Model 的说明

SingleThreadModel 接口的作用是保证在同一时刻只有一个线程可以执行给定 servlet 实例的 service 方法。需要特别注意的是，这个保证只是对于单个 servlet 实例而言，因为容器可以有选择地池化此类对象。那些可以同时被多个 servlet 实例访问的对象，比如 HttpSession 实例，可能在任何时刻对多个 servlet 都是可用的，SingleThreadModel 接口的实现应该包含此内容。

推荐开发者采用其他方式解决以上问题，而不要实现 SingleThreadModel 接口。比如避免使用实例变量或者将访问此类资源的代码同步化。此版本规范中 SingleThreadModel 接口已被废弃。

> 2.3  Servlet 生命周期

servlet 的管理基于定义良好的生命周期。所谓的生命周期，定义了 servlet 应该如何被加载、实例化、初始化、处理请求以及如何从服务中被移除。在 API 生命周期的形式表现为 javax.servlet.Servlet 接口的 init，service 以及 destroy 方法。所有的 servlet 都必须直接实现该接口，或者通过继承 GenericServlet 或者 HttpServlet 抽象类间接实现该接口。

> 2.3.1  加载和实例化

容器负责加载和实例化 servlets 。加载和实例化可以发生在容器启动时，或者延迟到容器真正认为需要它处理请求时。

当 servlet 引擎启动后，容器必须找到所需要的 servlet 类。容器利用通常的 Java 类的加载机制加载这些 servlet 类。可以从本地文件系统、远程文件系统甚至网络服务处加载。

加载完 Servlet 类之后，容器将实例化它们以备使用。

> 2.3.2  初始化

servelt 对象实例化之后，必须经过容器的初始化才能处理来自客户端的请求。基于初始化机制，servlet 可以读取持久化配置数据，初始化动作消耗资源（比如基于的 JDBC API 的数据库连接），同时执行其他一些一次性的活动。容器通过调用 Servlet 接口的 init 方法来初始化 servlet 实例，该方法的参数是唯一的（每个 servlet 声明）实现了 ServletConfig 接口的类对象。servlet 可以通过这个配置对象从 Web 应用的配置信息中获取“名—值”对形式的初始化参数。还可以通过该对象获取描述 servlet 运行期环境的类对象（实现了 ServletContext 接口）。关于 ServletContext 接口的更多内容将在第四章中介绍。

> 2.3.2.1  初始化的错误

初始化过程中，servlet 实例可以抛出 UnavailableException 或者 ServletException 。这种情况下，servlet 必须被容器清理掉，不能放到活动的服务中去。这种情况被认为初始化失败，因此 destroy 方法不会被调用。

在一次失败的初始化之后，容器可以实例化和初始化新的实例。唯一需要额外说明的就是 UnavailableException 表示一个最小时间段内的不可用状态，因此容器必须等待这个时间段过去然后再开始创建并初始化下一个 servlet 实例。

> 2.3.2.2  工具考量

静态初始化方法在工具加载并内省（反射）Web 应用过程中被触发的情况与 init 方法被调用的情况是不同的。开发者在Servlet 接口的 init 方法被调用之前都不能假定 servlet 已经在活动容器的运行时环境中了。比如说，servlet不应该在仅仅只有静态初始化方法被调用的情况下试图建立与数据库或者 EJB 容器的连接。

> 2.3.3  请求处理

servlet 正确初始化之后，就可以被容器用来处理客户端请求。请求由 ServletRequest 类型的请求对象表示。servlet 调用相应的处理方法并以 ServletResponse 类型的对象填充响应。这些对象作为参数被传递给 Servlet 接口的 service 方法。

如果是 HTTP 请求，容器提供的对象类型就是 HttpServletRequest 和 HttpServletResponse 。

特别的，被容器放进服务中的 servlet 实例可以在整个生命周期内不处理任何请求。

> 2.3.3.1  多线程问题

servlet 容器可以通过 servlet 的 service 方法发送并发请求。为了处理这些请求，servlet 开发者必须保证 service 方法的实现具有处理并发请求的能力。

尽管不推荐，开发者可以采取实现 SingleThreadModel 接口的方式来要求容器保证同一时刻只有一个请求线程处于 service 方法内部。容器可以通过串行化请求或者将 servlet 实例池化的方式来满足此要求。如果应用已经被被指为可分布式的，那么当应用分布式部署时容器将在每个 JVM 内部都维护一个 servlet 实例池。

由于 servlet 并未实现 SingleThreadModel 接口，如果 service 方法（或者由该方法分发到的 HttpServlet 抽象类的 doGet 或者 doPost 方法）被 synchronized 关键字修饰，容器将无法采用池化技术，而不得不强行将请求串行化。强烈建议开发者在这种环境下不要同步化 service 方法（或者由它分发到的方法），因为这将对性能造成决定性的影响。

> 2.3.3.2  请求处理过程中的异常

处理请求过程中 servlet 可以抛出 ServletException 或者 UnavailableException 异常。ServletException 表示在处理请求过程中发生了某些错误因而容器应该采取对应措施将请求清除掉。

UnavailableException 表示 servlet 暂时或者永久性地无法处理请求。

如果 UnavailableException 表示永久性的不可用，容器就必须从服务中清除该 servlet ，调用它的 destroy 方法，然后释放该 servlet 实例。由此导致的被决绝的请求都必须返回 SC_NOT_FOUND (404) 响应。

如果 UnavailableException 表示暂时性的不可用，容器可以选择在这段不可用的时间内不再将请求路由到该 servlet 。所有因此而被拒绝的请求都必须返回 SC_SERVICE_UNAVAILABEL (503) 状态的响应，同时附带 Retry-After 响应头用于表示不可用状态何时结束。

容器可以选择不区分这两种情况，而认为 UnavailableException 就是表示永久性的不可用，而后直接将抛出该异常的 servlet 从服务中清除掉。

> 2.3.3.3  异步处理

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