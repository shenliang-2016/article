### 4.2. 外部化配置

Spring Boot 使您可以外部化配置，以便可以在不同环境中使用相同的应用程序代码。您可以使用属性文件，YAML文件，环境变量和命令行参数来外部化配置。属性值可以通过使用 `@Value` 注解直接注入到您的 bean 中，可以通过 Spring 的 `Environment` 抽象访问，也可以通过 `@ConfigurationProperties` [绑定到结构化对象](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-typesafe-configuration-properties) 。

Spring Boot 使用一个非常特殊的 `PropertySource` 顺序，该顺序被设计为允许合理地覆盖值。按以下顺序考虑属性：

1. 当开发者工具激活时首先考虑 `$HOME/.config/spring-boot` 文件夹中的 [Devtools global settings properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-globalsettings) 。
2. 你的测试类上的 [`@TestPropertySource`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/test/context/TestPropertySource.html) 注解。
3. 你的测试类上的 `properties` 属性。在 [`@SpringBootTest`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/test/context/SpringBootTest.html) 和 [test annotations for testing a particular slice of your application](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) 上可用。
4. 命令行参数。
5. 来自 `SPRING_APPLICATION_JSON` 的属性（嵌入在环境变量或系统属性中的内联JSON）。
6. `ServletConfig` 初始参数。
7. `ServletContext` 初始参数。
8. 来自 `java:comp/env` 的 JNDI 属性。
9. Java System 属性 (`System.getProperties()`)。
10. 操作系统环境变量。
11.  `RandomValuePropertySource` ，仅拥有在 `random.*` 中的属性。
12. 在你的打包的 jar 之外的 [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties)  (`application-{profile}.properties` 以及 YAML 变体)。
13. 打包到你的 jar 内部的 [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties)  (`application-{profile}.properties` 以及 YAML 变体)。
14. 你的打包的 jar 之外的应用属性 (`application.properties` 以及 YAML 变体)。
15. 打包到你的 jar 之内的应用属性 (`application.properties` 以及 YAML 变体)。
16. 你的 `@Configuration` 类上的 [`@PropertySource`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/annotation/PropertySource.html) 注解。请注意，在刷新应用程序上下文之前，不会将此类属性源添加到 `Environment` 中。现在配置某些属性（例如在刷新开始之前读取的 `logging.*` 和  `spring.main.*` ）为时已晚。
17. 默认属性 (通过设定 `SpringApplication.setDefaultProperties` 指定)。

为了提供一个具体的示例，假设您开发一个使用 `@name` 属性的 `@Component`，如以下示例所示：

```java
import org.springframework.stereotype.*;
import org.springframework.beans.factory.annotation.*;

@Component
public class MyBean {

    @Value("${name}")
    private String name;

    // ...

}
```

在您的应用程序类路径上（例如，在 jar 中），您可以有一个 `application.properties` 文件，该文件为 `name` 提供了合理的默认属性值。在新环境中运行时，可以在 jar 外部提供一个 `application.properties` 文件来覆盖 `name`。对于一次性测试，您可以使用特定的命令行开关启动（例如，`java -jar app.jar --name="Spring"`）。

> 可以在命令行中使用环境变量来提供 `SPRING_APPLICATION_JSON` 属性。 例如，您可以在 UN * X shell 中使用以下行：
>
> ````
> $ SPRING_APPLICATION_JSON='{"acme":{"name":"test"}}' java -jar myapp.jar
> ````
> 在前面的示例中，您最终在 Spring `Environment` 中获得了 `acme.name=test` 。您还可以在 System 属性中以 `spring.application.json` 的形式提供 JSON，如以下示例所示：
>
> ````
> $ java -Dspring.application.json='{"name":"test"}' -jar myapp.jar
> ````
> 您还可以使用命令行参数来提供 JSON，如以下示例所示：
> ````
> $ java -jar myapp.jar --spring.application.json='{"name":"test"}'
> ````
> 您还可以将 JSON 作为 JNDI 变量提供，如下所示：`java:comp/env/spring.application.json`。

