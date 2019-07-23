#### 3.3.2 内建的 `PropertyEditor` 实现

Spring 使用`PropertyEditor`的概念来实现`Object`和`String`之间的转换。以与对象本身不同的方式表示属性可能很方便。例如，`Date`可以用人类可读的方式表示（如`String`：`'2007-14-09'`），而我们仍然可以将人类可读的形式转换回原始日期（或者更好的是，转换任何以人类可读的形式输入的日期为`Date`对象）。可以通过注册`java.beans.PropertyEditor`类型的自定义编辑器来实现此行为。在`BeanWrapper`上注册自定义编辑器，或者在特定的IoC容器中注册自定义编辑器（如前一章所述），使其了解如何将属性转换为所需类型。有关`PropertyEditor`的更多信息，请参阅 [Oracle的java.beans包的javadoc](https://docs.oracle.com/javase/8/docs/api/java/beans/package-summary.html) 。

在 Spring 中使用属性编辑的几个例子：

- 通过使用`PropertyEditor`实现来完成 beans 属性的设置。当你使用`String`作为你在 XML 中声明的一些 bean 的属性的值时，Spring（如果该属性的 setter 拥有一个`Class`参数）使用`ClassEditor`尝试解析该参数为一个`Class`对象。
- 在Spring的MVC框架中解析HTTP请求参数是通过使用可以在`CommandController`的所有子类中手动绑定的各种`PropertyEditor`实现来完成的。

Spring 拥有若干内建的`PropertyEditor`实现以方便使用。它们都放在`org.springframework.beans.propertyeditors`包中。大多数（不是所有，如下表中所示）都是，默认地，由`BeanWrapperImpl`注册。属性编辑器也以同样方式配置。你仍然可以注册你自己的变体来覆盖默认的。下表描述了 Spring 提供的各种`PropertyEditor`实现：

| 类                         | 解释                                       |
| ------------------------- | ---------------------------------------- |
| `ByteArrayPropertyEditor` | 字节数组编辑器。将字符串转化为相应的字节表示。默认通过`BeanWrapperImpl`注册。 |
| `ClassEditor`             | 将表示类的字符串解析为实际的类，或者执行逆向转换。当一个类没有找到，抛出`IllegalArgumentException`。默认地由`BeanWrapperImpl`注册。 |
| `CustomBooleanEditor`     | `Boolean`属性的可自定义属性编辑器。默认情况下，由`BeanWrapperImpl`注册。但可以通过将其自定义实例注册为自定义编辑器来覆盖。 |
| `CustomCollectionEditor`  | 集合的属性编辑器，将任何源`Collection`转换为给定的目标`Collection`类型。 |
| `CustomDateEditor`        | `java.util.Date`的可自定义属性编辑器，支持自定义`DateFormat`。没有默认注册。必须根据需要使用适当的格式进行注册。 |
| `CustomNumberEditor`      | 任何`Number`子类的可自定义属性编辑器，例如`Intege`r，`Long`，`Float`或`Double`。默认情况下，由`BeanWrapperImpl`注册，但可以通过将其自定义实例注册为自定义编辑器来覆盖。 |
| `FileEditor`              | 将字符串解析为 `java.io.File` 对象。默认情况下，由`BeanWrapperImpl`注册。 |
| `InputStreamEditor`       | 单向属性编辑器，可以获取字符串并生成（通过中间`ResourceEditor`和`Resource`）`InputStream`，以便`InputStream`属性可以直接以字符串形式设置。请注意，默认用法不会为您关闭`InputStream`。默认情况下，由`BeanWrapperImpl`注册。 |
| `LocaleEditor`            | 可以将字符串解析为`Locale`对象，反之亦然（字符串格式为`*[country]*[variant]`，与`Locale`的`toString()`方法相同）。默认情况下，由`BeanWrapperImpl`注册。 |
| `PatternEditor`           | 可以将字符串解析为`java.util.regex.Pattern`对象，反之亦然。 |
| `PropertiesEditor`        | 可以将字符串（使用`java.util.Properties`类的javadoc中定义的格式进行格式化）转换为`Properties`对象。默认情况下，由`BeanWrapperImpl`注册。 |
| `StringTrimmerEditor`     | 修剪字符串的属性编辑器。允许有选择性地将空字符串转换为`null`。默认情况下未注册 - 必须是用户注册的。 |
| `URLEditor`               | 可以将URL的字符串表示形式解析为实际的`URL`对象。 默认情况下，由`BeanWrapperImpl`注册。 |

Spring使用`java.beans.PropertyEditorManager`来设置可能需要的属性编辑器的搜索路径。搜索路径还包括`sun.bean.editors`，其中包括`Font`，`Color`和大多数基本类型等类型的`PropertyEditor`实现。另请注意，标准JavaBeans基础结构会自动发现`PropertyEditorclasses`（无需显式注册），如果它们与它们处理的类位于同一个包中，并且与该类具有相同的名称，并附加了`Editor`。例如，可以使用以下类和包结构，这足以使`SomethingEditor`类被识别并用作`Something-typed`属性的`PropertyEditor`。

```
com
  chank
    pop
      Something
      SomethingEditor // the PropertyEditor for the Something class
```

请注意，您也可以在此处使用标准`BeanInfo` JavaBeans机制（描述在 [这里](https://docs.oracle.com/javase/tutorial/javabeans/advanced/customization.html) ）。以下示例使用`BeanInfo`机制显式注册一个或多个`PropertyEditor`：

```
com
  chank
    pop
      Something
      SomethingBeanInfo // the BeanInfo for the Something class
```

以下引用的`SomethingBeanInfo`类的Java源代码将`CustomNumberEditor`与`Something`类的`age`属性相关联：

```java
public class SomethingBeanInfo extends SimpleBeanInfo {

    public PropertyDescriptor[] getPropertyDescriptors() {
        try {
            final PropertyEditor numberPE = new CustomNumberEditor(Integer.class, true);
            PropertyDescriptor ageDescriptor = new PropertyDescriptor("age", Something.class) {
                public PropertyEditor createPropertyEditor(Object bean) {
                    return numberPE;
                };
            };
            return new PropertyDescriptor[] { ageDescriptor };
        }
        catch (IntrospectionException ex) {
            throw new Error(ex.toString());
        }
    }
}
```

##### 注册额外的自定义 `PropertyEditor` 实现

当使用字符串值设置 bean 属性时，Spring IoC 容器最终使用标准的 JavaBeans`PropertyEditor`实现将这些字符串转化为属性的复杂类型。Spring 预注册了一系列的自定义`PropertyEditor`实现（比如，转化表示类名的字符串为`Class`对象）。更进一步，Java 的标准 JavaBeans`PropertyEditor`查找机制要求一个类的`PropertyEditor`应该被合适地命名，并放在它所支持的类同一个包中，从而保证它可以被自动发现。

如果需要注册其它自定义`PropertyEditor`，存在几种机制可以使用。手动程度最高的方法，通常不方便也不推荐，是使用`ConfigurableBeanFactory`接口的`registerCustomEditor()`方法，假定你拥有一个`BeanFactory`引用。另一种机制（稍微方便一点）使用一种特殊的 bean 工厂后处理器，名为`CustomEditorConfigurer`。尽管你可以与`BeanFactory`实现一起使用 bean 工厂后处理器，`CustomEditorConfigurer`拥有一个嵌套属性设置，因而我们强烈推荐你将其和`ApplicationContext`一起使用，此时你可以与所有其它 bean 一样部署它，它同样可以被自动侦测并应用。

注意，所有 bean 工厂和应用上下文都会自动使用一系列内建的属性编辑器，通过它们使用`BeanWrapper`处理属性转化。上一章节中列出了`BeanWrapper`注册的标准属性编辑器。另外，`ApplicationContext`也覆盖或者添加了额外的编辑器来处理资源，这些资源按照特定与应用上下文类型的方式查找。

标准 JavaBeans`PropertyEditor`实例被用来将表示为字符串的属性值转化为实际的属性复杂类型。你可以使用`CustomEditorConfigurer`，这是一个 bean 工厂后处理器，来方便地向`ApplicationContext`添加额外的`PropertyEditor`支持。

考虑下面的例子，定义了一个名为`ExoticType`的用户类以及另外一个类`DependsOnExoticType`，它需要`ExoticType`实例设定为属性：

```java
package example;

public class ExoticType {

    private String name;

    public ExoticType(String name) {
        this.name = name;
    }
}

public class DependsOnExoticType {

    private ExoticType type;

    public void setType(ExoticType type) {
        this.type = type;
    }
}
```

正确设置后，我们希望能够将`type`属性指定为字符串，`PropertyEditor`将其转换为实际的`ExoticType`实例。以下bean定义显示了如何设置此关系：

```xml
<bean id="sample" class="example.DependsOnExoticType">
    <property name="type" value="aNameForExoticType"/>
</bean>
```

`PropertyEditor`实现大概是下面这个样子：

```java
// converts string representation to ExoticType object
package example;

public class ExoticTypeEditor extends PropertyEditorSupport {

    public void setAsText(String text) {
        setValue(new ExoticType(text.toUpperCase()));
    }
}
```

最后，下面的示例演示如何使用`CustomEditorConfigurer`向`ApplicationIntext`注册新的`PropertyEditor`，然后可以根据需要使用它：

```xml
<bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="customEditors">
        <map>
            <entry key="example.ExoticType" value="example.ExoticTypeEditor"/>
        </map>
    </property>
</bean>
```

###### 使用 `PropertyEditorRegistrar`

使用 Spring 容器注册属性编辑器的另一种机制是创建和使用`PropertyEditorRegistrar`。当您需要在几种不同情况下使用同一组属性编辑器时，此接口特别有用。您可以编写相应的注册器，并在每种情况下重复使用它。`PropertyEditorRegistrar`实例与名为`PropertyEditorRegistry`的接口一起工作，该接口由 Spring `BeanWrapper`（和`DataBinder`）实现。`PropertyEditorRegistrar`实例在与`CustomEditorConfigurer`（[此处](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion-customeditor-registration) 描述）结合使用时特别方便，它公开了一个名为`setPropertyEditorRegistrars(..)`的方法。以这种方式添加到`CustomEditorConfigurer`的`PropertyEditorRegistrar`实例可以很容易地与`DataBinder`和 Spring MVC 控制器共享。此外，它避免了在自定义编辑器上进行同步的需要：`PropertyEditorRegistrar`需要为每个 bean 创建尝试创建新的`PropertyEditor`实例。

下面的例子展示了如何创建你自己的`PropertyEditorRegistrar`实现：

```java
package com.foo.editors.spring;

public final class CustomPropertyEditorRegistrar implements PropertyEditorRegistrar {

    public void registerCustomEditors(PropertyEditorRegistry registry) {

        // it is expected that new PropertyEditor instances are created
        registry.registerCustomEditor(ExoticType.class, new ExoticTypeEditor());

        // you could register as many custom property editors as are required here...
    }
}
```

另请参阅`org.springframework.beans.support.ResourceEditorRegistrar`以获取`PropertyEditorRegistrar`实现示例。请注意，在实现 `registerCustomEditors(..)` 方法时，它会创建每个属性编辑器的新实例。

下一个示例显示如何配置`CustomEditorConfigurer`并将我们的`CustomPropertyEditorRegistrar`实例注入其中：

```xml
<bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="propertyEditorRegistrars">
        <list>
            <ref bean="customPropertyEditorRegistrar"/>
        </list>
    </property>
</bean>

<bean id="customPropertyEditorRegistrar"
    class="com.foo.editors.spring.CustomPropertyEditorRegistrar"/>
```

最后（与本章的重点有所不同，对于那些使用 [Spring的MVC Web框架](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc) 的人来说），使用`PropertyEditorRegistrars`和数据绑定 `Controllers`（如`SimpleFormController`）会非常方便。以下示例在`initBinder(..)`方法的实现中使用`PropertyEditorRegistrar`：

```java
public final class RegisterUserController extends SimpleFormController {

    private final PropertyEditorRegistrar customPropertyEditorRegistrar;

    public RegisterUserController(PropertyEditorRegistrar propertyEditorRegistrar) {
        this.customPropertyEditorRegistrar = propertyEditorRegistrar;
    }

    protected void initBinder(HttpServletRequest request,
            ServletRequestDataBinder binder) throws Exception {
        this.customPropertyEditorRegistrar.registerCustomEditors(binder);
    }

    // other methods to do with registering a User
}
```

这种`PropertyEditor`注册方式会导致简洁的代码（`initBinder(..)`的实现只有一行），并允许将公共`PropertyEditor`注册代码封装在一个类中，然后在所需的 `Controllers`之间共享。

