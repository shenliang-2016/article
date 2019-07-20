#### 2.3.2 `ClassPathResource`

此类表示一个应该从类路径获取的资源。它要么使用线程上下文类加载器，一个给定的类加载器，或者一个给定的用于资源加载的类。

如果类路径资源留驻在文件系统中，`Resource`实现支持解析为`java.io.File`。但是当类路径资源位于 jar 包中而尚未解压（被 servlet 引擎或者其他容器或环境）到文件系统中，不支持这种解析。为了解决这个问题，各种`Resource`实现都支持解析为`java.net.URL`。

`ClassPathResource`是由Java代码通过显式使用`ClassPathResource`构造函数创建的，但是当你调用一个带有表示路径的`String`参数的API方法时，通常会隐式创建它。对于后一种情况，JavaBeans`PropertyEditor`在字符串路径上识别特殊前缀`classpath:`，并在这种情况下创建`ClassPathResource`。

#### 2.3.3 `FileSystemResource`

这是一个用于`java.io.File`和`java.nio.file.Path`处理的`Resource`实现。它支持解析为`File`和`URL`。

#### 2.3.4 `ServletContextResource`

这是`ServletContext`资源的`Resource`实现，它解释相关Web应用程序根目录中的相对路径。

它始终支持流访问和 URL 访问，但只有在Web应用程序存档被解压之后且资源实际位于文件系统上时才允许`java.io.File`访问。无论它是解压到在文件系统上还是直接从JAR或其他地方（如数据库）访问，实际上都依赖于Servlet容器。

#### 2.3.5. `InputStreamResource`

`InputStreamResource`是给定`InputStream`的`Resource`实现。只有在没有适用的特定`Resource`实现时才应该使用它。特别是，在可能的情况下，应该优先考虑使用`ByteArrayResource`或任何基于文件的`Resource`实现。

与其他`Resource`实现相比，这是已经打开的资源的描述符。因此，它从`isOpen()`返回`true`。如果需要将资源描述符保留在某处或者需要多次读取流，请不要使用它。

#### 2.3.6. `ByteArrayResource`

这是给定字节数组的`Resource`实现。它为给定的字节数组创建一个`ByteArrayInputStream`。

它对于从任何给定的字节数组加载内容非常有用，而无需使用一次性的`InputStreamResource`。

### 2.4 `ResourceLoader`

`ResourceLoader`接口意味着由可以返回（即加载）`Resource`实例的对象实现。以下清单显示了`ResourceLoader`接口定义：

```java
public interface ResourceLoader {

    Resource getResource(String location);

}
```

所有应用程序上下文都实现了`ResourceLoader`接口。因此，所有应用程序上下文都可用于获取`Resource`实例。

当你在特定的应用程序上下文中调用`getResource()`，并且指定的位置路径没有特定的前缀时，你会得到一个适合于该特定应用程序上下文的`Resource`类型。例如，假设针对`ClassPathXmlApplicationContext`实例执行了以下代码片段：

```java
Resource template = ctx.getResource("some/resource/path/myTemplate.txt");
```

对于`ClassPathXmlApplicationContext`，该代码返回一个`ClassPathResource`。如果针对`FileSystemXmlApplicationContext`实例执行相同的方法，它将返回`FileSystemResource`。对于`WebApplicationContext`，它将返回一个`ServletContextResource`。它同样会为每个上下文返回适当的对象。

因此，您可以以适合特定应用程序上下文的方式加载资源。

另一方面，您可以通过指定特殊的`classpath:`前缀来强制使用`ClassPathResource`，而不管应用程序上下文类型如何，如下例所示：

```java
Resource template = ctx.getResource("classpath:some/resource/path/myTemplate.txt");
```

类似地，您可以通过指定任何标准的`java.net.URL`前缀来强制使用`UrlResource`。以下一对示例使用`file`和`http`前缀：

```java
Resource template = ctx.getResource("file:///some/resource/path/myTemplate.txt");
Resource template = ctx.getResource("https://myhost.com/resource/path/myTemplate.txt");
```

下表总结了将`String`对象转换为`Resource`对象的策略：

| Prefix     | Example                          | Explanation                                                  |
| :--------- | :------------------------------- | :----------------------------------------------------------- |
| classpath: | `classpath:com/myapp/config.xml` | 从类路径加载。                                               |
| file:      | `file:///data/config.xml`        | 作为 `URL` 从文件系统加载。参考 [`FileSystemResource` Caveats](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-filesystemresource-caveats) 。 |
| http:      | `https://myserver/logo.png`      | 作为 `URL` 加载。                                            |
| (none)     | `/data/config.xml`               | 依赖底层的 `ApplicationContext`。                            |

### 2.5 `ResourceLoaderAware` 接口

`ResourceLoaderAware`接口是一个特殊的回调接口，它标识希望提供`ResourceLoader`引用的组件。以下清单显示了`ResourceLoaderAware`接口的定义：

```java
public interface ResourceLoaderAware {

    void setResourceLoader(ResourceLoader resourceLoader);
}
```

当一个类实现`ResourceLoaderAware`并被部署到应用程序上下文（作为Spring管理的bean）时，它被应用程序上下文识别为`ResourceLoaderAware`。然后，应用程序上下文调用`setResourceLoader(ResourceLoader)`，将自身作为参数提供（请记住，Spring中的所有应用程序上下文都实现了`ResourceLoader`接口）。

由于`ApplicationContext`是`ResourceLoader`，bean也可以实现`ApplicationContextAware`接口并直接使用提供的应用程序上下文来加载资源。但是，一般来说，最好使用专门的`ResourceLoader`接口，如果这就是你所需要的。代码只能耦合到资源加载接口（可以认为是实用程序接口），而不是整个Spring`ApplicationContext`接口。

在应用程序组件中，您还可以依赖自动装配`ResourceLoader`作为实现`ResourceLoaderAware`接口的替代方法。“传统的”构造函数和`byType`自动装配模式（如 [自动装配协作者](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 中所述）能够分别为构造函数参数或 setter 方法参数提供`ResourceLoader`。为了获得更大的灵活性（包括自动装配字段和多参数方法的能力），请考虑使用基于注解的自动装配功能。在这种情况下，只要字段，构造函数或方法带有`@Autowired`注解，`ResourceLoader`就自动注入一个字段，构造函数参数或方法参数，它们需要`ResourceLoader`类型。有关更多信息，请参阅 [使用`@Autowired`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-autowired-annotation) 。

### 2.6. Resources as Dependencies

如果 bean 本身将通过某种动态过程确定并提供资源路径，那么 bean 使用`ResourceLoader`接口加载资源可能是有意义的。例如，考虑加载某种模板，其中所需的特定资源取决于用户的角色。如果资源是静态的，那么完全消除`ResourceLoader`接口的使用是有意义的，让 bean 暴露它需要的`Resource`属性，并期望它们被注入其中。

使得注入这些属性变得微不足道的是，所有应用程序上下文都注册并使用特殊的JavaBeans`PropertyEditor`，它可以将`String`路径转换为`Resource`对象。因此，如果`myBean`具有类型为`Resource`的模板属性，则可以使用该资源的简单字符串进行配置，如以下示例所示：

```xml
<bean id="myBean" class="...">
    <property name="template" value="some/resource/path/myTemplate.txt"/>
</bean>
```

请注意，资源路径没有前缀。因此，由于应用程序上下文本身将被用作`ResourceLoader`，所以资源本身通过`ClassPathResource`，`FileSystemResource`或`ServletContextResource`加载，具体取决于上下文的确切类型。

如果需要强制使用特定的`Resource`类型，则可以使用前缀。以下两个示例显示了如何强制使用`ClassPathResource`和`UrlResource`（后者用于访问文件系统文件）：

```xml
<property name="template" value="classpath:some/resource/path/myTemplate.txt">
<property name="template" value="file:///some/resource/path/myTemplate.txt"/>
```

