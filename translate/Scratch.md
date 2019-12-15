## 6. Email

本章节描述如何使用 Spring 框架发送电子邮件。

> 库依赖
>
> 下面的 JAR 需要放在你的应用的类路径下以便使用 Spring 框架的电子邮件类库：
>
> -  [JavaMail](https://javaee.github.io/javamail/) 类库
>
> 此类库在网络上可以自由使用 — 比如，在 Maven 中央仓库中的 `com.sun.mail:javax.mail`。

Spring 框架提供了一个很好用的工具类库来发送邮件，将你从特定于底层邮件系统的技术细节中解脱出来，该类库同时还接管了客户端的底层资源处理。

`org.springframework.mail` 包是 Spring 框架电子邮件支持的根级别包。发送邮件的中央接口是 `MailSender` 接口。一个简单的值对象封装了简单邮件的属性，比如 `from` 和 `to` (当然还有很多别的属性)，就是 `SimpleMailMessage` 类。该包还包含受检查异常层级结构提供了低层级邮件系统异常的高层抽象，其根异常是 `MailException` 。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/mail/MailException.html) 了解更多有关邮件异常层级结构的信息。

`org.springframework.mail.javamail.JavaMailSender` 接口添加了特定的 JavaMail 特性，比如将 MIME 消息支持添加到 `MailSender` 接口（继承该接口）。`JavaMailSender` 也提供了一个名为 `org.springframework.mail.javamail.MimeMessagePreparator` 的回调接口来准备 `MimeMessage`。

