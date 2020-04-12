#### 5.3.4.  自定义管理服务器地址

您可以通过设置 `management.server.address` 属性来定制管理端点可用的地址。如果您只想在内部或面向操作的网络上侦听或仅侦听来自 `localhost` 的连接，则这样做很有用。

> 仅当端口与主服务器端口不同时，您才能在其他地址上侦听。

下面的例子 `application.properties` 不允许远程管理连接：

```properties
management.server.port=8081
management.server.address=127.0.0.1
```

#### 5.3.5. 禁用 HTTP 端点

如果你不希望通过 HTTP 暴露端点，你可以设定管理端口为 `-1`，如下面例子所示：

```properties
management.server.port=-1
```

也可以使用 `management.endpoints.web.exposure.exclude` 属性来实现，如以下示例所示：

```properties
management.endpoints.web.exposure.exclude=*
```

