### 3.4 Spring 类型转化

Spring 3 引入了`core.convert`包来提供通用的类型转化系统。该系统定义一个 SPI 来实现类型转化逻辑，并提供一个在运行时执行类型转化的 API。在 Spring 容器中，你可以使用这个系统作为`PropertyEditor`实现的替代品来将外部 bean 属性值字符串转化为需要的属性类型。你也可以在你的应用程序中任何需要类型转化的地方使用该公开 API 。

#### 3.4.1. 转化器 SPI

实现类型转化逻辑的 SPI 是简洁的，它是强类型的。如下面接口定义所示：

```java
package org.springframework.core.convert.converter;

public interface Converter<S, T> {

    T convert(S source);
}
```

要实现你自己的转化器，实现`Converter`接口，其中的参数`S`是你想要转化的类型，`T`是你想要转化为的类型。如果一个`S`集合或者数组需要转化为`T`集合或者数组，你也可以透明地应用该转化器，前提是已经注册了委托数组或者集合转化器（默认情况下`DefaultConversionService`就是这么做）。

每次`convert(S)`调用，源参数保证不为`null`。如果转化失败，你的`Converter`可以抛出任何未检查的异常。特别地，它应该抛出`IllegalArgumentException`来报告非法的源值。请确保你的`Converter`实现是线程安全的。

方便起见，`core.convert.support`包中提供了一些转化器实现。包括将字符串转化未数字或者其它常用类型的转化器。下面是`StringToInteger`类，一个典型的`Converter`实现：

```java
package org.springframework.core.convert.support;

final class StringToInteger implements Converter<String, Integer> {

    public Integer convert(String source) {
        return Integer.valueOf(source);
    }
}
```

#### 3.4.2. 使用 `ConverterFactory`

当您需要集中整个类层次结构的转换逻辑时（例如，从`String`转换为`Enum`对象时），您可以实现`ConverterFactory`，如以下示例所示：

```java
package org.springframework.core.convert.converter;

public interface ConverterFactory<S, R> {

    <T extends R> Converter<S, T> getConverter(Class<T> targetType);
}
```

参数化`S`为要转换的类型，`R`为定义转化目标类的范围的基本类型。然后实现`getConverter(Class<T>)`，其中`T`是`R`的子类。

以`StringToEnumConverterFactory`为例：

```java
package org.springframework.core.convert.support;

final class StringToEnumConverterFactory implements ConverterFactory<String, Enum> {

    public <T extends Enum> Converter<String, T> getConverter(Class<T> targetType) {
        return new StringToEnumConverter(targetType);
    }

    private final class StringToEnumConverter<T extends Enum> implements Converter<String, T> {

        private Class<T> enumType;

        public StringToEnumConverter(Class<T> enumType) {
            this.enumType = enumType;
        }

        public T convert(String source) {
            return (T) Enum.valueOf(this.enumType, source.trim());
        }
    }
}
```

#### 3.4.3. 使用 `GenericConverter`

当你需要比较复杂的`Converter`实现时，考虑使用`GenericConverter`接口。`GenericConverter`具有比`Converter`更灵活但不太强类型的签名，支持在多种源和目标类型之间进行转换。此外，`GenericConverter`提供了在实现转换逻辑时可以使用的源和目标字段上下文。这样的上下文允许类型转换由字段注解或在字段签名上声明的通用信息驱动。以下清单显示了`GenericConverter`的接口定义：

```java
package org.springframework.core.convert.converter;

public interface GenericConverter {

    public Set<ConvertiblePair> getConvertibleTypes();

    Object convert(Object source, TypeDescriptor sourceType, TypeDescriptor targetType);
}
```

要实现`GenericConverter`，请让 `getConvertibleTypes()` 返回支持的源→目标类型对。然后实现 `convert(Object, TypeDescriptor, TypeDescriptor)` 以包含转换逻辑。源`TypeDescriptor`提供对包含要转换的值的源字段的访问。目标`TypeDescriptor`提供对要设置转换值的目标字段的访问。

`GenericConverter`的一个很好的例子是在Java数组和集合之间进行转换的转换器。这样的`ArrayToCollectionConverter`会内省声明目标集合类型的字段以解析集合的元素类型。这样，在目标字段上设置集合之前，可以将源数组中的每个元素转换为目标集合元素类型。

> 由于`GenericConverter`是更复杂的 SPI 接口，你应该仅仅在确实需要时使用。通常的类型转化请优先使用`Converter`或者`ConverterFactory`。

##### 使用 `ConditionalGenericConverter`

有时，只有在特定条件成立时才希望`Converter`运行。例如，如果目标字段上存在特定注解，才需要运行`Converter`，或者如果在目标类上定义了特定方法（例如静态`valueOf`方法），才运行`Converter`。`ConditionalGenericConverter`是`GenericConverter`和`ConditionalConverter`接口的联合，允许您定义此类自定义匹配条件：

```java
public interface ConditionalConverter {

    boolean matches(TypeDescriptor sourceType, TypeDescriptor targetType);
}

public interface ConditionalGenericConverter extends GenericConverter, ConditionalConverter {
}
```

`ConditionalGenericConverter`的一个很好的例子是`EntityConverter`，它在持久化实体标识符和实体引用之间进行转换。仅当目标实体类型声明静态查找方法（例如，`findAccount(Long)`）时，此类`EntityConverter`才可能匹配。您可以在匹配的实现`matches(TypeDescriptor, TypeDescriptor)`中执行这样的查找方法检查。

