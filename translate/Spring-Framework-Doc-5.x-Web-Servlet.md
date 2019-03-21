# Web on Servlet Stack

Version 5.1.5.RELEASE

----

文档的这一部分介绍基于 Servlet API 构建并部署在 Servlet 容器中的 Servlet-stack web 应用的支撑技术。包括以下单独的章节 [Spring MVC](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc), [View Technologies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-view), [CORS Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc-cors), 和 [WebSocket Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#websocket).。有关 reactive-stack web applications, 可以参考 [Web on Reactive Stack](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web-reactive.html#spring-web-reactive).

# 1. DispatcherServlet

Spring MVC，如同许多其它 web 框架，围绕一个中央````Servlet````按照前端控制器模式进行设计。该中央````Servlet````，也就是````DispatcherServlet````，为请求处理提供了共享算法，同时实际的工作其实是由可配置的代理组件执行。这种模型是灵活的，而且可以支持各种各样的工作流程。

````DispatcherServlet````，如同任何其它````Servlet````，需要按照 Servlet 规范使用 Java 配置类或者在部署描述器文件````web.xml````中声明和映射。然后，该````DispatcherServlet````使用 Spring 配置来发现它进行请求映射所需要的代理组件、视图解析器、异常处理器等等。

