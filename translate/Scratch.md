##### 模拟并监视 Beans

运行测试时，有时有必要在应用程序上下文中模拟某些组件。例如，您可能在开发过程中无法使用某些远程服务的门面。当您要模拟在实际环境中可能难以触发的故障时，模拟功能也很有用。

Spring Boot 包含一个 `@MockBean` 注解，可用于为 `ApplicationContext` 内部的 bean 定义一个 Mockito 模拟。您可以使用注解添加新的 bean 或替换单个现有的 bean 定义。注解可以直接用于测试类，测试中的字段或 `@Configuration` 类和字段。在字段上使用时，还将注入创建的模拟的实例。每种测试方法后，模拟 beans 都会自动重置。

> 如果您的测试使用 Spring Boot 的测试注解之一（例如 `@SpringBootTest` ），则会自动启用此功能。要以其他方式使用此功能，必须明确添加侦听器，如以下示例所示：
>
> ````java
> @TestExecutionListeners(MockitoTestExecutionListener.class)
> ````

以下示例使用模拟实现替换了现有的 `RemoteService` bean：

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

> `@MockBean` 不能用于模拟应用程序上下文刷新期间执行的 bean 的行为。到执行测试时，应用程序上下文刷新已完成，并且配置模拟行为为时已晚。我们建议在这种情况下使用 `@Bean` 方法创建和配置模拟。

另外，您可以使用 `@SpyBean` 来将任何现有的 bean 与 Mockito 的 `spy` 一起包装。有关完整的详细信息，请参见 [Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/test/mock/mockito/SpyBean.html)。

> CGLib 代理（例如为作用域范围内的 bean 创建的代理）将代理的方法声明为 `final`。这会阻止 Mockito 正常运行，因为它无法在其默认配置中模拟或监视 `final` 方法。如果您想对这样的 bean 进行模拟或监视，请通过在应用程序的测试依赖项中添加 `org.mockito:mockito-inline` 来将 Mockito 配置为使用其内联模拟程序。这使 Mockito 可以模拟并监视 `final` 方法。

> Spring 的测试框架在测试之间缓存应用程序上下文，并为共享相同配置的测试重用上下文，而 `@MockBean` 或 `@SpyBean` 的使用会影响缓存键，这很可能会增加上下文数量。

> 如果您使用 `@SpyBean` 来监视通过名称引用参数的 `@Cacheable` 方法，则您的应用程序必须使用 `-parameters` 进行编译。这样可以确保一旦侦察到 bean，就可以将参数名称用于缓存基础结构。

