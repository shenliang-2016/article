##### 模拟并监视 Beans

运行测试时，有时有必要在应用程序上下文中模拟某些组件。例如，您可能在开发过程中无法使用某些远程服务的门面。当您要模拟在实际环境中可能难以触发的故障时，模拟功能也很有用。

Spring Boot 包含一个 `@MockBean` 注解，可用于为 `ApplicationContext` 内部的 bean 定义一个 Mockito 模拟。您可以使用注解添加新的 bean 或替换单个现有的 bean 定义。注解可以直接用于测试类，测试中的字段或 `@Configuration` 类和字段。在字段上使用时，还将注入创建的模拟的实例。每种测试方法后，模拟 beans 都会自动重置。

> If your test uses one of Spring Boot’s test annotations (such as `@SpringBootTest`), this feature is automatically enabled. To use this feature with a different arrangement, a listener must be explicitly added, as shown in the following example:
>
> ````java
> @TestExecutionListeners(MockitoTestExecutionListener.class)
> ````

The following example replaces an existing `RemoteService` bean with a mock implementation:

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.context.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;

@SpringBootTest
class MyTests {

    @MockBean
    private RemoteService remoteService;

    @Autowired
    private Reverser reverser;

    @Test
    void exampleTest() {
        // RemoteService has been injected into the reverser bean
        given(this.remoteService.someCall()).willReturn("mock");
        String reverse = reverser.reverseSomeCall();
        assertThat(reverse).isEqualTo("kcom");
    }

}
```

> `@MockBean` cannot be used to mock the behavior of a bean that’s exercised during application context refresh. By the time the test is executed, the application context refresh has completed and it is too late to configure the mocked behavior. We recommend using a `@Bean` method to create and configure the mock in this situation.

Additionally, you can use `@SpyBean` to wrap any existing bean with a Mockito `spy`. See the [Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/test/mock/mockito/SpyBean.html) for full details.

> CGLib proxies, such as those created for scoped beans, declare the proxied methods as `final`. This stops Mockito from functioning correctly as it cannot mock or spy on `final` methods in its default configuration. If you want to mock or spy on such a bean, configure Mockito to use its inline mock maker by adding `org.mockito:mockito-inline` to your application’s test dependencies. This allows Mockito to mock and spy on `final` methods.

> While Spring’s test framework caches application contexts between tests and reuses a context for tests sharing the same configuration, the use of `@MockBean` or `@SpyBean` influences the cache key, which will most likely increase the number of contexts.

> If you are using `@SpyBean` to spy on a bean with `@Cacheable` methods that refer to parameters by name, your application must be compiled with `-parameters`. This ensures that the parameter names are available to the caching infrastructure once the bean has been spied upon.