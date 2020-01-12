###### 映射 Spring MVC 之外的错误页面

对于不使用 Spring MVC 的应用程序，可以使用 `ErrorPageRegistrar` 接口直接注册 `ErrorPages`。此抽象直接与基础嵌入式 servlet 容器一起使用，即使您没有 Spring MVC `DispatcherServlet` 也可以使用。

```java
@Bean
public ErrorPageRegistrar errorPageRegistrar(){
    return new MyErrorPageRegistrar();
}

// ...

private static class MyErrorPageRegistrar implements ErrorPageRegistrar {

    @Override
    public void registerErrorPages(ErrorPageRegistry registry) {
        registry.addErrorPages(new ErrorPage(HttpStatus.BAD_REQUEST, "/400"));
    }

}
```

> 如果您注册的 `ErrorPage` 具有最终由 `Filter` 处理的路径（这在某些非 Spring Web 框架，如 Jersey 和 Wicket，中很常见），则必须将 `Filter` 明确注册为 `ERROR` 调度程序，如以下示例所示：

```java
@Bean
public FilterRegistrationBean myFilter() {
    FilterRegistrationBean registration = new FilterRegistrationBean();
    registration.setFilter(new MyFilter());
    ...
    registration.setDispatcherTypes(EnumSet.allOf(DispatcherType.class));
    return registration;
}
```

请注意，默认的 `FilterFilterationBean` 不包含 `ERROR` 调度程序类型。

注意：当 Spring Boot 部署到 servlet 容器时，将使用其错误页面过滤器将具有错误状态的请求转发到适当的错误页面。如果尚未提交响应，则只能将请求转发到正确的错误页面。缺省情况下，WebSphere Application Server 8.0 及更高版本在成功完成 servlet 的服务方法后提交响应。您应该通过将 `com.ibm.ws.webcontainer.invokeFlushAfterService` 设置为 `false` 来禁用此行为。

