#### 3.4.4 `ConversionService` API

`ConversionService`定义了一个通用接口用于在运行时执行类型转化逻辑。转换器通常运行在下面这种门面接口背后。

````java
package org.springframework.core.convert;

public interface ConversionService {
  boolean canConvert(Class<?> sourceType, Class<?> targetType);
  
  <T> T convert(Object source, Class<T> targetType);
  
  boolean canConvert(TypeDescriptor sourceType, TypeDescriptor targetType);

  Object convert(Object source, TypeDescriptor sourceType, TypeDescriptor targetType);
}
````

大部分`ConversionService`实现同样实现了`ConverterRegistry`，该接口提供了注册转换器的 SPI。站在内部来说，`ConversionService`实现代理了它注册的转换器来执行类型转换逻辑。

在`core.convert.support`包中有一个健壮的`ConversionService`实现。`GenericConversionService`是通用实现，适用于大部分场景。`ConversionServiceFactory`提供了一个方便的工厂来创建普通的`ConversionService`配置。

#### 3.4.5 配置`ConversionService`

`ConversionService`是一个无状态的对下个，它被设计为在应用启动时实例化，然后在多个进程之间共享。在一个 Spring 应用中，你通常应该为每个 Spring 容器（或者`ApplicationContext`）配置一个`ConversionService`实例。Spring 获取该`ConversionService`实例并在任何需要框架执行类型转换的地方使用。你也可以将该实例注入你的 beans 并直接调用它。

> 如果没有为 Spring 配置`ConversionService`，则使用原始的基于`PropertyEditor`的系统。

为 Spring 注册默认的`ConversionService`，添加下面的 bean 定义：

````xml
<bean id="conversionService"
    class="org.springframework.context.support.ConversionServiceFactoryBean"/>
````

默认的`ConversionService`可以在字符串、数字、枚举、集合、映射以及其它普通类型之间执行转换。为了用你自己的自定义转化器替换或者覆盖默认的转化器，设置`converters`属性。该属性值实现任意`Converter`，`ConverterFactory`或者`GenericConverter`接口。

````xml
<bean id="conversionService"
        class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <set>
            <bean class="example.MyCustomConverter"/>
        </set>
    </property>
</bean>
````

在 Spring MVC 应用中也广泛应用了`ConversionService`。参考 Spring MVC 章节中的 [Conversion and Formatting](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 。

某些情况下，你可能希望在类型转换过程中进行格式化。参考 [The `FormatterRegistry` SPI](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#format-FormatterRegistry-SPI) 中有关`FormattingConversionServiceFactoryBean`的使用细节。

