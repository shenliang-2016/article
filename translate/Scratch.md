#### 4.14.1. RestTemplate 定制

可以通过三种方法定制 `RestTemplate` ，采用哪种方法取决于你想在何种范围上定制。

为了使任何自定义的范围尽可能狭窄，请注入自动配置的 `RestTemplateBuilder`，然后根据需要调用其方法。每个方法调用都会返回一个新的 `RestTemplateBuilder` 实例，因此自定义设置仅会影响构建器的使用。

要进行整个应用程序的附加定制，请使用 `RestTemplateCustomizer` bean。所有这些 bean 都会自动注册到自动配置的 `RestTemplateBuilder` 中，并应用于使用它构建的任何模板。

以下示例显示了一个定制器，该定制器为除 `192.168.0.5` 之外的所有主机配置代理的使用：

```java
static class ProxyCustomizer implements RestTemplateCustomizer {

    @Override
    public void customize(RestTemplate restTemplate) {
        HttpHost proxy = new HttpHost("proxy.example.com");
        HttpClient httpClient = HttpClientBuilder.create().setRoutePlanner(new DefaultProxyRoutePlanner(proxy) {

            @Override
            public HttpHost determineProxy(HttpHost target, HttpRequest request, HttpContext context)
                    throws HttpException {
                if (target.getHostName().equals("192.168.0.5")) {
                    return null;
                }
                return super.determineProxy(target, request, context);
            }

        }).build();
        restTemplate.setRequestFactory(new HttpComponentsClientHttpRequestFactory(httpClient));
    }

}
```

最后，最极端（很少使用）的选项是创建自己的 `RestTemplateBuilder` bean。这样做会关闭 `RestTemplateBuilder` 的自动配置，并阻止使用任何 `RestTemplateCustomizer` bean。

