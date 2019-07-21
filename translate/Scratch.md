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

##### Ant-style Patterns

Path locations can contain Ant-style patterns, as the following example shows:

```
/WEB-INF/*-context.xml
com/mycompany/**/applicationContext.xml
file:C:/some/path/*-context.xml
classpath:com/mycompany/**/applicationContext.xml
```

When the path location contains an Ant-style pattern, the resolver follows a more complex procedure to try to resolve the wildcard. It produces a `Resource` for the path up to the last non-wildcard segment and obtains a URL from it. If this URL is not a `jar:` URL or container-specific variant (such as `zip:` in WebLogic, `wsjar` in WebSphere, and so on), a `java.io.File` is obtained from it and used to resolve the wildcard by traversing the filesystem. In the case of a jar URL, the resolver either gets a `java.net.JarURLConnection` from it or manually parses the jar URL and then traverses the contents of the jar file to resolve the wildcards.

###### Implications on Portability

If the specified path is already a file URL (either implicitly because the base `ResourceLoader` is a filesystem one or explicitly), wildcarding is guaranteed to work in a completely portable fashion.

If the specified path is a classpath location, the resolver must obtain the last non-wildcard path segment URL by making a `Classloader.getResource()` call. Since this is just a node of the path (not the file at the end), it is actually undefined (in the`ClassLoader` javadoc) exactly what sort of a URL is returned in this case. In practice, it is always a `java.io.File` representing the directory (where the classpath resource resolves to a filesystem location) or a jar URL of some sort (where the classpath resource resolves to a jar location). Still, there is a portability concern on this operation.

If a jar URL is obtained for the last non-wildcard segment, the resolver must be able to get a `java.net.JarURLConnection` from it or manually parse the jar URL, to be able to walk the contents of the jar and resolve the wildcard. This does work in most environments but fails in others, and we strongly recommend that the wildcard resolution of resources coming from jars be thoroughly tested in your specific environment before you rely on it.

##### The `classpath*:` Prefix

When constructing an XML-based application context, a location string may use the special `classpath*:` prefix, as the following example shows:

```
ApplicationContext ctx =
    new ClassPathXmlApplicationContext("classpath*:conf/appContext.xml");
```

This special prefix specifies that all classpath resources that match the given name must be obtained (internally, this essentially happens through a call to `ClassLoader.getResources(…)`) and then merged to form the final application context definition.

> The wildcard classpath relies on the `getResources()` method of the underlying classloader. As most application servers nowadays supply their own classloader implementation, the behavior might differ, especially when dealing with jar files. A simple test to check if `classpath*` works is to use the classloader to load a file from within a jar on the classpath: `getClass().getClassLoader().getResources("<someFileInsideTheJar>")`. Try this test with files that have the same name but are placed inside two different locations. In case an inappropriate result is returned, check the application server documentation for settings that might affect the classloader behavior.

You can also combine the `classpath*:` prefix with a `PathMatcher` pattern in the rest of the location path (for example, `classpath*:META-INF/*-beans.xml`). In this case, the resolution strategy is fairly simple: A `ClassLoader.getResources()` call is used on the last non-wildcard path segment to get all the matching resources in the class loader hierarchy and then, off each resource, the same `PathMatcher` resolution strategy described earlier is used for the wildcard subpath.

##### Other Notes Relating to Wildcards

Note that `classpath*:`, when combined with Ant-style patterns, only works reliably with at least one root directory before the pattern starts, unless the actual target files reside in the file system. This means that a pattern such as `classpath*:*.xml` might not retrieve files from the root of jar files but rather only from the root of expanded directories.

Spring’s ability to retrieve classpath entries originates from the JDK’s `ClassLoader.getResources()` method, which only returns file system locations for an empty string (indicating potential roots to search). Spring evaluates `URLClassLoader` runtime configuration and the `java.class.path` manifest in jar files as well, but this is not guaranteed to lead to portable behavior.

> The scanning of classpath packages requires the presence of corresponding directory entries in the classpath. When you build JARs with Ant, do not activate the files-only switch of the JAR task. Also, classpath directories may not get exposed based on security policies in some environments — for example, stand-alone applications on JDK 1.7.0_45 and higher (which requires 'Trusted-Library' to be set up in your manifests. See https://stackoverflow.com/questions/19394570/java-jre-7u45-breaks-classloader-getresources).
>
> On JDK 9’s module path (Jigsaw), Spring’s classpath scanning generally works as expected. Putting resources into a dedicated directory is highly recommendable here as well, avoiding the aforementioned portability problems with searching the jar file root level.

Ant-style patterns with `classpath:` resources are not guaranteed to find matching resources if the root package to search is available in multiple class path locations. Consider the following example of a resource location:

```
com/mycompany/package1/service-context.xml
```

Now consider an Ant-style path that someone might use to try to find that file:

```
classpath:com/mycompany/**/service-context.xml
```

Such a resource may be in only one location, but when a path such as the preceding example is used to try to resolve it, the resolver works off the (first) URL returned by `getResource("com/mycompany");`. If this base package node exists in multiple classloader locations, the actual end resource may not be there. Therefore, in such a case you should prefer using `classpath*:`with the same Ant-style pattern, which searches all class path locations that contain the root package.

#### 2.7.3 `FileSystemResource` Caveats

A `FileSystemResource` that is not attached to a `FileSystemApplicationContext` (that is, when a `FileSystemApplicationContext`is not the actual `ResourceLoader`) treats absolute and relative paths as you would expect. Relative paths are relative to the current working directory, while absolute paths are relative to the root of the filesystem.

For backwards compatibility (historical) reasons however, this changes when the `FileSystemApplicationContext` is the `ResourceLoader`. The `FileSystemApplicationContext` forces all attached `FileSystemResource` instances to treat all location paths as relative, whether they start with a leading slash or not. In practice, this means the following examples are equivalent:

```
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("conf/context.xml");
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("/conf/context.xml");
```

The following examples are also equivalent (even though it would make sense for them to be different, as one case is relative and the other absolute):

```
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("some/resource/path/myTemplate.txt");
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("/some/resource/path/myTemplate.txt");
```

In practice, if you need true absolute filesystem paths, you should avoid using absolute paths with `FileSystemResource` or `FileSystemXmlApplicationContext` and force the use of a `UrlResource` by using the `file:` URL prefix. The following examples show how to do so:

```
// actual context type doesn't matter, the Resource will always be UrlResource
ctx.getResource("file:///some/resource/path/myTemplate.txt");
// force this FileSystemXmlApplicationContext to load its definition via a UrlResource
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("file:///conf/context.xml");
```