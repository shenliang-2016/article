##### 排除测试配置

如果您的应用程序使用组件扫描（例如，如果使用 `@SpringBootApplication` 或 `@ComponentScan` ），则可能会偶然发现为局部创建的仅为特定测试使用的配置类被全局应用了。

正如我们 [之前所见](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config )，可以在测试的内部类上使用 `@TestConfiguration` 来自定义主要配置。如果将 `@TestConfiguration` 放在顶级类上，则表明 `src/test/java` 中的类不应通过扫描来拾取。然后，可以在需要的位置显式导入该类，如以下示例所示：

```java
@SpringBootTest
@Import(MyTestsConfiguration.class)
class MyTests {

    @Test
    void exampleTest() {
        ...
    }

}
```

> 如果您直接使用 `@ComponentScan`（即不是通过 `@SpringBootApplication`），则需要向其中注册 `TypeExcludeFilter`。有关详细信息，请参见 [Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/context/TypeExcludeFilter.html)。

