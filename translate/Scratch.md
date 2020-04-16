#### 5.4.2. 禁用 JMX 端点

如果你不想通过 JMX 暴露端点，你可以设置 `management.endpoints.jmx.exposure.exclude` 属性为 `*`，如下面例子所示：

```properties
management.endpoints.jmx.exposure.exclude=*
```

#### 5.4.3. 在 HTTP 上为 JMX 使用 Jolokia

Jolokia 是一种 JMX-HTTP 桥接技术，提供了另一种访问 JMX beans 的方法。为了使用 Jolokia，引入 `org.jolokia:jolokia-core` 依赖。比如，使用 Maven，你需要添加下面的依赖：

```xml
<dependency>
    <groupId>org.jolokia</groupId>
    <artifactId>jolokia-core</artifactId>
</dependency>
```

然后 Jolokia 端点就可以通过添加 `jolokia` 或者 `*` 到 `management.endpoints.web.exposure.include` 属性而暴露。这样你就可以通过使用 `/actuator/jolokia` 在你的管理 HTTP 服务器上访问它们。

##### 自定义 Jolokia

Jolokia 包含一些设定，你可以通过设定 servlet 参数来配置它们。在 Spring Boot 中，你可以使用 `application.properties` 文件。为了做到这一点，为参数名称添加前缀 `management.endpoint.jolokia.config.`，如下面例子所示：

```properties
management.endpoint.jolokia.config.debug=true
```

##### 禁用 Jolokia

如果你使用 Jolokia 但不希望 Spring Boot 配置它，设定 `management.endpoint.jolokia.enabled` 属性为 `false`，如下所示：

```properties
management.endpoint.jolokia.enabled=false
```

