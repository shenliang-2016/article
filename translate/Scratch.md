##### 消息转换

[Same as in Spring WebFlux](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-codecs)

`spring-web` 模块包含 `HttpMessageConverter` 契约，通过 `InputStream` 读取 HTTP 请求的请求体，通过 `OutputStream` 将数据写入 HTTP 响应体。`HttpMessageConverter` 实例可以在服务端（比如，在 SpringMVC REST 控制器里）和客户端（比如，用在 `RestTemplate` 中）使用。

框架中提供了主要媒体（MIME）类型的具体实现，默认情况下，这些实现已在客户端通过 `RestTemplate` 注册，在服务端通过 `RequestMethodHandlerAdapter` 注册（请参阅 [配置消息转换器](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-config-message-converters)）。

`HttpMessageConverter` 实现在下一节中描述。对所有的消息转换器，都有一个默认的媒体类型，不过你可以通过设定 `supportedMediaTypes` bean 属性覆盖默认值。下面的表描述了各种实现：

| MessageConverter                         | Description                                                  |
| :--------------------------------------- | :----------------------------------------------------------- |
| `StringHttpMessageConverter`             | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求实例读取 `String` 实例，向 HTTP 响应写入 `String` 实例。默认地，该转换器支持所有的文本媒体类型（`text/*`）并以 `Content-Type`  值 `text/plain` 写入。 |
| `FormHttpMessageConverter`               | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入表单数据。默认情况下，此转换器读取和写入 `application/x-www-form-urlencoded` 媒体类型。 表单数据是从 `MultiValueMap<String, String>` 中读取并写入的。 |
| `ByteArrayHttpMessageConverter`          | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入字节数组。默认情况下，此转换器支持所有媒体类型（`*/*`），并使用 `application/octet-stream` 的 `Content-Type` 进行写入。您可以通过设置 `supportedMediaTypes` 属性并覆盖 `getContentType(byte[])` 来覆盖此属性。 |
| `MarshallingHttpMessageConverter`        | 一个 `HttpMessageConverter` 实现，可以通过使用来自 `org.springframework.oxm` 包的 Spring 的 `Marshaller` 和 `Unmarshaller` 抽象来读写 XML。该转换器需要使用 `Marshaller` 和 `Unmarshaller` 才能工作。您可以通过构造函数或 bean 属性注入它们。默认情况下，此转换器支持 `text/xml` 和 `application/xml`。 |
| `MappingJackson2HttpMessageConverter`    | 一个 `HttpMessageConverter` 实现，可以通过使用 Jackson 的 `ObjectMapper` 来读取和写入 JSON。您可以根据需要使用 Jackson 提供的注解来自定义 JSON 映射。当需要进一步控制时（对于需要为特定类型提供自定义 JSON 序列化器/反序列化器的情况），可以通过 `ObjectMapper` 属性注入自定义 `ObjectMapper`。默认情况下，此转换器支持 `application/json`。 |
| `MappingJackson2XmlHttpMessageConverter` | 一个 `HttpMessageConverter` 实现，可以使用 [Jackson XML](https://github.com/FasterXML/jackson-dataformat-xml) 扩展名的 `XmlMapper` 来读写 XML。您可以根据需要使用 JAXB 或 Jackson 提供的注解来自定义 XML 映射。当需要进一步控制时（对于需要为特定类型提供自定义 XML 序列化器/反序列化器的情况），可以通过 `ObjectMapper` 属性注入自定义 `XmlMapper`。默认情况下，此转换器支持 `application/xml`。 |
| `SourceHttpMessageConverter`             | `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入 `javax.xml.transform.Source`。仅支持 `DOMSource`，`SAXSource` 和 `StreamSource`。默认情况下，此转换器支持 `text/xml` 和 `application/xml`。 |
| `BufferedImageHttpMessageConverter`      | 一个`HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入 `java.awt.image.BufferedImage`。该转换器读取和写入 Java I/O API 支持的媒体类型。 |

##### Jackson JSON 视图

您可以指定 [Jackson JSON View](https://www.baeldung.com/jackson-json-view-annotation) 以仅序列化对象属性的一部分，如以下示例所示：

```java
MappingJacksonValue value = new MappingJacksonValue(new User("eric", "7!jd#h23"));
value.setSerializationView(User.WithoutPasswordView.class);

RequestEntity<MappingJacksonValue> requestEntity =
    RequestEntity.post(new URI("https://example.com/user")).body(value);

ResponseEntity<String> response = template.exchange(requestEntity, String.class);
```

##### Multipart

要发送多部分数据，您需要提供一个 `MultiValueMap <String, Object>`，其值可以是部分内容的 `Object`，文件部分的 `Resource` 或带首部的部分内容的 `HttpEntity`。例如：

```java
    MultiValueMap<String, Object> parts = new LinkedMultiValueMap<>();

    parts.add("fieldPart", "fieldValue");
    parts.add("filePart", new FileSystemResource("...logo.png"));
    parts.add("jsonPart", new Person("Jason"));

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_XML);
    parts.add("xmlPart", new HttpEntity<>(myBean, headers));
```

在大多数情况下，您不必为每个部分指定 `Content-Type`。内容类型是根据要序列化的 `HttpMessageConverter` 自动确定的，对于基于文件扩展名的 `Resource` 则是自动确定的。如有必要，您可以显式地为 `MediaType` 提供一个 `HttpEntity` 包装器。

一旦 `MultiValueMap` 准备就绪，您可以将其传递给 `RestTemplate`，如下所示：

```java
    MultiValueMap<String, Object> parts = ...;
    template.postForObject("https://example.com/upload", parts, Void.class);
```

如果 `MultiValueMap` 包含至少一个非 `String` 值，则 `FormHttpMessageConverter` 将 `Content-Type` 设置为 `multipart/form-data`。如果 `MultiValueMap` 具有 `String` 值，则 `Content-Type` 默认为 `application/x-www-form-urlencoded`。如有必要，还可以显式设置 `Content-Type`。

#### 1.8.2 使用 `AsyncRestTemplate` (已废弃)

`AsyncRestTemplate` 已弃用。对于所有您可能考虑使用 `AsyncRestTemplate` 的场景，请使用 [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 代替。

