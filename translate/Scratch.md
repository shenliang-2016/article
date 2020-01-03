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
12. [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) outside of your packaged jar (`application-{profile}.properties` and YAML variants).
13. [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) packaged inside your jar (`application-{profile}.properties` and YAML variants).
14. Application properties outside of your packaged jar (`application.properties` and YAML variants).
15. Application properties packaged inside your jar (`application.properties` and YAML variants).
16. [`@PropertySource`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/annotation/PropertySource.html) annotations on your `@Configuration` classes. Please note that such property sources are not added to the `Environment` until the application context is being refreshed. This is too late to configure certain properties such as `logging.*` and `spring.main.*` which are read before refresh begins.
17. Default properties (specified by setting `SpringApplication.setDefaultProperties`).

To provide a concrete example, suppose you develop a `@Component` that uses a `name` property, as shown in the following example:

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

On your application classpath (for example, inside your jar) you can have an `application.properties` file that provides a sensible default property value for `name`. When running in a new environment, an `application.properties` file can be provided outside of your jar that overrides the `name`. For one-off testing, you can launch with a specific command line switch (for example, `java -jar app.jar --name="Spring"`).

> The `SPRING_APPLICATION_JSON` properties can be supplied on the command line with an environment variable. For example, you could use the following line in a UN*X shell:
> ````
> $ SPRING_APPLICATION_JSON='{"acme":{"name":"test"}}' java -jar myapp.jar
> ````
> In the preceding example, you end up with `acme.name=test` in the Spring `Environment`. You can also supply the JSON as `spring.application.json` in a System property, as shown in the following example:
> ````
> $ java -Dspring.application.json='{"name":"test"}' -jar myapp.jar
> ````
> You can also supply the JSON by using a command line argument, as shown in the following example:
> ````
> $ java -jar myapp.jar --spring.application.json='{"name":"test"}'
> ````
> You can also supply the JSON as a JNDI variable, as follows: `java:comp/env/spring.application.json`.