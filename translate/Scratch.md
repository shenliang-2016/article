##### 接收输入

端点上的操作通过它们的参数接收输入。当通过 web 暴露时，这些参数的值取自 URL 的查询参数以及 JSON 请求体。当通过 JMX 暴露时，参数被映射到 MBean 操作的参数。参数默认是强制需要的。通过使用 `@org.springframework.lang.Nullable` 注解修饰它们可以将其变为可选的。

JSON 请求体中的每个根属性都能够映射到端点参数。考虑下面的 JSON 请求体：

```json
{
    "name": "test",
    "counter": 42
}
```

这可以被用于调用一个携带 `String name` 和 `int counter` 参数的写操作。

> 由于端点与技术无关，因此只能在方法签名中指定简单类型。特别地，不支持使用自定义类型声明一个单独的参数来定义 `name` 和 `counter` 属性。

> 为了使输入映射到操作方法的参数，实现端点的 Java 代码应使用 `-parameters` 进行编译，而实现端点的 Kotlin 代码应使用 `-java-parameters` 进行编译。如果您使用的是 Spring Boot 的 Gradle 插件，或者您使用的是 Maven 和 `spring-boot-starter-parent`，则此操作会自动发生。