#### 4.27.1. 使用 `WebServiceTemplate` 调用 Web Services 

如果你需要在应用中调用远程 Web services ，可以使用 [`WebServiceTemplate`](https://docs.spring.io/spring-ws/docs/3.0.8.RELEASE/reference/#client-web-service-template) 类。由于 `WebServiceTemplate` 使用之前通常都需要按照需求自定义，Spring Boot 并未提供任何单独的自动配置的 `WebServiceTemplate` bean。相反，它自动配置了一个 `WebServiceTemplateBuilder` ，用来按需创建 `WebServiceTemplate` 实例。

下面是个典型的例子：

```java
@Service
public class MyService {

    private final WebServiceTemplate webServiceTemplate;

    public MyService(WebServiceTemplateBuilder webServiceTemplateBuilder) {
        this.webServiceTemplate = webServiceTemplateBuilder.build();
    }

    public DetailsResp someWsCall(DetailsReq detailsReq) {
         return (DetailsResp) this.webServiceTemplate.marshalSendAndReceive(detailsReq, new SoapActionCallback(ACTION));
    }

}
```

默认地， `WebServiceTemplateBuilder` 探测合适的 HTTP-based `WebServiceMessageSender` 使用类路径上可用的 HTTP client 类库。你也可以如下自定义读取或者连接超时时间：

```java
@Bean
public WebServiceTemplate webServiceTemplate(WebServiceTemplateBuilder builder) {
    return builder.messageSenders(new HttpWebServiceMessageSenderBuilder()
            .setConnectTimeout(5000).setReadTimeout(2000).build()).build();
}
```