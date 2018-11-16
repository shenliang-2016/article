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

