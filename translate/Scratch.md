#### 5.3.2. 自定义管理服务器端口

对于基于云的部署，通过使用默认的 HTTP 端口公开管理端点是明智的选择。但是，如果您的应用程序在自己的数据中心内运行，则您可能更喜欢使用其他 HTTP 端口公开端点。

您可以设置 `management.server.port` 属性来更改 HTTP 端口，如以下示例所示：

```properties
management.server.port=8081
```

> 在 Cloud Foundry 上，默认情况下，应用程序仅在端口 8080 上接收 HTTP 和 TCP 路由请求。如果要在 Cloud Foundry 上使用自定义管理端口，则需要明确设置应用程序的路由，以将流量转发到该自定义端口。

#### 5.3.3. 配置管理专用的 SSL

当配置为使用自定义端口时，还可以通过使用各种 `management.server.ssl.*` 属性为管理服务器配置其自己的 SSL。例如，这样做可以使管理服务器在主应用程序使用 HTTPS 时通过 HTTP 可用，如以下属性设置所示：

```properties
server.port=8443
server.ssl.enabled=true
server.ssl.key-store=classpath:store.jks
server.ssl.key-password=secret
management.server.port=8080
management.server.ssl.enabled=false
```

或者，主服务器和管理服务器都可以使用 SSL，但具有不同的密钥库，如下所示：

```properties
server.port=8443
server.ssl.enabled=true
server.ssl.key-store=classpath:main.jks
server.ssl.key-password=secret
management.server.port=8080
management.server.ssl.enabled=true
management.server.ssl.key-store=classpath:management.jks
management.server.ssl.key-password=secret
```

