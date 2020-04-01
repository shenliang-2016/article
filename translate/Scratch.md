##### Property 条件

通过 `@ConditionalOnProperty` 注解，可以基于 Spring Environment 属性包含配置。使用`prefix`和`name`属性来指定应检查的属性。默认情况下，匹配存在且不等于 `false` 的任何属性。您还可以使用 `havingValue` 和 `matchIfMissing` 属性来创建更高级的检查。

##### Resource 条件

`@ConditionalOnResource` 注解仅在存在特定资源时才包括配置。可以使用通常的 Spring 约定来指定资源，如以下示例所示： `file:/home/user/test.dat` 。

##### Web Application 条件

通过 `@ConditionalOnWebApplication` 和 `@ConditionalOnNotWebApplication` 注解，可以根据应用程序是否为 Web 应用程序来包含配置。基于 Servlet 的 Web 应用程序是任何使用 Spring `WebApplicationContext`，定义 `session` 作用域或具有 `ConfigurableWebEnvironment` 的应用程序。响应式 Web 应用程序是使用 `ReactiveWebApplicationContext` 或具有 `ConfigurableReactiveWebEnvironment` 的任何应用程序。

##### SpEL Expression 条件

`@ConditionalOnExpression` 注解允许根据 [SpEL expression](https://docs.spring.io/spring/docs/5.2.5.RELEASE/spring-framework-reference/core.html#expressions) 的结果来决定是否包含配置。