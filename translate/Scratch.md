###### 输入类型转换

传递给端点操作方法的参数，如果必要，会自动被转换为需要的数据类型。在调用操作方法之前，通过 JMX 或者 HTTP 请求接收的输入被转换为需要的数据类型，使用一个  `ApplicationConversionService` 实例。或者任何由 `@EndpointConverter` 修饰的 `Converter` 或者 `GenericConverter` beans。

##### 自定义 Web 端点

一个 `@Endpoint`, `@WebEndpoint`, 或者 `@EndpointWebExtension` 上的操作会自动通过 HTTP 暴露，使用 Jersey, Spring MVC, 或者 Spring WebFlux。如果 Jersey 和 Spring MVC 都可用， Spring MVC 将被优先使用。

###### Web 端点请求谓词

请求谓词会为 web 暴露端点上的每个操作自动生成。