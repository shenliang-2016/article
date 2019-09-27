您可以使用客户端测试来测试内部使用 `RestTemplate` 的代码。这个想法是声明预期的请求并提供“存根”响应，以便您可以专注于隔离测试代码（即，不运行服务器）。以下示例显示了如何执行此操作：

```java
RestTemplate restTemplate = new RestTemplate();

MockRestServiceServer mockServer = MockRestServiceServer.bindTo(restTemplate).build();
mockServer.expect(requestTo("/greeting")).andRespond(withSuccess());

// Test code that uses the above RestTemplate ...

mockServer.verify();
```

在前面的示例中，`MockRestServiceServer`（客户端 REST 测试的核心类）使用自定义的 `ClientHttpRequestFactory` 配置 `RestTemplate`，该 `CustomerHttpRequestFactory` 根据期望断言实际的请求并返回“存根”响应。在这种情况下，我们希望有一个请求 `/greeting`，并希望返回一个包含 `text/plain` 内容的 200 响应。我们可以根据需要定义其他预期的请求和存根响应。当我们定义期望的请求和存根响应时，`RestTemplate` 可以照常在客户端代码中使用。在测试结束时，可以使用 `mockServer.verify()` 来验证是否满足所有期望。

默认情况下，请求应按声明的期望顺序进行。您可以在构建服务器时设置 `ignoreExpectOrder` 选项，在这种情况下，将检查所有期望（按顺序）以找到给定请求的匹配项。这意味着允许请求以任何顺序出现。以下示例使用 `ignoreExpectOrder`：

```java
server = MockRestServiceServer.bindTo(restTemplate).ignoreExpectOrder(true).build();
```

即使默认情况下无顺序请求，每个请求也只能执行一次。 `expect` 方法提供了一个重载的变体，该变体接受指定计数范围的 `ExpectedCount` 参数（例如，`once`，`manyTimes`，`max`，`min`，`between` 等）。以下示例使用 `times`：

```java
RestTemplate restTemplate = new RestTemplate();

MockRestServiceServer mockServer = MockRestServiceServer.bindTo(restTemplate).build();
mockServer.expect(times(2), requestTo("/something")).andRespond(withSuccess());
mockServer.expect(times(3), requestTo("/somewhere")).andRespond(withSuccess());

// ...

mockServer.verify();
```

请注意，如果未设置 `ignoreExpectOrder`（默认设置），因此要求按声明顺序进行请求，则该顺序仅适用于所有预期请求中的第一个。例如，如果期望 `/something` 两次，然后是 `/somewhere` 三次，那么在请求 `/somewhere` 之前应该先请求 `/something`，但是除了随后的 `/something` 和 `/somewhere`，请求可以随时发出。

作为上述所有方法的替代，客户端测试支持还提供了 `ClientHttpRequestFactory` 实现，您可以将其配置为 `RestTemplate` 以将其绑定到 `MockMvc` 实例。这样就可以使用实际的服务器端逻辑来处理请求，而无需运行服务器。以下示例显示了如何执行此操作：

```java
MockMvc mockMvc = MockMvcBuilders.webAppContextSetup(this.wac).build();
this.restTemplate = new RestTemplate(new MockMvcClientHttpRequestFactory(mockMvc));

// Test code that uses the above RestTemplate ...
```

##### 静态导入

与服务器端测试一样，用于客户端测试的 API 需要进行一些静态导入。通过搜索 `MockRest*` 可以很容易地找到它们。Eclipse 用户应在 Java→编辑器→Content Assist→收藏夹下的Eclipse首选项中，将 `MockRestRequestMatchers.*` 和 `MockRestResponseCreators.*` 作为“最喜欢的静态成员”添加。这样可以在键入静态方法名称的第一个字符后使用内容辅助。其他IDE（例如IntelliJ）可能不需要任何其他配置。请自行检查你的环境是否支持静态成员上的代码完成。

##### 客户端 REST 测试的更多示例

Spring MVC Test 自己的测试包括 [example tests](https://github.com/spring-projects/spring-framework/tree/master/spring-test/src/test/java/org/springframework/test/web/client/samples) 的客户端 REST 测试。

