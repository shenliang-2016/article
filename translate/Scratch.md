#### 其他配置工具

以下是一些其他配置实用程序的摘要。

*Preferences API*允许应用程序在依赖于实现的后备存储中存储和检索配置数据。支持异步更新，并且多个线程甚至多个应用程序可以安全地更新同一组首选项。有关更多信息，请参阅  [Preferences API Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/preferences/index.html) 。

部署在*JAR*包中的应用程序使用清单来描述存档的内容。有关更多信息，请参阅 [Packaging Programs in JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) 课程。

*Java Web Start应用程序*的配置包含在*JNLP*文件中。有关更多信息，请参阅 [Java Web Start](https://docs.oracle.com/javase/tutorial/deployment/webstart/index.html) 课程。

*Java Plug-in applet*的配置部分取决于用于在网页中嵌入applet的HTML标记。这些标记可以包含 `<applet>`, `<object>`, `<embed>`, 和 `<param>`，具体取决于applet和浏览器。有关更多信息，请参阅 [Java Applets](https://docs.oracle.com/javase/tutorial/deployment/applet/index.html) 课程。

 [`java.util.ServiceLoader`](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) 类提供了一个简单的服务提供者工具。服务提供者是服务的实现 - 一组众所周知的接口和（通常是抽象的）类。服务提供者中的类通常实现接口并子类化服务中定义的类。可以将服务提供程序安装为扩展（请参阅 [The Extension Mechanism](https://docs.oracle.com/javase/tutorial/ext/index.html) ）。通过将提供者添加到类路径或通过其他特定于平台的方式，也可以使提供者可用。

### 系统工具

 [`System`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html) 类实现了许多系统实用程序。其中一些已在上一节 [Configuration Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/config.html) 中介绍过。本节介绍一些其他系统实用程序。

#### 命令行 I/O 对象

`System` 提供了几个预定义的I/O对象，这些对象在Java应用程序中非常有用，可以从命令行启动。它们实现了大多数操作系统提供的标准I/O流，以及用于输入密码的控制台对象。有关更多信息，请参阅 [Basic I/O](https://docs.oracle.com/javase/tutorial/essential/io/index.html) 课程中 [I/O from the Command Line](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) 。

#### 系统属性

在 [Properties](https://docs.oracle.com/javase/tutorial/essential/environment/properties.html) 中，我们检查了应用程序可以使用`Properties`对象来维护其配置的方式。Java平台本身使用`Properties`对象来维护自己的配置。`System`类维护一个`Properties`对象，该对象描述当前工作环境的配置。系统属性包括有关当前用户，Java运行时的当前版本以及用于分隔文件路径名的组件的字符的信息。

下表描述了一些最重要的系统属性。

| Key                 | Meaning                                                      |
| ------------------- | ------------------------------------------------------------ |
| `"file.separator"`  | Character that separates components of a file path. This is "`/`" on UNIX and "`\`" on Windows. |
| `"java.class.path"` | Path used to find directories and JAR archives containing class files. Elements of the class path are separated by a platform-specific character specified in the `path.separator` property. |
| `"java.home"`       | Installation directory for Java Runtime Environment (JRE)    |
| `"java.vendor"`     | JRE vendor name                                              |
| `"java.vendor.url"` | JRE vendor URL                                               |
| `"java.version"`    | JRE version number                                           |
| `"line.separator"`  | Sequence used by operating system to separate lines in text files |
| `"os.arch"`         | Operating system architecture                                |
| `"os.name"`         | Operating system name                                        |
| `"os.version"`      | Operating system version                                     |
| `"path.separator"`  | Path separator character used in `java.class.path`           |
| `"user.dir"`        | User working directory                                       |
| `"user.home"`       | User home directory                                          |
| `"user.name"`       | User account name                                            |

----

**安全性考虑：**  [Security Manager](https://docs.oracle.com/javase/tutorial/essential/environment/security.html) 可以限制对系统属性的访问。这通常是applet中的一个问题，它无法读取某些系统属性，也无法编写任何系统属性。有关在applet中访问系统属性的更多信息，请参阅 [Doing More With Java Rich Internet Applications](https://docs.oracle.com/javase/tutorial/deployment/doingMoreWithRIA/index.html) 课程中的 [System Properties](https://docs.oracle.com/javase/tutorial/deployment/doingMoreWithRIA/properties.html) 。

----

**读取系统属性**

`System`类有两个用于读取系统属性的方法：`getProperty`和`getProperties`。

`System`类有两个不同版本的`getProperty`。两者都检索参数列表中指定的属性的值。两个`getProperty`方法中较简单的方法是一个参数，一个属性键。例如，要获取`path.separator`的值，请使用以下语句：

```java
System.getProperty("path.separator");
```

`getProperty`方法返回一个包含该属性值的字符串。如果该属性不存在，则此版本的`getProperty`返回`null`。

另一个版本的`getProperty`需要两个`String`参数：第一个参数是要查找的键，第二个参数是如果找不到键或者没有值则返回的默认值。例如，以下对`getProperty`的调用会查找名为`subliminal.message`的`System`属性。这不是一个有效的系统属性，因此这个方法不是返回`null`，而是返回作为第二个参数提供的默认值：“`Buy StayPuft Marshmallows！`”

```java
System.getProperty("subliminal.message", "Buy StayPuft Marshmallows!");
```

`System`类提供的访问属性值的最后一个方法是`getProperties`方法，它返回一个 [`Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) 对象。该对象包含一组完整的系统属性定义。

**写入系统属性**

要修改现有的系统属性集，请使用`System.setProperties`。此方法采用已初始化为包含要设置的属性的`Properties`对象。此方法使用`Properties`对象表示的新集合替换整个系统属性集。

----

**警告：** 更改系统属性具有潜在危险，应谨慎处理。启动后不会重读许多系统属性，这些属性仅供参考。更改某些属性可能会产生意外的副作用。

----

下一个例子，[`PropertiesTest`](https://docs.oracle.com/javase/tutorial/essential/environment/examples/PropertiesTest.java)，创建一个 `Properties` 对象并从 [`myProperties.txt`](https://docs.oracle.com/javase/tutorial/essential/environment/examples/myProperties.txt) 初始化它。

```java
subliminal.message=Buy StayPuft Marshmallows!
```

`PropertiesTest` 接下来使用 `System.setProperties` 来安装新的 `Properties` 对象作为当前系统属性集合。

```java
import java.io.FileInputStream;
import java.util.Properties;

public class PropertiesTest {
    public static void main(String[] args)
        throws Exception {

        // set up new properties object
        // from file "myProperties.txt"
        FileInputStream propFile =
            new FileInputStream( "myProperties.txt");
        Properties p =
            new Properties(System.getProperties());
        p.load(propFile);

        // set the system properties
        System.setProperties(p);
        // display new properties
        System.getProperties().list(System.out);
    }
}
```

注意`PropertiesTest`如何创建`Properties`对象，`p`，它被用作`setProperties`的参数：

```java
Properties p = new Properties(System.getProperties());
```

此语句使用当前系统属性集初始化新属性对象`p`，在这个小应用程序的情况下，它是由运行时系统初始化的属性集。然后，应用程序从文件`myProperties.txt`将其他属性加载到`p`中，并将系统属性设置为`p`。这具有将`myProperties.txt`中列出的属性添加到运行时系统在启动时创建的属性集的效果。请注意，应用程序可以创建`p`而不使用任何默认的`Properties`对象，如下所示：

```java
Properties p = new Properties();
```

另请注意，系统属性的值可以被覆盖！例如，如果`myProperties.txt`包含以下行，则将覆盖`java.vendor`系统属性：

```java
java.vendor=Acme Software Company
```

通常，请注意不要覆盖系统属性。

`setProperties`方法更改当前正在运行的应用程序的系统属性集。这些变化并不持久。也就是说，更改应用程序中的系统属性不会影响将来对此解释程序或任何其他应用程序的Java解释程序的调用。运行时系统每次启动时都会重新初始化系统属性。如果要保持对系统属性的更改，则应用程序必须在退出之前将值写入某个文件，并在启动时再次读取它们。

