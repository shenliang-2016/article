### 3.7. WebTestClient

`WebTestClient` 是包装 [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 的薄壳。它可以执行请求并公开专用的API来验证响应。`WebTestClient` 通过使用 [模拟请求和响应](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-web-reactive) 绑定到 WebFlu x应用程序，或者它可以通过 HTTP 连接测试任何 Web 服务器。

> Kotlin 用户：参考 [this section](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/languages.html#kotlin-webtestclient-issue) 获取有关使用 `WebTestClient` 的更多信息。

#### 3.7.1. 设置

要创建一个 `WebTestClient` ，必须选择几个服务器设置选项之一。实际上，您是在配置要绑定到的 WebFlux 应用程序，还是使用 URL 连接到正在运行的服务器。

##### 绑定到控制器

以下示例说明如何创建服务器设置以一次测试一个 `@Controller` ：

```
    client = WebTestClient.bindToController(new TestController()).build();
```

上例加载了 [WebFlux Java配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-config) 并注册了给定的控制器。通过使用模拟请求和响应对象，可以在没有 HTTP 服务器的情况下测试生成的 WebFlux 应用程序。构建器上有更多方法可以定制默认 WebFlux Java 配置。

##### 绑定到 Router Function

下面的例子展示了如何从 [RouterFunction](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-fn) 配置服务器：

```
    RouterFunction<?> route = ...
    client = WebTestClient.bindToRouterFunction(route).build();
```

在内部，配置被传递到 `RouterFunctions.toWebHandler`。通过使用模拟请求和响应对象，可以在没有 HTTP 服务器的情况下测试生成的 WebFlux 应用程序。

##### 绑定到 `ApplicationContext`

以下示例显示了如何从应用程序的 Spring 配置或其一部分来设置服务器：

```
    @RunWith(SpringRunner.class)
    @ContextConfiguration(classes = WebConfig.class) 
    public class MyTests {

        @Autowired
        private ApplicationContext context; 

        private WebTestClient client;

        @Before
        public void setUp() {
            client = WebTestClient.bindToApplicationContext(context).build(); 
        }
    }
```

在内部，配置被传递到 `WebHttpHandlerBuilder` 以建立请求处理链。有关更多详细信息，请参见 [WebHandler API](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-web-handler-api) 。通过使用模拟请求和响应对象，可以在没有 HTTP 服务器的情况下测试生成的 WebFlux 应用程序。

##### 绑定到服务器

以下服务器设置选项使您可以连接到正在运行的服务器：

```
    client = WebTestClient.bindToServer().baseUrl("http://localhost:8080").build();
```

##### 客户端构建器

除了前面描述的服务器设置选项之外，您还可以配置客户端选项，包括基本URL，默认首部，客户端过滤器等。这些选项可以在 `bindToServer` 之后使用。对于所有其他配置，您需要使用 `configureClient()` 从服务器配置转换为客户端配置，如下所示：

```
    client = WebTestClient.bindToController(new TestController())
            .configureClient()
            .baseUrl("/test")
            .build();
```

#### 3.7.2. 编写测试

`WebTestClient` 提供的 API 与 [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 相同，是使用 `exchange()` 执行请求的关键。在 `exchange()` 之后，是一个链式的的 API 流程，用于验证响应。

通常，首先声明响应状态和首部，如下所示：

```
    client.get().uri("/persons/1")
            .accept(MediaType.APPLICATION_JSON_UTF8)
            .exchange()
            .expectStatus().isOk()
            .expectHeader().contentType(MediaType.APPLICATION_JSON_UTF8)
            // ...
```

然后，您指定如何解码和使用响应主体：

- `expectBody(Class <T>)`：解码为单个对象。

- `expectBodyList(Class <T>)`：解码并将对象收集到 `List <T>`。

- `expectBody()`：将 [JSON Content](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#webtestclient-json) 或一个空的正文解码为 `byte[]`。

然后，您可以对响应主体使用内置的断言。下面的示例展示了一种方法：

```
    client.get().uri("/persons")
            .exchange()
            .expectStatus().isOk()
            .expectBodyList(Person.class).hasSize(3).contains(person);
```

您还可以超越内置的断言并创建自己的断言，如以下示例所示：

```
    client.get().uri("/persons/1")
            .exchange()
            .expectStatus().isOk()
            .expectBody(Person.class)
            .consumeWith(result -> {
                // custom assertions (e.g. AssertJ)...
            });
```

您还可以退出工作流程并获得结果，如下所示：

```
    EntityExchangeResult<Person> result = client.get().uri("/persons/1")
            .exchange()
            .expectStatus().isOk()
            .expectBody(Person.class)
            .returnResult();
```

> 当你需要解码为一个使用范型的目标类型时，搜寻该接收 [`ParameterizedTypeReference`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/core/ParameterizedTypeReference.html) 而不是 `Class<T>` 的重载方法。

##### 无内容

如果响应没有内容（或者您不在乎），则使用 `Void.class`，以确保释放资源。以下示例显示了如何执行此操作：

```
    client.get().uri("/persons/123")
            .exchange()
            .expectStatus().isNotFound()
            .expectBody(Void.class);
```

或者，如果要断言没有响应内容，则可以使用类似于以下内容的代码：

```
    client.post().uri("/persons")
            .body(personMono, Person.class)
            .exchange()
            .expectStatus().isCreated()
            .expectBody().isEmpty();
```

##### JSON 内容

当使用 `expectBody()` 时，响应以 `byte[]` 的形式被使用。这对于原始内容声明很有用。例如，您可以使用 [JSONAssert](https://jsonassert.skyscreamer.org/) 来验证 JSON 内容，如下所示：

```
    client.get().uri("/persons/1")
            .exchange()
            .expectStatus().isOk()
            .expectBody()
            .json("{\"name\":\"Jane\"}")
```

你也可以使用 [JSONPath](https://github.com/jayway/JsonPath) 表达式，如下所示：

```
    client.get().uri("/persons")
            .exchange()
            .expectStatus().isOk()
            .expectBody()
            .jsonPath("$[0].name").isEqualTo("Jane")
            .jsonPath("$[1].name").isEqualTo("Jason");
```

##### 流式响应

要测试无限流（例如，“ `text/event-stream`” 或 “`application/stream+json`”），您需要在响应状态和首部断言之后立即退出链接的 API（使用“`returnResult`”），如以下示例所示：

```
    FluxExchangeResult<MyEvent> result = client.get().uri("/events")
            .accept(TEXT_EVENT_STREAM)
            .exchange()
            .expectStatus().isOk()
            .returnResult(MyEvent.class);
```

现在，您可以使用 `Flux <T>`，在解码后的对象出现时声明它们，然后在达到测试目标时在某个时候取消。我们建议使用 “`reactor-test`” 模块中的 “`StepVerifier`” 来执行此操作，如以下示例所示：

```
    Flux<Event> eventFux = result.getResponseBody();

    StepVerifier.create(eventFlux)
            .expectNext(person)
            .expectNextCount(4)
            .consumeNextWith(p -> ...)
            .thenCancel()
            .verify();
```

##### 请求体

当涉及到构建请求时，`WebTestClient` 提供了与 `WebClient` 相同的 API，实现主要是简单的传递。有关如何操作的示例，请参见 [WebClient文档](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client-body) 准备带有正文的请求，包括提交表单数据，多部分请求等。

## 4. 更多资源

参考以下资源获取有关测试的更多信息：

- [JUnit](https://www.junit.org/): “面向程序员的Java测试框架”. 由 Spring Framework 在其测试套件中使用。
- [TestNG](http://testng.org/): 一个受 JUnit 启发的测试框架，并添加了对注解，测试组，数据驱动的测试，分布式测试和其他功能的支持。
- [AssertJ](https://joel-costigliola.github.io/assertj/): “Java的断言”, 包括对 Java 8 lambda，流和其他功能的支持。
- [Mock Objects](https://en.wikipedia.org/wiki/Mock_Object): 维基百科上的文章。
- [MockObjects.com](http://www.mockobjects.com/): 专门用于模拟对象的网站，一种用于在测试驱动的开发中改进代码设计的技术。
- [Mockito](https://mockito.github.io/): 基于 [Test Spy](http://xunitpatterns.com/Test Spy.html) 模式的Java 模拟类库。
- [EasyMock](http://easymock.org/): “通过使用Java的代理机制动态生成接口来为接口（以及通过类扩展的对象）提供Mock对象” 的 Java 类库。Spring框架在其测试套件中使用。
- [JMock](http://jmock.org/): 支持带有模拟对象的Java代码的测试驱动开发的库。
- [DbUnit](http://dbunit.sourceforge.net/): 针对数据库驱动的JUnit扩展项目，也可与Ant和Maven一起使用。除其他特性之外，它使数据库在测试运行之间进入已知状态。
- [The Grinder](http://grinder.sourceforge.net/): Java负载测试框架。