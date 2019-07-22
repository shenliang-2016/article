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

##### Registering Additional Custom `PropertyEditor` Implementations

When setting bean properties as string values, a Spring IoC container ultimately uses standard JavaBeans `PropertyEditor`implementations to convert these strings to the complex type of the property. Spring pre-registers a number of custom `PropertyEditor` implementations (for example, to convert a class name expressed as a string into a `Class` object). Additionally, Java’s standard JavaBeans `PropertyEditor` lookup mechanism lets a `PropertyEditor` for a class be named appropriately and placed in the same package as the class for which it provides support, so that it can be found automatically.

If there is a need to register other custom `PropertyEditors`, several mechanisms are available. The most manual approach, which is not normally convenient or recommended, is to use the `registerCustomEditor()` method of the`ConfigurableBeanFactory` interface, assuming you have a `BeanFactory` reference. Another (slightly more convenient) mechanism is to use a special bean factory post-processor called `CustomEditorConfigurer`. Although you can use bean factory post-processors with `BeanFactory` implementations, the `CustomEditorConfigurer` has a nested property setup, so we strongly recommend that you use it with the `ApplicationContext`, where you can deploy it in similar fashion to any other bean and where it can be automatically detected and applied.

Note that all bean factories and application contexts automatically use a number of built-in property editors, through their use a `BeanWrapper` to handle property conversions. The standard property editors that the `BeanWrapper` registers are listed in the [previous section](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion). Additionally, `ApplicationContexts` also override or add additional editors to handle resource lookups in a manner appropriate to the specific application context type.

Standard JavaBeans `PropertyEditor` instances are used to convert property values expressed as strings to the actual complex type of the property. You can use `CustomEditorConfigurer`, a bean factory post-processor, to conveniently add support for additional `PropertyEditor` instances to an `ApplicationContext`.

Consider the following example, which defines a user class called `ExoticType` and another class called `DependsOnExoticType`, which needs `ExoticType` set as a property:

```
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

When things are properly set up, we want to be able to assign the type property as a string, which a `PropertyEditor` converts into an actual `ExoticType` instance. The following bean definition shows how to set up this relationship:

```
<bean id="sample" class="example.DependsOnExoticType">
    <property name="type" value="aNameForExoticType"/>
</bean>
```

The `PropertyEditor` implementation could look similar to the following:

```
// converts string representation to ExoticType object
package example;

public class ExoticTypeEditor extends PropertyEditorSupport {

    public void setAsText(String text) {
        setValue(new ExoticType(text.toUpperCase()));
    }
}
```

Finally, the following example shows how to use `CustomEditorConfigurer` to register the new `PropertyEditor` with the`ApplicationContext`, which will then be able to use it as needed:

```
<bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="customEditors">
        <map>
            <entry key="example.ExoticType" value="example.ExoticTypeEditor"/>
        </map>
    </property>
</bean>
```

###### Using `PropertyEditorRegistrar`

Another mechanism for registering property editors with the Spring container is to create and use a `PropertyEditorRegistrar`. This interface is particularly useful when you need to use the same set of property editors in several different situations. You can write a corresponding registrar and reuse it in each case. `PropertyEditorRegistrar` instances work in conjunction with an interface called `PropertyEditorRegistry`, an interface that is implemented by the Spring `BeanWrapper` (and `DataBinder`). `PropertyEditorRegistrar` instances are particularly convenient when used in conjunction with `CustomEditorConfigurer`(described [here](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion-customeditor-registration)), which exposes a property called `setPropertyEditorRegistrars(..)`. `PropertyEditorRegistrar` instances added to a `CustomEditorConfigurer` in this fashion can easily be shared with `DataBinder` and Spring MVC controllers. Furthermore, it avoids the need for synchronization on custom editors: A `PropertyEditorRegistrar` is expected to create fresh `PropertyEditor` instances for each bean creation attempt.

The following example shows how to create your own `PropertyEditorRegistrar` implementation:

```
package com.foo.editors.spring;

public final class CustomPropertyEditorRegistrar implements PropertyEditorRegistrar {

    public void registerCustomEditors(PropertyEditorRegistry registry) {

        // it is expected that new PropertyEditor instances are created
        registry.registerCustomEditor(ExoticType.class, new ExoticTypeEditor());

        // you could register as many custom property editors as are required here...
    }
}
```

See also the `org.springframework.beans.support.ResourceEditorRegistrar` for an example `PropertyEditorRegistrar`implementation. Notice how in its implementation of the `registerCustomEditors(..)` method ,it creates new instances of each property editor.

The next example shows how to configure a `CustomEditorConfigurer` and inject an instance of our`CustomPropertyEditorRegistrar` into it:

```
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

Finally (and in a bit of a departure from the focus of this chapter for those of you using [Spring’s MVC web framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc)), using `PropertyEditorRegistrars` in conjunction with data-binding `Controllers` (such as `SimpleFormController`) can be very convenient. The following example uses a `PropertyEditorRegistrar` in the implementation of an `initBinder(..)` method:

```
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

This style of `PropertyEditor` registration can lead to concise code (the implementation of `initBinder(..)` is only one line long) and lets common `PropertyEditor` registration code be encapsulated in a class and then shared amongst as many `Controllers`as needed.