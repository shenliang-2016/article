## 2. 资源

本章节介绍 Spring 如何处理资源以及如何在 Spring 中使用资源。包含下列主题：

- [介绍](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-introduction)
- [Resource 接口](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resource)
- [内建 Resource 实现](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations)
- [`ResourceLoader`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resourceloader)
- [`ResourceLoaderAware` 接口](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resourceloaderaware)
- [Resources 作为依赖](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-as-dependencies)
- [应用上下文和资源路径](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-app-ctx)

### 2.1. 介绍

Java 的标准`java.net.URL`类和用来处理各种 URL 前缀的标准处理器，很不幸，并不非常能够胜任对所有低层次资源的访问。例如，没有标准化的 URL 实现可用于访问需要从类路径或相对于`ServletContext`获取的资源。虽然可以为专用的 URL 前缀注册新的处理程序（类似于`http:`这样的前缀的现有处理程序），但这通常非常复杂，并且 URL 接口仍然缺少一些理想的功能，例如检查被指向的资源存在的方法。

### 2.2. Resource 接口

Spring的`Resource`接口旨在成为一个更有能力的接口，用于抽象对低级资源的访问。以下清单显示了`Resource`接口定义：

```java
public interface Resource extends InputStreamSource {

    boolean exists();

    boolean isOpen();

    URL getURL() throws IOException;

    File getFile() throws IOException;

    Resource createRelative(String relativePath) throws IOException;

    String getFilename();

    String getDescription();

}
```

正如`Resource`接口的定义所示，它扩展了`InputStreamSource`接口。以下清单显示了`InputStreamSource`接口的定义：

```java
public interface InputStreamSource {

    InputStream getInputStream() throws IOException;

}
```

`Resource` 接口的最重要的方法包括：

- `getInputStream()`: 定位并打开资源，返回读取资源的`InputStream`。每次调用都会返回一个新的`InputStream`。关闭这些流是方法调用者的责任。
- `exists()`: 返回一个 `boolean` 值表示该资源的物理形式是否确实存在。
- `isOpen()`: 返回一个 `boolean` 值表示该资源是否使用一个打开的流处理。如果返回`true`，则该`InputStream`就不能被多次读取，只能读取一次之后就关闭以防止资源泄漏。对所有常规资源实现，返回`false`，但是`InputStreamResource`除外。
- `getDescription()`: 返回此资源的描述，用于处理资源时的错误输出。这通常是完全限定的文件名或资源的实际URL。

其它方法允许你获取表示资源的实际的`URL`或者`File`对象（如果底层实现兼容并支持该功能）。

当需要资源时，Spring 自身广泛使用了`Resource`抽象，作为很多方法签名的参数类型。一些 Spring APIs 中的其它方法（比如各种`ApplicationContext`实现的构造器）使用一个`String`以简单形式来创建适用于上下文实现的`Resource`，或者通过`String`路径上的特殊前缀，让调用者指定必须创建和使用的特定`Resource`。

虽然Spring中大量使用了`Resource`接口，但在自己的代码中使用它作为通用实用程序类非常有用，用于访问资源，即使你的代码不知道或不关心任何其他 Spring 组件。虽然这会将您的代码耦合到 Spring，但它实际上只将它耦合到这一小组实用程序类中，这些实用程序类可以作为`URL`的更有能力的替代品，并且可以被认为等同于您将用于此目的的任何其他库。

> `Resource`抽象不会替代功能，它会尽可能包装功能。比如，`UrlResource`包装 URL 并使用包装后的`URL`来完成它的工作。

