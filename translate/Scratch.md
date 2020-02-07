### 4.24. 使用 JMX 的监控和管理

Java 管理扩展（JMX）提供了监视和管理应用程序的标准机制。Spring Boot 将最适合的 `MBeanServer` 公开为ID为 `mbeanServer` 的 bean。带有 Spring JMX 注解（`@ManagedResource`，`@ManagedAttribute` 或 `@ManagedOperation`）的任何 bean 都可以使用。

如果您的平台提供标准的 `MBeanServer`，则 Spring Boot 将使用该标准，并在必要时默认使用 VM `MBeanServer`。如果全部失败，将创建一个新的 `MBeanServer`。

参见 [`JmxAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jmx/JmxAutoConfiguration.java) 类以获取更多详细信息。