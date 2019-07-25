#### 3.5.2 注解驱动的格式化

字符串格式化能够被通过字段类型或者注解配置。为了绑定注解到`Formatter`，实现`AnnotationFormatterFactory`。下面的例子展示了`AnnotationFormatterFactory`接口：

```java
package org.springframework.format;

public interface AnnotationFormatterFactory<A extends Annotation> {

    Set<Class<?>> getFieldTypes();

    Printer<?> getPrinter(A annotation, Class<?> fieldType);

    Parser<?> getParser(A annotation, Class<?> fieldType);
}
```

为了创建一个实现，参数`A`应该是你希望关联到格式化逻辑的字段`annotationType`，比如`org.springframework.format.annotation.DateTimeFormat`。同时拥有`getFieldTypes()`返回该注解能够修饰的字段的类型。拥有`getPrinter()`返回一个`Printer`对象来打印注解修饰的字段值。拥有`getParser()`返回一个`Parser`为注解修饰的字段转换一个`clientValue`。

下面的例子`AnnotationFormatterFactory`实现绑定`@NumberFormat`注解到一个格式化器上以指定一个数字格式或者模式：

```java
public final class NumberFormatAnnotationFormatterFactory
        implements AnnotationFormatterFactory<NumberFormat> {

    public Set<Class<?>> getFieldTypes() {
        return new HashSet<Class<?>>(asList(new Class<?>[] {
            Short.class, Integer.class, Long.class, Float.class,
            Double.class, BigDecimal.class, BigInteger.class }));
    }

    public Printer<Number> getPrinter(NumberFormat annotation, Class<?> fieldType) {
        return configureFormatterFrom(annotation, fieldType);
    }

    public Parser<Number> getParser(NumberFormat annotation, Class<?> fieldType) {
        return configureFormatterFrom(annotation, fieldType);
    }

    private Formatter<Number> configureFormatterFrom(NumberFormat annotation, Class<?> fieldType) {
        if (!annotation.pattern().isEmpty()) {
            return new NumberStyleFormatter(annotation.pattern());
        } else {
            Style style = annotation.style();
            if (style == Style.PERCENT) {
                return new PercentStyleFormatter();
            } else if (style == Style.CURRENCY) {
                return new CurrencyStyleFormatter();
            } else {
                return new NumberStyleFormatter();
            }
        }
    }
}
```

为了触发格式化，你可以用`@NumberFormat`注解修饰字段，如下面例子所示：

```java
public class MyModel {

    @NumberFormat(style=Style.CURRENCY)
    private BigDecimal decimal;
}
```

##### 格式化注解 API

可移植格式注解 API 存在于`org.springframework.format.annotation`包中。您可以使用`@NumberFormat`来格式化`Number`字段，例如`Double`和`Long`，以及`@DateTimeFormat`来格式化`java.util.Date`，`java.util.Calendar`，`Long`（ 对于毫秒时间戳）以及 JSR-310`java.time`和 Joda-Time 值类型。

以下示例使用`@DateTimeFormat`将`java.util.Date`格式化为 ISO Date（yyyy-MM-dd）：

```java
public class MyModel {

    @DateTimeFormat(iso=ISO.DATE)
    private Date date;
}
```

#### 3.5.3 `FormatterRegistry` SPI

`FormatterRegistry`是用于注册格式化器和转换器的 SPI。`FormattingConversionService`是适用于大多数环境的`FormatterRegistry`的实现。您可以以编程方式或声明性地将此变体配置为Spring bean，例如，通过使用`FormattingConversionServiceFactoryBean`。因为此实现还实现了`ConversionService`，所以您可以直接将其配置为与 Spring 的`DataBinder`和 Spring Expression Language（SpEL）一起使用。

以下清单显示了`FormatterRegistry` SPI：

```java
package org.springframework.format;

public interface FormatterRegistry extends ConverterRegistry {

    void addFormatterForFieldType(Class<?> fieldType, Printer<?> printer, Parser<?> parser);

    void addFormatterForFieldType(Class<?> fieldType, Formatter<?> formatter);

    void addFormatterForFieldType(Formatter<?> formatter);

    void addFormatterForAnnotation(AnnotationFormatterFactory<?, ?> factory);
}
```

如上面的清单所示，您可以按字段类型或注解注册格式化程序。

`FormatterRegistry` SPI 允许您集中配置格式规则，而不是在控制器之间复制此类配置。例如，您可能希望强制所有日期字段以某种方式格式化，或者具有特定注解的字段以某种方式格式化。使用共享的`FormatterRegistry`，您可以定义一次这些规则，并在需要格式化时应用它们。

#### 3.5.4 `FormatterRegistrar` SPI

`FormatterRegistrar`是一个 SPI，用于通过`FormatterRegistry`注册格式化程序和转换器。以下清单显示了其接口定义：

```java
package org.springframework.format;

public interface FormatterRegistrar {

    void registerFormatters(FormatterRegistry registry);
}
```

在为给定格式类别注册多个相关转换器和格式化程序时，`FormatterRegistrar`非常有用，例如日期格式。它在声明性注册不足的情况下也很有用 - 例如，当格式化程序需要在与其自己的`<T>`不同的特定字段类型下编入索引时，或者在注册`Printer` /`Parser`对时。下一节提供有关转换器和格式化程序注册的更多信息。

#### 3.5.5 在 Spring MVC 中配置格式化

参考 Spring MVC 中的 [Conversion and Formatting](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 。