# Web on Servlet Stack

Version 5.1.5.RELEASE

----

文档的这一部分介绍基于 Servlet API 构建并部署在 Servlet 容器中的 Servlet-stack web 应用的支撑技术。包括以下单独的章节 [Spring MVC](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc), [View Technologies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-view), [CORS Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-cors), 和 [WebSocket Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#websocket).。有关 reactive-stack web applications, 可以参考 [Web on Reactive Stack](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web-reactive.html#spring-web-reactive).

# 1. Spring Web MVC

Spring Web MVC 是建立在 Servlet API 基础上的原生 web 框架，从一开始就已经被包含在 Spring 框架中。正式名称````Spring Web MVC````，来自它的源代码模块名([`spring-webmvc`](https://github.com/spring-projects/spring-framework/tree/master/spring-webmvc))，不过它更广泛为人所知的却是名字````Spring MVC````。

与 Spring Web MVC 并列，Spring 框架 5.0 引入了名为````Spring WebFlux````的基于响应式技术栈的 web 框架，名字同样来自它的源代码模块名 ([`spring-webflux`](https://github.com/spring-projects/spring-framework/tree/master/spring-webflux))。本章介绍 Spring Web MVC，下一章介绍 Spring WebFlux。

获取基线信息以及与 Servlet 容器和 Java EE 版本范围的兼容性，参考 Spring 框架 [Wiki](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Versions)。

## 1.1 DispatcherServlet

Spring MVC，如同许多其它 web 框架，围绕一个中央````Servlet````按照前端控制器模式进行设计。该中央````Servlet````，也就是````DispatcherServlet````，为请求处理提供了共享算法，同时实际的工作其实是由可配置的代理组件执行。这种模型是灵活的，而且可以支持各种各样的工作流程。

````DispatcherServlet````，如同任何其它````Servlet````，需要按照 Servlet 规范使用 Java 配置类或者在部署描述器文件````web.xml````中声明和映射。然后，该````DispatcherServlet````使用 Spring 配置来发现它进行请求映射所需要的代理组件、视图解析器、异常处理器等等。

下面的例子展示了通过 Java 配置类注册和初始化````DispatcherServlet````，可以被 Servlet 容器自动探测到（参考  [Servlet Config](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-container-config)）：

````java
public class MyWebApplicationInitializer implements WebApplicationInitializer {
    
    @Override
    public void onStartup(ServletContext servletCxt) {
        // Load Spring web application configuration
        AnnotationConfigWebApplicationContext ac = new AnnotationConfigWebApplicationContext();
        ac.register(AppConfig.class);
        ac.refresh();
        
        // Create and register the DispatcherServlet
        DispatcherServlet servlet = new DispatcherServlet(ac);
        ServletRegistration.Dynamic registration = servletCxt.addServlet("app", servlet);
        registration.setLoadOnStartup(1);
        registration.addMapping("/app/*");
    }
}
````

> 除了直接使用 ServletContext API，你还可以继承````AbstractAnnotationConfigDispatcherServletInitializer````并且覆盖其中的特定方法（参考  [Context Hierarchy](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-servlet-context-hierarchy) 下的例子）。

下面的例子展示了在````web.xml````配置文件中注册和初始化````DispatcherServlet````：

````xml
<web-app>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/app-context.xml</param-value>
    </context-param>
    
    <servlet>
        <servlet-name>app</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value></param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>app</servlet-name>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>
</web-app>
````

> Spring Boot 遵循不同的初始化序列。Spring Boot 使用 Spring 配置来引导它自己以及内置的 Servlet   容器，而不依靠 Servlet 容器进行生命周期管理。Spring 配置中被探测到的````Filter````和````Servlet````声明会随着 Servlet 容器注册。更多细节参考 [Spring Boot documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-embedded-container)。

### 1.1.1 Context 层级结构

````DsipatcherServlet````期望一个````WebApplicationContext````（普通的````ApplicationContext````的扩展）为了它自己的配置。````WebApplicationContext````拥有一个指向````ServletContext````以及与之相关的````Servlet````的链接。它们也会被绑定到````ServletContext````因而应用可以使用````RequestContextUtils````中的静态方法来寻找````WebApplicationContext````，如果它们需要访问它。

对很多应用来说，拥有唯一一个````WebApplicationContext````是简单而又足够的。不过也可能存在一个 context 的层级结构，作为根的````WebApplicationContext````在多个````DispatcherServlet````或者其它````Servlet````实例之间共享，每个都拥有它们自己的子````WebApplicationContext````配置。更多信息参见  [Additional Capabilities of the `ApplicationContext`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#context-introduction)。

根````WebApplicationContext````典型地包含基础设施 beans，比如数据存取类和业务服务类等需要在多个````Servlet````实例之间共享的 beans。这些 beans 可以在 Servlet 各自的子````WebApplicationContext````中有效地继承和覆盖，这些````WebApplicationContext````中通常包含属于给定````Servlet````的 beans 。下面的图展示了上述关系：

![image-20190321204627481](/work/article/translate/assets/spring/image-20190321204627481.png)

下面的例子配置了一个````WebApplicationContext````层级结构：

````java
public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[] { RootConfig.class };
    }
    
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class<?>[] { App1Config.class };
    }
    
    @Override
    protected String[] getServletMapping() {
        return new String[] { "/app1/*" };
    }
}
````

>  如果一个应用上下文层级结构不是必需的，则应用可以通过````getRootConfigClasses()````返回所有的配置，同时通过````getServletConfigClasses()````方法返回````null````。

下面的例子是等效的````web.xml````：

````xml
<web-app>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/root-context.xml</param-value>
    </context-param>

    <servlet>
        <servlet-name>app1</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/app1-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>app1</servlet-name>
        <url-pattern>/app1/*</url-pattern>
    </servlet-mapping>

</web-app>
````

> 如果一个应用中上下文层级结构不是必需的，则应用可以只配置````root````上下文，同时将````contextConfigLocation```` Servlet 参数置空。

### 1.1.2 指定 Bean 类型