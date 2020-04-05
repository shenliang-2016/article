##### Servlet 端点

通过实现带有 `@ServletEndpoint` 注解、同时也实现了 `Supplier` 的类，`Servlet` 可以作为端点公开。Servlet 端点提供了与 Servlet 容器的更深层集成，但以可移植性为代价。它们旨在用于将现有的 `Servlet` 公开为端点。对于新的端点，应尽可能使用 `@Endpoint` 和 `@WebEndpoint` 注解。

##### Controller 端点

`@ControllerEndpoint` 和 `@RestControllerEndpoint` 可用于实现仅由 Spring MVC 或 Spring WebFlux 公开的端点。方法使用 Spring MVC 和 Spring WebFlux 的标准注解（例如，`@RequestMapping` 和 `@GetMapping`）进行映射，端点的 ID 用作路径的前缀。控制器端点提供了与 Spring web 框架的更深层集成，但以可移植性为代价。尽可能使用 `@Endpoint` 和 `@WebEndpoint` 注解。