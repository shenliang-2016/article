#### 4.15.2. WebClient 定制

`WebClient` 自定义有三种主要方法，具体取决于您希望自定义应用的范围。

为了使所有定制的范围尽可能狭窄，请注入自动配置的 `WebClient.Builder`，然后根据需要调用其方法。`WebClient.Builder` 实例是有状态的：构建器上的任何更改都会反映在随后使用它创建的所有客户端中。如果要使用同一构建器创建多个客户端，则还可以考虑使用 `WebClient.Builder other = builder.clone();` 克隆该构建器。

为了对所有 `WebClient.Builder` 实例进行应用范围的附加自定义，您可以声明 `WebClientCustomizer` bean 并在注入时在本地更改 `WebClient.Builder`。

最后，您可以使用原始 API 并使用 `WebClient.create()`。在这种情况下，不会应用任何自动配置或 `WebClientCustomizer`。

