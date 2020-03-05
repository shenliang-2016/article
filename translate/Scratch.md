### 4.27. Web Services

Spring Boot 提供 Web Services 自动配置，你所需要做的就只是定义你的 `Endpoints`。

[Spring Web Services 特性](https://docs.spring.io/spring-ws/docs/3.0.8.RELEASE/reference/) 能够很方便地通过 `spring-boot-starter-webservices` 模块访问。

`SimpleWsdl11Definition` 和 `SimpleXsdSchema` beans 能够自动创建，分别用于 WSDLs 和 XSDs 。为了实现这一点，配置它们的位置，如下面例子所示：

```properties
spring.webservices.wsdl-locations=classpath:/wsdl
```