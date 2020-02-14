##### 自动配置的测试

Spring Boot 的自动配置系统适用于应用程序，但有时对于测试来说可能有点过多。它通常仅有助于加载测试应用程序“切片”所需的配置部分。例如，您可能想测试 Spring MVC 控制器是否正确映射了 URL，并且不想在这些测试中涉及数据库调用，或者您想测试 JPA 实体，并且当您使用 JPA 实体时，您对 Web 层不感兴趣。

`spring-boot-test-autoconfigure` 模块包含许多注解，可用于自动配置此类“切片”。它们中的每一个都以类似的方式工作，提供了一个可加载 `ApplicationContext` 的 `@…Test` 注解和一个或多个可用于自定义自动配置设置的 `@AutoConfigure…` 注解。

> 每个切片将组件扫描范围限制为适当的组件，并加载一组非常受限制的自动配置类。如果您需要排除其中之一，则大多数 `@…Test` 注解都提供了 `excludeAutoConfiguration` 属性。或者，您可以使用 `@ImportAutoConfiguration#exclude`。
>

> 不支持在一个测试中使用多个 `@…Test` 注解来包含多个“切片”。如果需要多个“切片”，请选择一个 `@…Test` 注解，并手动添加其他“切片”的 `@AutoConfigure…` 注解。

> 也可以将 `@AutoConfigure…` 注解与标准的 `@SpringBootTest` 注解一起使用。如果您对“切片”应用程序不感兴趣，但需要一些自动配置的测试 bean，则可以使用此组合。

