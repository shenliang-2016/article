### 1.11 使用 JSR 330 标准注解

从 Spring 3.0 开始，Spring 提供了对 JSR-330 标准注解（依赖注入）的支持。那些注解像 Spring 注解一样被扫描。为了使用它们，你需要将相关的 jars 放在你的类路径下。

> 如果你使用Maven，则 `javax.inject` 坐标在 Maven 标准中央仓库 (<https://repo1.maven.org/maven2/javax/inject/javax.inject/1/>) 中是可用的。你可以添加下列依赖到你的 `pom.xml` 文件中：
>
> ```xml
> <dependency>
>     <groupId>javax.inject</groupId>
>     <artifactId>javax.inject</artifactId>
>     <version>1</version>
> </dependency>
> ```

#### 1.11.1 使用`@Inject`和`@Named`进行依赖注入

代替 `@Autowired`，你可以如下使用 `@javax.inject.Inject` ：

```java
import javax.inject.Inject;

public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    public void listMovies() {
        this.movieFinder.findMovies(...);
        ...
    }
}
```

与`@Autowired`一样，您可以在字段级别，方法级别和构造函数 - 参数级别使用`@Inject`。此外，您可以将注入点声明为 `Provider`，允许按需访问较短作用域范围的bean或通过 `Provider.get()` 调用对其他bean的延迟访问。以下示例提供了上述示例的变体：

```java
import javax.inject.Inject;
import javax.inject.Provider;

public class SimpleMovieLister {

    private Provider<MovieFinder> movieFinder;

    @Inject
    public void setMovieFinder(Provider<MovieFinder> movieFinder) {
        this.movieFinder = movieFinder;
    }

    public void listMovies() {
        this.movieFinder.get().findMovies(...);
        ...
    }
}
```

如果要为应注入的依赖项使用限定名称，则应使用`@Named`注解，如以下示例所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(@Named("main") MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

与`@Autowired`一样，`@Inject`也可以与`java.util.Optional`或`@Nullable`一起使用。这在这里更适用，因为`@Inject`没有必需的属性。以下一对示例显示了如何使用`@Inject`和`@Nullable`：

```java
public class SimpleMovieLister {

    @Inject
    public void setMovieFinder(Optional<MovieFinder> movieFinder) {
        ...
    }
}
public class SimpleMovieLister {

    @Inject
    public void setMovieFinder(@Nullable MovieFinder movieFinder) {
        ...
    }
}
```

#### 1.11.2 `@Named`和`@ManagedBean`：`@Component`注解的标准等价物

代替 `@Component`，你可以使用 `@javax.inject.Named` 或者 `javax.annotation.ManagedBean`，如下面例子所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

@Named("movieListener")  // @ManagedBean("movieListener") could be used as well
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

在不指定组件名称的情况下使用`@Component`是很常见的。`@Named`可以以类似的方式使用，如下例所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

@Named
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

使用`@Named`或`@ManagedBean`时，可以使用与使用Spring注解时完全相同的方式使用组件扫描，如以下示例所示：

```java
@Configuration
@ComponentScan(basePackages = "org.example")
public class AppConfig  {
    ...
}
```

> 与`@Component`相比，JSR-330 `@Named`和JSR-250 `@ManagedBean`注解不可组合。您应该使用Spring的构造型模型来构建自定义组件注解。

#### 1.11.3 JSR-330 标准注解的局限性

当你使用标准注解时，你应该了解其一些重要的不可用的特性，如下表所述：

| Spring              | javax.inject.*        | javax.inject restrictions / comments     |
| ------------------- | --------------------- | ---------------------------------------- |
| @Autowired          | @Inject               | `@Inject` 没有 'required' 属性。可以以 Java 8 中的 `Optional`替代。 |
| @Component          | @Named / @ManagedBean | JSR-330不提供可组合模型，只是一种识别命名组件的方法。           |
| @Scope("singleton") | @Singleton            | JSR-330的默认作用域范围就像Spring的原型。但是，为了使其与Spring的一般默认值保持一致，默认情况下，Spring容器中声明的JSR-330 bean是一个单例。为了使用除单例之外的作用域范围，您应该使用Spring的`@Scope`注解。`javax.inject`也提供了`@Scope`注解。然而，这个仅用于创建你自己的注解。 |
| @Qualifier          | @Qualifier / @Named   | `javax.inject.Qualifier`只是构建自定义限定符的元注解。具体`String`限定符（如Spring的带有值的`@Qualifier`）可以通过`javax.inject.Named`关联。 |
| @Value              | -                     | 没有等价物                                    |
| @Required           | -                     | 没有等价物                                    |
| @Lazy               | -                     | 没有等价物                                    |
| ObjectFactory       | Provider              | `javax.inject.Provider`是Spring的`ObjectFactory`的直接替代品，只有更短的`get()`方法名称。它也可以与Spring的`@Autowired`或者没有注解修饰的构造函数和setter方法结合使用。 |

