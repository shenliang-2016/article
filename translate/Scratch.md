#### 1.15.1 使用`MessageSource`进行国际化

`ApplicationContext`接口还继承了名为`MessageSource`的接口，因而，提供了国际化（i18n）功能。Spring 还提供了`HierarchicalMessageSource`接口，该接口可以杰斯消息层级结构。综上所述，这些接口提供了 Spring 有效消息解析所需要的基础功能。这些接口定义的方法包括：

- `String getMessage(String code, Object[] args, String default, Locale loc)`: 从`MessageSource`获取消息的基本方法。如果特定语言的消息没有找到，则使用默认消息。传入的任何参数都会编程替换值，使用标准类库提供的`MessageFormat`功能。
- `String getMessage(String code, Object[] args, Locale loc)`: 与上面的方法基本相同，但有一点不同：无法指定默认消息。如果找不到默认消息，则抛出`NoSuchMessageException`。
- `String getMessage(MessageSourceResolvable resolvable, Locale locale)`: 上述方法中使用的所有属性也包装在名为`MessageSourceResolvable`的类中，您可以将该类与此方法一起使用。

加载`ApplicationContext`时，它会自动搜索在上下文中定义的`MessageSource` bean。该bean必须具有名称`messageSource`。如果找到这样的bean，则对前面方法的所有调用都被委托给消息源。如果未找到任何消息源，`ApplicationContext`将尝试查找包含具有相同名称的bean的父类。如果是，则将该bean用作`MessageSource`。如果`ApplicationContext`仍然找不到任何消息源，则会实例化一个空的`DelegatingMessageSource`，以便能够接受对上面定义的方法的调用。

Spring 提供了两种`MessageSource`实现，`ResourceBundleMessageSource`和`StaticMessageSource`，两者都实现了`HierarchicalMessageSource`以便嵌套消息源。`StaticMessageSource`很少使用，不过它提供了编程方式向消息源添加消息的方法。下面的例子展示了`ResourceBundleMessageSource`：

```xml
<beans>
    <bean id="messageSource"
            class="org.springframework.context.support.ResourceBundleMessageSource">
        <property name="basenames">
            <list>
                <value>format</value>
                <value>exceptions</value>
                <value>windows</value>
            </list>
        </property>
    </bean>
</beans>
```

这个例子假定你在类路径下定义了三个资源包，名为`format`、`exception`和`windows`。任何涉及到消息的请求都会以 JDK 标准方式被处理，通过`ResourceBundle`对象来解析消息。为了举例子，假定两个资源包文件内容如下：

```
# in format.properties
message=Alligators rock!
```

```
# in exceptions.properties
argument.required=The {0} argument is required.
```

下面的例子展示了一个执行`MessageSource`功能的程序。记住所有的`ApplicationContext`实现同时也是`MessageSource`实现，因此可以被转化为`MessageSource`接口：

```java
public static void main(String[] args) {
    MessageSource resources = new ClassPathXmlApplicationContext("beans.xml");
    String message = resources.getMessage("message", null, "Default", null);
    System.out.println(message);
}
```

上面的程序输入如下：

```
Alligators rock!
```

总而言之，`MessageSource`在名为`beans.xml`的文件中定义，该文件存在于类路径的根目录中。`messageSource` bean定义通过其`basenames`属性引用许多资源包。以列表形式传递给`basenames`属性的三个文件名作为类路径根目录下的文件存在，分别称为`format.properties`，`exceptions.properties`和`windows.properties`。

下面的例子展示了传递给消息查找的参数。这些参数被转化为`String`对象并插入查找消息中的占位符中：

```xml
<beans>

    <!-- this MessageSource is being used in a web application -->
    <bean id="messageSource" class="org.springframework.context.support.ResourceBundleMessageSource">
        <property name="basename" value="exceptions"/>
    </bean>

    <!-- lets inject the above MessageSource into this POJO -->
    <bean id="example" class="com.something.Example">
        <property name="messages" ref="messageSource"/>
    </bean>

</beans>
```

```java
public class Example {

    private MessageSource messages;

    public void setMessages(MessageSource messages) {
        this.messages = messages;
    }

    public void execute() {
        String message = this.messages.getMessage("argument.required",
            new Object [] {"userDao"}, "Required", null);
        System.out.println(message);
    }
}
```

`execute()` 方法调用输出：

```
The userDao argument is required.
```

关于国际化（“i18n”），Spring的各种`MessageSource`实现遵循与标准JDK `ResourceBundle`相同的区域设置解析和回退规则。简而言之，继续前面定义的示例`messageSource`，如果要根据British（`en-GB`）语言环境解析消息，则应分别创建名为`format_en_GB.properties`，`exceptions_en_GB.properties`和`windows_en_GB.properties`的文件。

通常，区域设置解析由应用程序的周围环境管理。在以下示例中，手动指定解析（英国）消息的区域设置：

```
# in exceptions_en_GB.properties
argument.required=Ebagum lad, the {0} argument is required, I say, required.
```

```java
public static void main(final String[] args) {
    MessageSource resources = new ClassPathXmlApplicationContext("beans.xml");
    String message = resources.getMessage("argument.required",
        new Object [] {"userDao"}, "Required", Locale.UK);
    System.out.println(message);
}
```

上面程序的输出：

```
Ebagum lad, the 'userDao' argument is required, I say, required.
```

您还可以使用`MessageSourceAware`接口获取对已定义的任何`MessageSource`的引用。在创建和配置bean时，应用程序上下文的`MessageSource`会注入实现`MessageSourceAware`接口的`ApplicationContext`中定义的任何bean。

> 作为`ResourceBundleMessageSource`的替代，Spring提供了一个`ReloadableResourceBundleMessageSource`类。此变体支持相同的包文件格式，但比基于标准JDK的`ResourceBundleMessageSource`实现更灵活。特别是，它允许从任何Spring资源位置（不仅从类路径）读取文件，并支持属性文件的热重新加载（同时有效地缓存它们）。有关详细信息，请参阅`ReloadableResourceBundleMessageSource`文档。

