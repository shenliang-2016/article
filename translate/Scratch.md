## 国际化网络资源

在现代互联网社区中，许多用户不再满足于仅使用ASCII符号来标识域名或Web资源。例如，他们希望能够使用阿拉伯语或中文的原生字符注册新域名。这就是为什么网络资源的国际化是扩大万维网视野的基石。

本课程介绍网络域名资源的国际化。

### 域名国际化

过去，Internet域名仅包含ASCII符号。随着互联网的普及并被全世界采用，有必要支持域名的国际化，特别是支持包含Unicode字符的域名。

采用国际化域名应用程序（IDNA）机制作为将Unicode字符转换为标准ASCII域名的标准，从而保持域名系统的稳定性。该系统执行查找服务以将用户友好名称转换为网络地址。

国际化域名的示例：

- `http://清华大学.cn`
- `http://www.транспорт.com`

如果您按照这些链接进行操作，您将看到地址栏中表示的Unicode域名被ASCII字符串替换。

为了在应用程序中实现类似的功能， [`java.net.IDN`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) 类提供了在ASCII和非ASCII格式之间转换域名的方法。

| Method                                   | Purpose                                  |
| ---------------------------------------- | ---------------------------------------- |
| [`toASCII(String)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toASCII-java.lang.String-)<br />[`toASCII(String, flag)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toASCII-java.lang.String-int-) | 在将IDN发送到域名解析系统或将IDN写入需要ASCII字符的文件（例如DNS主文件）之前使用。如果输入字符串不符合[RFC 3490](http://www.ietf.org/rfc/rfc3490.txt)，则这些方法会抛出`IllegalArgumentException`。 |
| [`toUnicode(String)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toUnicode-java.lang.String-)<br />[`toUnicode(String, flag)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toUnicode-java.lang.String-int-) | 在向用户显示名称时使用，例如从DNS区域获取的名称。此方法将字符串从ASCII兼容编码（ACE）转换为Unicode代码点。这种方法永远不会失败。如果出现错误，输入字符串保持不变，并且不加修改地返回。 |

可选的`flag`参数指定转换过程的行为。`ALLOW_UNASSIGNED`标志允许包含在Unicode 3.2中未分配的代码点。`USE_STD3_ASCII_RULES`标志确保遵守STD-3 ASCII规则。您可以单独使用这些标志，也可以逻辑“或”在一起使用。如果不需要任何标志，请使用该方法的单参数版本。

## 国际化服务提供者

国际化服务提供商支持依赖于语言环境的数据和服务的插件。因为可以插入依赖于语言环境的数据和服务，所以第三方能够提供在`java.text`和`java.util`包中大多数区域设置敏感类的实现。

服务是一组编程接口和类，可以访问特定应用程序的功能或特性。服务提供者接口（SPI）是服务定义的公共接口和抽象类的集合。服务提供商实现SPI。服务提供程序使您可以创建可扩展的应用程序，您可以在不修改其原始代码库的情况下进行扩展。您可以使用新的插件或模块增强其功能。有关服务提供程序和可扩展应用程序的更多信息，请参阅 [Creating Extensible Applications](https://docs.oracle.com/javase/tutorial/ext/basics/spi.html) 。

你可以使用国际化服务提供商来提供下面这些区域敏感类的自定义实现：

- [`BreakIterator`](https://docs.oracle.com/javase/8/docs/api/java/text/BreakIterator.html) 对象
- [`Collator`](https://docs.oracle.com/javase/8/docs/api/java/text/Collator.html) 对象
- 语言编码，国家编码，以及 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 类的变种名称
- 时区名称
- 货币符号
- [`DateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormat.html) 对象
- [`DateFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormatSymbols.html) 对象
- [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 对象
- [`DecimalFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormatSymbols.html) 对象

相应的 SPIs 被包含在 `java.text.spi` 和 `java.util.spi` 包中：

| `java.util.spi`                          | `java.text.spi`                          |
| ---------------------------------------- | ---------------------------------------- |
| [`CurrencyNameProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/CurrencyNameProvider.html)[`LocaleServiceProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/LocaleServiceProvider.html)[`TimeZoneNameProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/TimeZoneNameProvider.html) | [`BreakIteratorProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/BreakIteratorProvider.html)[`CollatorProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/CollatorProvider.html)[`DateFormatProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DateFormatProvider.html)[`DateFormatSymbolsProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DateFormatSymbolsProvider.html)[`DecimalFormatSymbolsProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DecimalFormatSymbolsProvider.html)[`NumberFormatProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/NumberFormatProvider.html) |

比如，如果你希望为一个新的区域提供 `NumberFormat` 对象，实现 `java.text.spi.NumberFormatProvider` 类并实现以下方法：

- `getCurrencyInstance(Locale locale)`
- `getIntegerInstance(Locale locale)`
- `getNumberInstance(Locale locale)`
- `getPercentInstance(Locale locale)`

```java
Locale loc = new Locale("da", "DK");
NumberFormat nf = NumberFormatProvider.getNumberInstance(loc);
```

这些方法首先检查Java运行时环境是否支持所请求的语言环境。如果是这样，方法使用该支持。否则，这些方法会调用已安装提供程序的`getAvailableLocales`方法以获取适当的接口，以查找支持所请求区域设置的提供程序。

有关如何使用服务提供程序进行国际化的深入示例，请参阅 [Installing a Custom Resource Bundle as an Extension](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html)。本节介绍如何实现[`ResourceBundleControlProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html) 接口，该接口使您可以使用任何自定义`ResourceBundle.Control`类，而无需对应用程序的源代码进行任何其他更改。

### 作为扩展安装自定义资源包

 [Customizing Resource Bundle Loading](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html) 一节介绍了如何更改资源包的加载方式。这涉及从[`ResourceBundle.Control`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.Control.html) 派生一个新类，然后通过调用以下方法检索资源包：

```java
ResourceBundle getBundle(
  String baseName,
  Locale targetLocale,
  ResourceBundle.Control control)
```

参数 `control` 是你的 `ResourceBundle.Control` 实现。

 [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html) 接口允许你改变下面方法加载资源包的方式：

```java
ResourceBundle getBundle(
  String baseName,
  Locale targetLocale)
```

请注意，此版本的 [`ResourceBundle.getBundle`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-java.util.Locale-) 方法不需要`ResourceBundle.Control`类的实例。`ResourceBundleControlProvider`是服务提供者接口（SPI）。SPI使您能够创建可扩展的应用程序，这些应用程序可以轻松扩展而无需修改其原始代码库。有关更多信息，请参阅 [Creating Extensible Applications](https://docs.oracle.com/javase/tutorial/ext/basics/spi.html) 。

要使用SPI，首先要通过实现类似`ResourceBundleControlProvider`的SPI来创建服务提供者。实现SPI时，指定它将如何提供服务。`ResourceBundleControlProvider` SPI提供的服务是在应用程序调用`ResourceBundle.getBundle(String baseName, Locale targetLocale)`方法时获取适当的`ResourceBundle.Control`实例。您将服务提供程序与Java扩展机制打包为已安装的扩展。运行应用程序时，不要在类路径中命名扩展名；运行时环境查找并加载这些扩展。

已安装的`ResourceBundleControlProvider` SPI实现替换了默认的`ResourceBundle.Control`类（它定义了默认的资源包加载过程）。因此，`ResourceBundleControlProvider`接口使您可以使用任何自定义`ResourceBundle.Control`类，而无需对应用程序的源代码进行任何其他更改。此外，此接口使您可以编写应用程序，而无需引用任何自定义ResourceBundle.Control类。

 [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java) 示例显示了如何实现`ResourceBundleControlProvider`接口以及如何将其打包为已安装的扩展。此示例包装在zip文件`RBCPTest.zip`中，包含以下文件：

- ```
  src
  ```

  - [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/java.util.spi.ResourceBundleControlProvider)

  - [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java)

  - ```
    rbcp
    ```

    - [`PropertiesResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControl.java)
    - [`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java)
    - [`XMLResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControl.java)
    - [`XMLResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControlProvider.java)

  - ```
    resources
    ```

    - [`RBControl.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl.properties)
    - [`RBControl_zh.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh.properties)
    - [`RBControl_zh_CN.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_CN.properties)
    - [`RBControl_zh_HK.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_HK.properties)
    - [`RBControl_zh_TW.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_TW.properties)
    - [`XmlRB.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/XmlRB.xml)
    - [`XmlRB_ja.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/XmlRB_ja.xml)

- ```
  lib
  ```

  - [`rbcontrolprovider.jar`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#package-provider)

- `build`: 包含打包在 `rbcontrolprovider.jar` 中的所有文件以及类文件 `RBCPTest.class`

- [`build.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/build.xml)

下面的步骤向你展示了如何重新创建 `RBCPTest.zip` 文件的内容，`RBCPTest`例子如何工作，以及如何运行它：

1. [创建 ResourceBundle.Control 类实现](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#create-implementations-of-resourcebundle.control)
2. [实现 ResourceBundleControlProvider 接口](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#implement-resourcebundlecontrolprovider)
3. [在你的应用中调用方法 ResourceBundle.getBundle](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#invoke-resourcebundle.getbundle)
4. [通过创建配置文件来注册服务提供者](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#register-service-provider)
5. [将服务提供者、它需要的类和配置文件到一个 JAR 包中](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#package-provider)
6. [运行 RBCPTest 程序](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#run-rbcptest)

**[1. 创建 ResourceBundle.Control 类实现]()**

 [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java) 示例使用 `ResourseBundle.Control` 的两种实现：

- [`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java):  `ResourceBundle.Control` 与在 [Customizing Resource Bundle Loading](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html) 中定义的 `ResourceBundle.Control` 实现相同。
- [`XMLResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControl.java): 此 `ResourceBundle.Control` 实现使用方法 [`Properties.loadFromXML`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#loadFromXML-java.io.InputStream-)加载基于 XML 的资源包。

**XML 属性文件**

如 [Backing a ResourceBundle with Properties Files](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html) 章节中所述，属性文件是简单的文本文件。其中每一行都是一个键值对。XML 属性文件类似于普通属性文件：它们同样包含键值对，除了是 XML 结构。下面的 XML 属性文件 `XmlRB.xml`：

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE properties [
<!ELEMENT properties ( comment?, entry* ) >
<!ATTLIST properties version CDATA #FIXED "1.0">
<!ELEMENT comment (#PCDATA) >
<!ELEMENT entry (#PCDATA) >
<!ATTLIST entry key CDATA #REQUIRED>
]>

<properties>
    <comment>Test data for RBCPTest.java</comment>
    <entry key="type">XML</entry>
</properties>
```

下面是等价的属性文本文件内容：

```
# Test data for RBCPTest.java
type = XML
```

所有的 XML 属性文件都具有相同的结构：

- 指定文档类型定义（DTD）的DOCTYPE声明：DTD定义XML文件的结构。**注意：**您可以在XML属性文件中使用以下DOCTYPE声明：

  ```
  <!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">  
  ```

  导出或导入属性时不访问系统URI（http://java.sun.com/dtd/properties.dtd）; 它是一个唯一标识XML属性文件的DTD的字符串。

 - 根元素`<properties>`：此元素包含所有其他元素。

 - 任意数量的`<comment>`元素：这些元素用于注释。

 - 任意数量的`<entry>`元素：使用属性`key`指定键; 指定`<entry>`标签之间的键值。

参考 [`Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) 类获取有关 XML 属性文件的更多信息。

**[2. 实现 ResourceBundleControlProvider 接口]()**

此接口包含一个方法，即 [`ResourceBundle.Control getControl(String baseName)`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html#getControl-java.lang.String-) 方法。参数`baseName`是资源包的名称。在`getBundle`的方法定义中，指定应该在给定资源包名称的情况下返回的`ResourceBundle.Control`实例。

`RBCPTest`示例包含`ResourceBundleControlProvider`接口的两个实现，[`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java) 和 [`XMLResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControlProvider.java)。如果资源包的基本名称以`resources.RBControl`开头（在此示例中，所有资源文件都包含在包 `resources`中），则`PropertiesResourceBundleControlProvider.getBundle`方法返回`PropertiesResourceBundleControl`的实例：

```java
package rbcp;

import java.util.ResourceBundle;
import java.util.spi.ResourceBundleControlProvider;

public class PropertiesResourceBundleControlProvider
    implements ResourceBundleControlProvider {
    static final ResourceBundle.Control PROPERTIESCONTROL =
        new PropertiesResourceBundleControl();

    public ResourceBundle.Control getControl(String baseName) {
        System.out.println("Class: " + getClass().getName() + ".getControl");
        System.out.println("    called for " + baseName);

        // Throws a NPE if baseName is null.
        if (baseName.startsWith("resources.RBControl")) {
            System.out.println("    returns " + PROPERTIESCONTROL);
            return PROPERTIESCONTROL;
        }
        System.out.println("    returns null");
        System.out.println();
        return null;
    }
}
```

类似地，如果资源包的基本名称以`resources.Xml`开头，则`XMLResourceBundleControlProvider.getControl`方法返回`XMLResourceBundleControl`的实例。

注意：您可以创建`ResourceBundleControlProvider`接口的一个实现，该实现返回`PropertiesResourceBundleControl`或`XMLResourceBundleControl`的实例，具体取决于基本名称。

**[3. 在你的应用中调用方法 ResourceBundle.getBundle]()**

 `RBCPTest` 类使用方法 [`ResourceBundle.getBundle`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-java.util.Locale-) 检索资源包：

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class RBCPTest {
    public static void main(String[] args) {
        ResourceBundle rb = ResourceBundle.getBundle(
            "resources.XmlRB", Locale.ROOT);
        String type = rb.getString("type");
        System.out.println("Root locale. Key, type: " + type);
        System.out.println();

        rb = ResourceBundle.getBundle("resources.XmlRB", Locale.JAPAN);
        type = rb.getString("type");
        System.out.println("Japan locale. Key, type: " + type);
        System.out.println();

        test(Locale.CHINA);
        test(new Locale("zh", "HK"));
        test(Locale.TAIWAN);
        test(Locale.CANADA);
    }

    private static void test(Locale locale) {
        ResourceBundle rb = ResourceBundle.getBundle(
            "resources.RBControl", locale);
        System.out.println("locale: " + locale);
        System.out.println("    region: " + rb.getString("region"));
        System.out.println("    language: " + rb.getString("language"));
        System.out.println();
    }
}
```

请注意，此类中不会出现`ResourceBundle.Control`或`ResourceBundleControlProvider`的任何实现。由于`ResourceBundleControlProvider`接口使用Java扩展机制，因此运行时环境会查找并加载这些实现。但是，使用 [`ServiceLoader`](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) 类加载与Java扩展机制一起安装的`ResourceBundleControlProvider`实现和其他服务提供程序。使用此类意味着您必须使用配置文件注册服务提供程序，这将在下一步中介绍。

**[4. 通过创建配置文件来注册服务提供者]()**

配置文件的名称是提供程序实现的接口或类的完全限定名称。配置文件包含提供程序的完全限定类名。 [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/java.util.spi.ResourceBundleControlProvider) 文件包含`PropertiesResourceBundleControlProvider`和`XMLResourceBundleControlProvider`的完全限定名称，每行一个名称：

```java
rbcp.XMLResourceBundleControlProvider
rbcp.PropertiesResourceBundleControlProvider
```

**[5. 将服务提供者、它需要的类和配置文件到一个 JAR 包中]()**

编译源文件。从包含`build.xml`文件的目录，运行下面的命令：

```
javac -d build src/java.* src/rbcp/*.java
```

此命令将编译`src`目录中包含的源文件，并将类文件放在`build`目录中。在Windows上，请确保使用反斜杠（\）分隔目录和文件名。

创建一个JAR文件，其中包含以下目录结构中的已编译类文件，资源文件和配置文件：

- ```
  META-INF
  ```

  - ```
    services
    ```

    - `java.util.spi.ResourceBundleControlProvider`

- ```
  rbcp
  ```

  - `PropertiesResourceBundleControl.class`
  - `PropertiesResourceBundleControlProvider.class`
  - `XMLResourceBundleControl.class`
  - `XMLResourceBundleControlProvider.class`

- ```
  resources
  ```

  - `RBControl.properties`
  - `RBControl_zh.properties`
  - `RBControl_zh_CN.properties`
  - `RBControl_zh_HK.properties`
  - `RBControl_zh_TW.properties`
  - `XmlRB.xml`
  - `XmlRB_ja.xml`

请注意，配置文件`java.util.spi.ResourceBundleControlProvider`必须打包在目录`/META-INF/services`中。此示例将这些文件打包到`lib`目录中的JAR文件`rbcontrolprovider.jar`中。

参考 [Packaging Programs in JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) 获取有关创建 JAR 文件的更多信息。

或者，下载并安装 [Apache Ant](http://ant.apache.org/) ，这是一个使您能够自动化构建过程的工具，例如编译Java文件和创建JAR文件。确保Apache Ant可执行文件位于`PATH`环境变量中，以便您可以从任何目录运行它。安装Apache Ant后，请按照下列步骤操作：

1. 编辑文件 [`build.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/build.xml) 并修改 `${JAVAC}` 为你的 Java 编译器、 `javac` 的完整路径名，修改 `${JAVA}` 为你的 Java 可执行运行时`java`的完整路径名。 

2. 从包含文件`build.xml`的同一目录运行以下命令：

   ```
   ant jar
   ```

   此命令编译Java源文件，并将它们以及所需的资源和配置文件打包到`lib`目录中的JAR文件`rbcontrolprovider.jar`中。

**[6. 运行 RBCPTest 程序]()**

在命令提示符处，从包含`build.xml`文件的目录运行以下命令：

```
java -Djava.ext.dirs=lib -cp build RBCPTest
```

此命令假定以下内容：

 - 包含RBCPTest示例的已编译代码的JAR文件位于目录`lib`中。
 - 编译的类`RBCPTest.class`位于 `build` 目录中。

或者，使用Apache Ant并从包含`build.xml`文件的目录运行以下命令：

```
ant run
```

安装Java扩展时，通常将扩展的JAR文件放在JRE的`lib/ext`目录中。但是，此命令指定包含具有系统属性`java.ext.dirs`的Java扩展的目录。

`RBCPTest`程序首先尝试使用基本名称`resources.XmlRB`和语言环境`Locale.ROOT`和`Local.JAPAN`检索资源包。检索这些资源包的程序输出类似于以下内容：

```
Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.XmlRB
    returns rbcp.XMLResourceBundleControl@16c1857
Root locale. Key, type: XML

Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.XmlRB
    returns rbcp.XMLResourceBundleControl@16c1857
Japan locale. Key, type: Value from Japan locale
```

该程序成功获取`XMLResourceBundleControl`的实例，并访问属性文件`XmlRB.xml`和`XmlRB_ja.xml`。

当`RBCPTest`程序尝试检索资源包时，它会调用配置文件`java.util.spi.ResourceBundleControlProvider`中定义的所有类。例如，当程序检索具有基本名称`resources.RBControl`和区域设置`Locale.CHINA`的资源包时，它将打印以下输出：

```
Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.RBControl
    returns null

Class: rbcp.PropertiesResourceBundleControlProvider.getControl
    called for resources.RBControl
    returns rbcp.PropertiesResourceBundleControl@1ad2911
locale: zh_CN
    region: China
    language: Simplified Chinese
```
