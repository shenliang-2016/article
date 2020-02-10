##### 自定义 WebTestClient

要自定义 `WebTestClient` bean，请配置 `WebTestClientBuilderCustomizer` bean。使用 `WebTestClient.Builder` 调用任何此类 bean，用于创建 `WebTestClient`。

##### 使用 JMX

由于测试上下文框架缓存上下文，因此默认情况下禁用 JMX，以防止相同的组件在同一域上注册。如果这样的测试需要访问 `MBeanServer`，请考虑将其标记为脏：

```java
@ExtendWith(SpringExtension.class)
@SpringBootTest(properties = "spring.jmx.enabled=true")
@DirtiesContext
class SampleJmxTests {

    @Autowired
    private MBeanServer mBeanServer;

    @Test
    void exampleTest() {
        // ...
    }

}
```

