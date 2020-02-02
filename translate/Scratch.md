### 4.17. 发送邮件

Spring 框架通过使用 `JavaMailSender` 接口提供了用于发送电子邮件的简单抽象，Spring Boot 为它提供了自动配置以及启动程序模块。

> 参考 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#mail) 了解 `JavaMailSender` 使用方法的详细介绍。

如果有 `spring.mail.host` 和相关的库（由 `spring-boot-starter-mail` 定义）可用，则如果不存在默认的 `JavaMailSender`，则会创建该库。可以通过 `spring.mail` 命名空间中的配置项进一步定制发送者。参见 [`MailProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/mail/MailProperties.java) 以获取更多详细信息。

特别是，某些默认超时值是无限的，您可能需要更改该值，以避免线程被无响应的邮件服务器阻止，如以下示例所示：

```properties
spring.mail.properties.mail.smtp.connectiontimeout=5000
spring.mail.properties.mail.smtp.timeout=3000
spring.mail.properties.mail.smtp.writetimeout=5000
```

也可以使用来自 JNDI 的现有 `Session` 来配置 `JavaMailSender`：

```properties
spring.mail.jndi-name=mail/Session
```

设置 `jndi-name` 时，它优先于所有其他与 `Session` 相关的设置。

