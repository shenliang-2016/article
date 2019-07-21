### 2.7 应用上下文和资源路劲

本节介绍如何使用资源创建应用程序上下文，包括使用XML的快捷方式，如何使用通配符以及其他详细信息。

#### 2.7.1 构建应用上下文

应用程序上下文构造函数（对于特定的应用程序上下文类型）通常将字符串或字符串数组作为资源的位置路径，例如构成上下文定义的XML文件。

当这样的位置路径没有前缀时，从该路径构建并用于加载 bean 定义的特定`Resource`类型取决于并且适合于特定的应用程序上下文。例如，考虑以下示例，它创建一个`ClassPathXmlApplicationContext`：

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("conf/appContext.xml");
```

bean 定义是从类路径加载的，因为使用了`ClassPathResource`。但是，请考虑以下示例，它创建一个`FileSystemXmlApplicationContext`：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("conf/appContext.xml");
```

现在，bean 定义是从文件系统位置加载的（在这种情况下，相对于当前工作目录）。

请注意，在位置路径上使用特殊类路径前缀或标准 URL 前缀会覆盖为加载定义而创建的默认类型`Resource`。请考虑以下示例：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("classpath:conf/appContext.xml");
```

使用`FileSystemXmlApplicationContext`从类路径加载 bean 定义。但是，它仍然是一个`FileSystemXmlApplicationContext`。如果它随后被用作`ResourceLoader`，任何未加前缀的路径仍被视为文件系统路径。

##### 构建 `ClassPathXmlApplicationContext` 实例 — 快捷方式

`ClassPathXmlApplicationContext`公开了许多构造函数，以便于实例化。基本思想是你只能提供一个字符串数组，它只包含XML文件本身的文件名（没有前导路径信息），还提供了一个`Class`。然后，`ClassPathXmlApplicationContext`从提供的类派生路径信息。

请考虑以下目录布局：

```
com/
  foo/
    services.xml
    daos.xml
    MessengerService.class
```

下面的示例演示如何实例化一个`ClassPathXmlApplicationContext`实例，该实例由名为`services.xml`和`daos.xml`的文件中定义的 bean 组成（在类路径上）。

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext(
    new String[] {"services.xml", "daos.xml"}, MessengerService.class);
```

参考 [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 文档获取有关各种构造器细节。

#### 2.7.2 应用上下文构造器资源路径中的通配符

应用程序上下文构造函数值中的资源路径可以是简单路径（如前所示），每个路径都与目标`Resource`进行一对一映射，或者可以包含特殊的`classpath*:`前缀或内部 Ant 风格的正则表达式（使用Spring的`PathMatcher`实用程序进行匹配）。 后两者都是有效的通配符。

此机制的一个用途是当您需要进行基于组件风格的应用程序组装时。所有组件都可以将上下文定义片段“发布”到一个众所周知的位置路径，并且当使用前缀为`classpath*:`的相同路径创建最终应用程序上下文时，将自动拾取所有组件片段。

请注意，此通配符特定于在应用程序上下文构造函数中使用资源路径（或当直接使用`PathMatcher`实用程序类层次结构时），并在构造时解析。它与`Resource`类型本身无关。您不能使用`classpath*:`前缀来构造实际的`Resource`，因为一个资源对象一次只指向一个资源。

##### Ant-风格模式

路径位置可以包含 Ant-风格模式，如下面例子所示：

```
/WEB-INF/*-context.xml
com/mycompany/**/applicationContext.xml
file:C:/some/path/*-context.xml
classpath:com/mycompany/**/applicationContext.xml
```

当路径位置包含 Ant 样式模式时，解析程序遵循更复杂的过程来尝试解析通配符。它为直到最后一个非通配符段的路径生成一个`Resource`，并从中获取一个 URL 。如果此 URL 不是`jar：`URL 或特定于容器的变体（例如 WebLogic 中的`zip:`，WebSphere 中的`wsjar`等），则从中获取`java.io.File`并且用于通过遍历文件系统来解析通配符。对于jar URL，解析器从它获取`java.net.JarURLConnection`或手动解析jar URL，然后遍历jar文件的内容以解析通配符。

###### 对可移植性的影响

如果指定的路径已经是文件URL（隐式，因为基本的`ResourceLoader`是一个文件系统或明确的文件系统），保证通配符以完全可移植的方式工作。

如果指定的路径是类路径位置，则解析器必须通过进行`Classloader.getResource()`调用来获取最后一个非通配符路径段URL。由于这只是路径的一个节点（不是最后的文件），实际上它是未定义的（如`ClassLoader`文档所述）在这种情况下确切地返回了什么类型的URL。在实践中，它始终是一个`java.io.File`，表示目录（类路径资源解析为文件系统位置）或某种类型的jar URL（类路径资源解析为jar位置）。尽管如此，这种操作仍存在可移植性问题。

如果获取最后一个非通配符段的jar URL，解析器必须能够从中获取`java.net.JarURLConnection`或手动解析jar URL，以便能够遍历jar的内容并解析通配符。这在大多数环境中都有效，但在其他环境中无效，我们强烈建议您在依赖它之前，在特定环境中对来自jar的资源的通配符解析进行全面测试。

#####  `classpath*:` 前缀

构造基于XML的应用程序上下文时，位置字符串可以使用特殊的`classpath*:`前缀，如以下示例所示：

```java
ApplicationContext ctx =
    new ClassPathXmlApplicationContext("classpath*:conf/appContext.xml");
```

这个特殊的前缀指定必须获取与给定名称匹配的所有类路径资源（在内部，这主要通过调用 `ClassLoader.getResources(…)`）然后合并以形成最终的应用程序上下文定义。

> 通配符类路径依赖于底层类加载器的 `getResources()` 方法。由于现在大多数应用程序服务器都提供了自己的类加载器实现，因此行为可能会有所不同，尤其是在处理jar文件时。 检查 `classpath*` 是否有效的简单测试是使用类加载器从类路径中的jar中加载文件： `getClass().getClassLoader().getResources("<someFileInsideTheJar>")`。尝试使用具有相同名称但放在两个不同位置的文件进行此测试。 如果返回了不适当的结果，请检查应用程序服务器文档以获取可能影响类加载器行为的设置。

您还可以在位置路径的其余部分中将 `classpath*:` 前缀与`PathMatcher`模式组合在一起（例如，`classpath*:META-INF/*-beans.xml`）。在这种情况下，解析策略非常简单：在最后一个非通配符路径段上使用`ClassLoader.getResources()`调用来获取类加载器层次结构中的所有匹配资源，然后从每个资源中获取相同的资源。前面描述的`PathMatcher`解析策略用于通配符子路径。

##### 有关通配符的其它问题

请注意， `classpath*:`与Ant样式模式结合使用时，只能在模式启动前与至少一个根目录一起可靠地工作，除非实际目标文件驻留在文件系统中。这意味着诸如`classpath*:*.xml`之类的模式可能无法从jar文件的根目录中检索文件，而只能从扩展目录的根目录中检索文件。

Spring检索类路径条目的能力来自JDK的`ClassLoader.getResources()`方法，该方法只返回空字符串的文件系统位置（指示搜索的潜在根）。Spring也会在jar文件中评估`URLClassLoader`运行时配置和`java.class.path`清单，但这不能保证导致可移植行为。

> 扫描类路径包需要在类路径中存在相应的目录条目。使用Ant构建JAR时，请不要激活JAR任务的仅文件开关。此外，在某些环境中，基于安全策略，类路径目录可能不会公开 - 例如，JDK 1.7.0_45及更高版本上的独立应用程序（需要在清单中设置“Trusted-Library”。请参阅  https://stackoverflow.com/questions/19394570/java-jre-7u45-breaks-classloader-getresources）。
>
> 在JDK 9的模块路径（Jigsaw）上，Spring的类路径扫描通常按预期工作。此处强烈建议将资源放入专用目录，避免上述搜索jar文件根级别的可移植性问题。

如果要搜索的根包在多个类路径位置中可用，则不能保证使用带有`classpath：`资源的Ant样式模式查找匹配的资源。请考虑以下资源位置示例：

```
com/mycompany/package1/service-context.xml
```

现在考虑可能用来尝试查找该文件的Ant风格路径：

```
classpath:com/mycompany/**/service-context.xml
```

这样的资源可能只在一个位置，但是当使用前面例子之类的路径来尝试解析它时，解析器会处理由 `getResource("com/mycompany");`返回的（第一个）URL。如果此基本包节点存在于多个类加载器位置中，则实际的最终资源可能不存在。因此，在这种情况下，您应该更喜欢使用具有相同Ant样式模式的 `classpath*:`，它搜索包含根包的所有类路径位置。

#### 2.7.3 `FileSystemResource` 注意事项

没有附加到`FileSystemApplicationContext`的`FileSystemResource`（也就是说，当`FileSystemApplicationContext`不是实际的`ResourceLoader`时）就像你期望的那样处理绝对路径和相对路径。相对路径相对于当前工作目录，而绝对路径相对于文件系统的根目录。

但是，为了向后兼容（历史）原因，当`FileSystemApplicationContext`是`ResourceLoader`时，这会发生变化。`FileSystemApplicationContext`强制所有附加的`FileSystemResource`实例将所有位置路径视为相对路径，无论它们是否以前导斜杠开头。实际上，这意味着以下示例是等效的：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("conf/context.xml");
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("/conf/context.xml");
```

以下示例也是等效的（即使它们有所不同，因为一个案例是相对的而另一个案例是绝对的）：

```java
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("some/resource/path/myTemplate.txt");
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("/some/resource/path/myTemplate.txt");
```

实际上，如果你需要真正的绝对文件系统路径，你应该避免使用带有`FileSystemResource`或`FileSystemXmlApplicationContext`的绝对路径，并使用`file：`URL前缀强制使用`UrlResource`。以下示例显示了如何执行此操作：

```java
// actual context type doesn't matter, the Resource will always be UrlResource
ctx.getResource("file:///some/resource/path/myTemplate.txt");
// force this FileSystemXmlApplicationContext to load its definition via a UrlResource
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("file:///conf/context.xml");
```

