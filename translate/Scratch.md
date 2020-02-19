##### 自动配置的 REST 客户端

您可以使用 `@ RestClientTest` 来测试 REST 客户端。默认情况下，它会自动配置 Jackson，GSON 和 Jsonb 支持，配置 `RestTemplateBuilder`，并增加对 `MockRestServiceServer` 的支持。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。

>  由 `@RestClientTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

你希望测试的特定 beans 应该使用 `@RestClientTest` 注解的 `value` 或者 `components` 属性标示，如下面例子所示：

```java
@RestClientTest(RemoteVehicleDetailsService.class)
class ExampleRestClientTest {

    @Autowired
    private RemoteVehicleDetailsService service;

    @Autowired
    private MockRestServiceServer server;

    @Test
    void getVehicleDetailsWhenResultIsSuccessShouldReturnDetails()
            throws Exception {
        this.server.expect(requestTo("/greet/details"))
                .andRespond(withSuccess("hello", MediaType.TEXT_PLAIN));
        String greeting = this.service.callRestService();
        assertThat(greeting).isEqualTo("hello");
    }

}
```