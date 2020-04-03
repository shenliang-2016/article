##### 配置键

如果你的启动器提供配置键，为它们使用唯一的命名空间。特别的，切勿将你的配置键包含到 Spring Boot 使用的明明空间中（比如 `server`，`management`，`spring`  等等）。如果你使用相同的命名空间，你就可能随后意外修改这些命名空间，从而打破你的模块。根据经验，最佳实践是为你的配置键添加你所使用的命名空间前缀（比如，`acme`）。

确保所有的配置键中的每个属性都添加了 javadoc 文档说明，如下面例子所示：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    /**
     * Whether to check the location of acme resources.
     */
    private boolean checkLocation = true;

    /**
     * Timeout for establishing a connection to the acme server.
     */
    private Duration loginTimeout = Duration.ofSeconds(3);

    // getters & setters

}
```

> 您应该仅将简单文本与 `@ConfigurationProperties` 字段 Javadoc 一起使用，因为在将它们添加到 JSON 之前不会对其进行处理。

这里是一些我们默认遵循的规则以保持描述的一致性：

- 不要用 "The" 或者 "A" 开始描述。
- 对于 `boolean` 类型，使用 "Whether" 或者 "Enable" 开始描述。
- 对于基于集合的类型，使用 "Comma-separated list" 开始描述。
- 使用 `java.time.Duration` 而不是 `long` ，同时描述默认单位，如果不是毫秒。比如：如果没有使用时间间隔后缀，那么使用的就是秒。
- 描述中不要给出默认值，除非它必须在运行时确定。

确保 [触发元数据生成](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#configuration-metadata-annotation-processor) 以便 IDE 助手也能够对你的配置键产生作用。你可能希望浏览生成的元数据 (`META-INF/spring-configuration-metadata.json`) 以确保你的配置键都被准确地文档化了。在兼容的 IDE 中使用你的启动器也是检验这些元数据质量的好办法。