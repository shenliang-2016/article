### 2.3 内建 Resource 实现

Spring 包含下列 `Resource` 实现：

- [`UrlResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-urlresource)
- [`ClassPathResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-classpathresource)
- [`FileSystemResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-filesystemresource)
- [`ServletContextResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-servletcontextresource)
- [`InputStreamResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-inputstreamresource)
- [`ByteArrayResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-bytearrayresource)

#### 2.3.1. `UrlResource`

`UrlResource`包装`java.net.URL`，可用于访问通常可通过 URL 访问的任何对象，例如文件，HTTP目标，FTP目标等。所有 URL 都具有标准化的字符串表示，以便使用适当的标准化前缀来指示另一个URL类型。这包括 `file:` 用于访问文件系统路径，`http:` 用于通过HTTP协议访问资源，`ftp:`用于通过FTP访问资源，以及其他。

`UrlResource`由Java代码通过显式使用`UrlResource`构造函数创建，但通常在调用采用`String`参数表示路径的API方法时隐式创建。对于后一种情况，JavaBeans `PropertyEditor`最终决定要创建哪种类型的`Resource`。如果路径字符串包含众所周知的（对于它）前缀（例如 `classpath:`)，则会为该前缀创建适当的专用 `Resource` 。但是，如果它无法识别前缀，则假定该字符串是标准URL字符串并创建`UrlResource`。

