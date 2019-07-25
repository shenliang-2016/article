#### 3.4.6 编程方式使用`ConversionService`

为了以编程方式使用`ConversionService`实例，你可以将其引用注入任何其它 bean 中。下面的例子展示了如何做。

````java
@Service
public class MyService {
  
  @Autowired
  public MyService(ConversionService conversionService) {
    this.conversionService = conversionService;
  }
  
  public void doIt() {
    this.conversionService.convert(...);
  }
}
````

大多数情况下，你可以使用指定`targetType`的`convert`方法，但是它不适用于更复杂的类型，比如参数化元素的集合。比如，如果你想要以编程方式将一个`Integer`的`List`转换为`String`的`List`，你需要提供源类型和目标类型的正式定义。

幸运的是，`TypeDescriptor`提供各种选项来保证无论如何都可以这样做。如下面例子所示：

````java
DefaultConversionService cs = new DefaultConversionService();

List<Integer> input = ....
cs.convert(input,
          TypeDescriptor.forObject(input), // List<Integer> type descriptor)
          TypeDescriptor.collection(List.class, TypeDescriptor.valueOf(String.class)));
````

注意，`DefaultConversionService`自动注册转换器，这些转换器适用于大部分环境。包含集合转换器、纯量（scalar）转换器，以及基本的`Object`到`String`的转换器。你可以使用`DefaultConversionService`类上的`addDefaultConverters`静态方法来注册相同的转换器以及任何`ConverterRegistry`。

值类型转换器被数组和集合复用，因此没有必要为从`S`的`Collection`向`T`的`Collection`的转换创建特定的转换器，假定标准集合处理是合适的。

### 3.5 Spring 字段格式化

如上一章节中所述， [`core.convert`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#core-convert) 是一个通用类型转换系统。它提供了一个通用的`ConversionService` API 以及一个强类型的`Converter` SPI 来实现类型转换逻辑。Spring 容器使用这个系统来绑定 bean 属性值。另外，Spring 表达式语言（SpEL）和`DataBinder`都使用该系统绑定字段值。比如，当 SpEL 需要将`Short`强制转换为`Long`以完成`expression.setValue(Object bean, Object value)`尝试，`core.convert`系统将执行此强制转换。

考虑典型的客户端环境下，比如 web 或者桌面应用，的类型转换需求。在这种环境下，你通常会从`String`转换以支持客户端回传过程，同时转换为`String`以支持视图渲染过程。另外，你通常会需要本地化`String` 值。通用的`core.convert` `Converter` SPI 不直接支持这种格式化需求。为了直接支持它们，Spring 3 引入了一个方便的`Formatter`提供一个简单而健壮的客户端环境下的`PropertyEditor`实现替代品。

通常，你可以使用`Converter` SPI 当你需要实现通用类型转换逻辑 - 比如，为了转换`java.util.Date`和`Long`。你可以使用该`Formatter` SPI 当你在客户端环境中（比如 web 应用）工作而又需要转换并打印本地化的字段值时。`ConversionService`同时为两个 SPIs 提供了通用类型转换 API 。

### 3.5.1 `Formatter` SPI

`Formatter` SPI 提供实现字段格式化逻辑是简单而强类型的。下面列出了`Formatter`接口定义：

````java
package org.springframework.format

public interface Formatter<T> extends Printer<T>, Parser<T> {

}
````

`Formatter`继承自`Printer`和`Parser`两个构建块（building-block）接口。下面里除了这两个接口的定义：

````java
public interface Printer<T> {
  String print(T fieldValue, Locale locale);
}
````

````java
import java.text.ParseException;

public interface Parser<T> {
  T parse(String clientValue, Locale locale) throws ParseException;
}
````

为了创建你自己的`Formatter`，实现前面说到的`Formatter`接口。参数化的`T`是你希望格式化的对象的类型 - 比如，`java.util.Date`。实现`print()`方法来将`T`的实例打印显示到本地化客户端上。实现`parse()`方法来将从本地化客户端返回的格式化表示转换为`T`实例。你的`Formatter`应该抛出`ParseException`或者`IllegalArgumentException`，如果转换尝试失败。注意确保你的`Formatter`实现是线程安全的。

方便起见，`format`子包提供了若干`Formatter`实现。`number`包提供了`NumberStyleFormatter`，`CurrencyStyleFormatter`，以及`PercentStyleFormatter`来使用`java.text.NumberFormat`格式化`Number`对象。`datetime`包提供了`DateFormatter`来使用`java.text.DateFormat`格式化`java.util.Date`对象。`datetime.joda`包基于 [Joda-Time library](http://joda-time.sourceforge.net/) 提供了完善的日期时间格式化支持。

下面的`DateFormatter`是一个`Formatter`实现的例子：

````java
package org.springframework.format.datetime

public final class DateFormatter implements Formatter<Date> {

    private String pattern;

    public DateFormatter(String pattern) {
        this.pattern = pattern;
    }

    public String print(Date date, Locale locale) {
        if (date == null) {
            return "";
        }
        return getDateFormat(locale).format(date);
    }

    public Date parse(String formatted, Locale locale) throws ParseException {
        if (formatted.length() == 0) {
            return null;
        }
        return getDateFormat(locale).parse(formatted);
    }

    protected DateFormat getDateFormat(Locale locale) {
        DateFormat dateFormat = new SimpleDateFormat(this.pattern, locale);
        dateFormat.setLenient(false);
        return dateFormat;
    }
}
````

Spring 团队欢迎社区驱动的`Formatter`贡献。参考 [GitHub Issues](https://github.com/spring-projects/spring-framework/issues) 来贡献。

