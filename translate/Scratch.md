### 5.10. Cloud Foundry  支持

Spring Boot 执行器模块包含额外的支持，当你将应用部署到兼容的 Cloud Foundry 实例中时会被激活。`/cloudfoundryapplication` 路径提供了通向所有 `@Endpoint` 的替代安全路由。

扩展支持使 Cloud Foundry 管理 UI（例如可用于查看已部署的应用程序的 Web 应用程序）增加了 Spring Boot 执行器信息。例如，应用程序状态页面可能包含完整的运行状况信息，而不是典型的“正在运行”或“已停止”状态。

>  `/cloudfoundryapplication` 路径并不注解对普通用户开放。为了使用该端点，请求中必须携带有效的 UAA token 。

#### 5.10.1. 禁用扩展 Cloud Foundry 执行器支持

如果你想要完全禁用 `/cloudfoundryapplication` 端点，你可以将下面的设定到你的 `application.properties` 文件中：

**application.properties**

```properties
management.cloudfoundry.enabled=false
```

#### 5.10.2. Cloud Foundry 自签名证书

默认情况下， `/cloudfoundryapplication`  端点的安全性验证会对各种 Cloud Foundry 服务进行 SSL 调用。如果您的 Cloud Foundry UAA 或 Cloud Controller 服务使用自签名证书，则需要设置以下属性：

**application.properties**

```properties
management.cloudfoundry.skip-ssl-validation=true
```

#### 5.10.3. 自定义上下文路径

如果服务器的上下文路径已配置为`/`以外的任何其他值，则 Cloud Foundry 端点在应用程序的根目录将不可用。例如，如果使用 `server.servlet.context-path=/app`，则 Cloud Foundry 端点将位于 `/app/cloudfoundryapplication/*`。

如果您希望 Cloud Foundry 端点始终在 `/cloudfoundryapplication/*` 处可用，而不管服务器的上下文路径如何，那么您将需要在应用程序中显式配置它。配置将根据所使用的 Web 服务器而有所不同。对于 Tomcat，可以添加以下配置：

```java
@Bean
public TomcatServletWebServerFactory servletWebServerFactory() {
    return new TomcatServletWebServerFactory() {

        @Override
        protected void prepareContext(Host host, ServletContextInitializer[] initializers) {
            super.prepareContext(host, initializers);
            StandardContext child = new StandardContext();
            child.addLifecycleListener(new Tomcat.FixContextListener());
            child.setPath("/cloudfoundryapplication");
            ServletContainerInitializer initializer = getServletContextInitializer(getContextPath());
            child.addServletContainerInitializer(initializer, Collections.emptySet());
            child.setCrossContext(true);
            host.addChild(child);
        }

    };
}

private ServletContainerInitializer getServletContextInitializer(String contextPath) {
    return (c, context) -> {
        Servlet servlet = new GenericServlet() {

            @Override
            public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
                ServletContext context = req.getServletContext().getContext(contextPath);
                context.getRequestDispatcher("/cloudfoundryapplication").forward(req, res);
            }

        };
        context.addServlet("cloudfoundry", servlet).addMapping("/*");
    };
}
```