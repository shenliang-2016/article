##### 消息转换

[Same as in Spring WebFlux](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-codecs)

`spring-web` 模块包含 `HttpMessageConverter` 契约，通过 `InputStream` 读取 HTTP 请求的请求体，通过 `OutputStream` 将数据写入 HTTP 响应体。`HttpMessageConverter` 实例可以在服务端（比如，在 SpringMVC REST 控制器里）和客户端（比如，用在 `RestTemplate` 中）使用。

框架中提供了主要媒体（MIME）类型的具体实现，默认情况下，这些实现已在客户端通过 `RestTemplate` 注册，在服务端通过 `RequestMethodHandlerAdapter` 注册（请参阅 [配置消息转换器](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-config-message-converters)）。

`HttpMessageConverter` 实现在下一节中描述。对所有的消息转换器，都有一个默认的媒体类型，不过你可以通过设定 `supportedMediaTypes` bean 属性覆盖默认值。下面的表描述了各种实现：

| MessageConverter                         | Description                                                  |
| :--------------------------------------- | :----------------------------------------------------------- |
| `StringHttpMessageConverter`             | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求实例读取 `String` 实例，向 HTTP 响应写入 `String` 实例。默认地，该转换器支持所有的文本媒体类型（`text/*`）并以 `Content-Type`  值 `text/plain` 写入。 |
| `FormHttpMessageConverter`               | 一个 `HttpMessageConverter` 实现，可以从 HTTP 请求和响应中读取和写入表单数据。默认情况下，此转换器读取和写入 `application/x-www-form-urlencoded` 媒体类型。 表单数据是从 `MultiValueMap<String, String>` 中读取并写入的。 |
| `ByteArrayHttpMessageConverter`          | An `HttpMessageConverter` implementation that can read and write byte arrays from the HTTP request and response. By default, this converter supports all media types (`*/*`) and writes with a `Content-Type` of `application/octet-stream`. You can override this by setting the `supportedMediaTypes` property and overriding `getContentType(byte[])`. |
| `MarshallingHttpMessageConverter`        | An `HttpMessageConverter` implementation that can read and write XML by using Spring’s `Marshaller` and `Unmarshaller` abstractions from the `org.springframework.oxm` package. This converter requires a `Marshaller` and `Unmarshaller` before it can be used. You can inject these through constructor or bean properties. By default, this converter supports `text/xml` and `application/xml`. |
| `MappingJackson2HttpMessageConverter`    | An `HttpMessageConverter` implementation that can read and write JSON by using Jackson’s `ObjectMapper`. You can customize JSON mapping as needed through the use of Jackson’s provided annotations. When you need further control (for cases where custom JSON serializers/deserializers need to be provided for specific types), you can inject a custom `ObjectMapper` through the `ObjectMapper` property. By default, this converter supports `application/json`. |
| `MappingJackson2XmlHttpMessageConverter` | An `HttpMessageConverter` implementation that can read and write XML by using [Jackson XML](https://github.com/FasterXML/jackson-dataformat-xml) extension’s `XmlMapper`. You can customize XML mapping as needed through the use of JAXB or Jackson’s provided annotations. When you need further control (for cases where custom XML serializers/deserializers need to be provided for specific types), you can inject a custom `XmlMapper` through the `ObjectMapper` property. By default, this converter supports `application/xml`. |
| `SourceHttpMessageConverter`             | An `HttpMessageConverter` implementation that can read and write `javax.xml.transform.Source` from the HTTP request and response. Only `DOMSource`, `SAXSource`, and `StreamSource` are supported. By default, this converter supports `text/xml` and `application/xml`. |
| `BufferedImageHttpMessageConverter`      | An `HttpMessageConverter` implementation that can read and write `java.awt.image.BufferedImage` from the HTTP request and response. This converter reads and writes the media type supported by the Java I/O API. |

##### Jackson JSON Views

You can specify a [Jackson JSON View](https://www.baeldung.com/jackson-json-view-annotation) to serialize only a subset of the object properties, as the following example shows:

```
MappingJacksonValue value = new MappingJacksonValue(new User("eric", "7!jd#h23"));
value.setSerializationView(User.WithoutPasswordView.class);

RequestEntity<MappingJacksonValue> requestEntity =
    RequestEntity.post(new URI("https://example.com/user")).body(value);

ResponseEntity<String> response = template.exchange(requestEntity, String.class);
```

##### Multipart

To send multipart data, you need to provide a `MultiValueMap<String, Object>` whose values may be an `Object` for part content, a `Resource` for a file part, or an `HttpEntity` for part content with headers. For example:

```java
    MultiValueMap<String, Object> parts = new LinkedMultiValueMap<>();

    parts.add("fieldPart", "fieldValue");
    parts.add("filePart", new FileSystemResource("...logo.png"));
    parts.add("jsonPart", new Person("Jason"));

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_XML);
    parts.add("xmlPart", new HttpEntity<>(myBean, headers));
```

In most cases, you do not have to specify the `Content-Type` for each part. The content type is determined automatically based on the `HttpMessageConverter` chosen to serialize it or, in the case of a `Resource` based on the file extension. If necessary, you can explicitly provide the `MediaType` with an `HttpEntity` wrapper.

Once the `MultiValueMap` is ready, you can pass it to the `RestTemplate`, as show below:

```java
    MultiValueMap<String, Object> parts = ...;
    template.postForObject("https://example.com/upload", parts, Void.class);
```

If the `MultiValueMap` contains at least one non-`String` value, the `Content-Type` is set to `multipart/form-data` by the `FormHttpMessageConverter`. If the `MultiValueMap` has `String` values the `Content-Type` is defaulted to `application/x-www-form-urlencoded`. If necessary the `Content-Type` may also be set explicitly.

#### 1.8.2. Using `AsyncRestTemplate` (Deprecated)

The `AsyncRestTemplate` is deprecated. For all use cases where you might consider using `AsyncRestTemplate`, use the [WebClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) instead.