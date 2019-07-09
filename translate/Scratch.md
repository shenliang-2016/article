#### 1.10.4 使用过滤器定制组件扫描

默认情况下，被注解`@Component`，`@Repository`，`@Service`，`@Controller` 或者你自定义的注解（本身被`@Component`修饰）修饰的类就是自动扫描探测的候选组件。不过，你可以修改和扩展这种行为，通过应用自定义过滤器。将它们添加为`@ComponentScan`注解的`include-filters`或者`excludeFilters`参数（或者作为`component-scan`元素的`include-filter`或者`exclude-filter`子元素）。每个过滤器元素都需要`type`和`expression`属性。下表描述了过滤器选项：

| Filter Type          | Example Expression           | Description                              |
| -------------------- | ---------------------------- | ---------------------------------------- |
| annotation (default) | `org.example.SomeAnnotation` | 要在目标组件中的类型级别出现的注解。                       |
| assignable           | `org.example.SomeClass`      | 目标组件可分配给（扩展或实现）的类（或接口）。                  |
| aspectj              | `org.example..*Service+`     | 要由目标组件匹配的AspectJ类型表达式。                   |
| regex                | `org\.example\.Default.*`    | 要由目标组件类名匹配的正则表达式。                        |
| custom               | `org.example.MyTypeFilter`   | `org.springframework.core.type.TypeFilter`接口的自定义实现。 |

以下示例显示忽略所有`@Repository`注释并使用“存根”存储库的配置：

```java
@Configuration
@ComponentScan(basePackages = "org.example",
        includeFilters = @Filter(type = FilterType.REGEX, pattern = ".*Stub.*Repository"),
        excludeFilters = @Filter(Repository.class))
public class AppConfig {
    ...
}
```

以下清单显示了等效的XML：

```java
<beans>
    <context:component-scan base-package="org.example">
        <context:include-filter type="regex"
                expression=".*Stub.*Repository"/>
        <context:exclude-filter type="annotation"
                expression="org.springframework.stereotype.Repository"/>
    </context:component-scan>
</beans>
```

> 您还可以通过在注解上设置`useDefaultFilters=false`或通过提供`use-default-filters=“false”`作为`<component-scan />`元素的属性来禁用默认过滤器。实际上，这会禁用自动检测使用`@Component`，`@Repository`，`@Service`，`@Controller`或`@Configuration`注解修饰的类。

#### 1.10.5 在组件中定义 Bean 元数据

Spring组件还可以向容器提供bean定义元数据。您可以在`@Configuration`注解修饰的类中使用用于定义bean元数据的相同`@Bean`注解来执行此操作。以下示例显示了如何执行此操作：

```java
@Component
public class FactoryMethodComponent {

    @Bean
    @Qualifier("public")
    public TestBean publicInstance() {
        return new TestBean("publicInstance");
    }

    public void doWork() {
        // Component method implementation omitted
    }
}
```

上面的类是一个Spring组件，在其 `doWork()` 方法中具有特定于应用程序的代码。但是，它还提供了一个bean定义，它具有引用 `publicInstance()`方法的工厂方法。`@Bean`注解标识工厂方法和其他bean定义属性，例如通过`@Qualifier`注解指定的限定符值。可以指定的其他方法级注解是`@Scope`，`@Lazy`和自定义限定符注解。

> 除了它的组件初始化角色之外，您还可以将`@Lazy`注解放在标有`@Autowired`或`@Inject`的注入点上。在这种情况下，它会导致惰性解析代理注入。

如前所述，支持自动装配的字段和方法，以及对`@Bean`方法的自动装配的额外支持。以下示例显示了如何执行此操作：

```java
@Component
public class FactoryMethodComponent {

    private static int i;

    @Bean
    @Qualifier("public")
    public TestBean publicInstance() {
        return new TestBean("publicInstance");
    }

    // use of a custom qualifier and autowiring of method parameters
    @Bean
    protected TestBean protectedInstance(
            @Qualifier("public") TestBean spouse,
            @Value("#{privateInstance.age}") String country) {
        TestBean tb = new TestBean("protectedInstance", 1);
        tb.setSpouse(spouse);
        tb.setCountry(country);
        return tb;
    }

    @Bean
    private TestBean privateInstance() {
        return new TestBean("privateInstance", i++);
    }

    @Bean
    @RequestScope
    public TestBean requestScopedInstance() {
        return new TestBean("requestScopedInstance", 3);
    }
}
```

该示例将`String`方法参数`country`自动装配到另一个名为`privateInstance`的bean上的`age`属性值。Spring Expression Language元素通过符号`#{<expression>}`定义属性的值。对于`@Value`注释，表达式解析器预先配置为在解析表达式文本时查找bean名称。

从Spring Framework 4.3开始，您还可以声明一个类型为`InjectionPoint`的工厂方法参数（或其更具体的子类：`DependencyDescriptor`）来访问触发创建当前bean的请求注入点。请注意，这仅适用于创建bean实例，而不适用于注入现有实例。因此，此功能对原型作用域的bean最有意义。对于其他作用域，工厂方法只能看到触发在给定作用域中创建新bean实例的注入点（例如，触发创建惰性单例bean的依赖项）。在这种情况下，您可以使用提供的注入点元数据和相关语义。以下示例显示了如何使用`InjectionPoint`：

```java
@Component
public class FactoryMethodComponent {

    @Bean @Scope("prototype")
    public TestBean prototypeInstance(InjectionPoint injectionPoint) {
        return new TestBean("prototypeInstance for " + injectionPoint.getMember());
    }
}
```

常规Spring组件中的`@Bean`方法的处理方式与Spring `@Configuration`类中的处理方式不同。不同之处在于，使用CGLIB不会增强`@Component`类来拦截方法和字段的调用。CGLIB代理是调用`@Configuration`类中的`@Bean`方法中的方法或字段创建对协作对象的bean元数据引用的方法。这些方法不是用普通的Java语义调用的，而是通过容器来提供通常的生命周期管理和Spring bean的代理，即使在通过对`@Bean`方法的编程调用引用其他bean时也是如此。相反，在普通的`@Component`类中调用`@Bean`方法中的方法或字段具有标准的Java语义，没有应用特殊的CGLIB处理或其他约束。

> 您可以将`@Bean`方法声明为`static`，允许在不创建包含配置类实例的情况下调用它们。这在定义后处理器bean（例如，`BeanFactoryPostProcessor`或`BeanPostProcessor`类型）时特别有意义，因为这样的bean在容器生命周期的早期就会初始化，并且应该避免在那时触发配置的其他部分。
>
> 由于技术限制，对静态`@Bean`方法的调用永远不会被容器拦截，甚至在`@Configuration`类中也没有（如本节前面所述）：CGLIB子类化只能覆盖非静态方法。因此，直接调用另一个`@Bean`方法具有标准的Java语义，从而导致直接从工厂方法本身返回一个独立的实例。
>
> `@Bean`方法的Java语言可见性对Spring容器中生成的bean定义没有立即影响。您可以根据需要在非`@Configuration`类中自由声明工厂方法，也可以在任何地方自由声明静态方法。但是，`@Conffiguration`类中的常规`@Bean`方法需要可以覆盖 - 也就是说，它们不能声明为`private`或`final`。
>
> `@Bean`方法也可以在给定组件或配置类的基类上出现，也可以在组件或配置类实现的接口中声明的Java 8默认方法上出现。这使得在编写复杂的配置时具有很大的灵活性，从Spring 4.2开始，甚至可以通过Java 8默认方法实现多重继承。
>
> 最后，单个类可以为同一个bean保存多个`@Bean`方法，作为根据运行时可用依赖项使用的多个工厂方法的安排。这与在其他配置方案中选择“最贪婪”构造函数或工厂方法的算法相同：在构造时选择具有最多可满足依赖项的变体，类似于容器在多个`@Autowired`构造函数之间进行选择的方式。

