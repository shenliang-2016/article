## 3.10 初始化 `DataSource`

`org.springframework.jdbc.datasource.init` 包提供了初始化现有 `DataSource` 的支持。内置数据库支持提供了为应用创建并初始化 `DataSource` 的选项。不过，有时候你需要初始化一个运行在某个服务器上的实例。

### 3.10.1 使用 Spring XML 初始化数据库

如果你希望初始化一个数据库，同时你可以提供一个 `DataSource` bean 的引用，你可以使用 `spring-jdbc` 命名空间中的 `initialize-database` 标签：

```xml
<jdbc:initialize-database data-source="dataSource">
    <jdbc:script location="classpath:com/foo/sql/db-schema.sql"/>
    <jdbc:script location="classpath:com/foo/sql/db-test-data.sql"/>
</jdbc:initialize-database>
```

上面的例子针对数据库执行了两条特定的脚本。第一条脚本创建一个概要，第二条脚本使用测试数据集填充表。脚本的位置也可以通过常用的 Ant 风格的通配符进行模式化，该风格广泛应用于 Spring 中的资源文件 (比如，`classpath*:/com/foo/**/sql/*-data.sql`)。如果你使用模式，则脚本的执行顺序就是它们的 URL 或者文件名的文本顺序。

数据库初始化器的默认行为就是无条件地执行给定的脚本。有时候这并不一定是你期望的－比如，如果你在已经存在测试数据的数据库中执行脚本。通过下面常用的先创建表然后插入数据的模式可以降低意外删除数据的风险。因为如果表已经存在，则第一步创建表就会失败。

不过，为了获得对创建和删除现有数据的更多控制，XML 命名空间提供了一些附加选项。第一个选项是一个标记来打开或者关闭初始化。你可以根据环境设定该标记（比如从系统属性或者环境 bean 拉取布尔值）。下面的例子从系统属性获取一个值：

```xml
<jdbc:initialize-database data-source="dataSource"
    enabled="#{systemProperties.INITIALIZE_DATABASE}"> 
    <jdbc:script location="..."/>
</jdbc:initialize-database>
```

第二个用于控制对现有数据的处理的选项对失败更加宽容。为此，你可以控制初始化器的能力来忽略它在执行来自脚本的 SQL 时发生的某些错误。如下面例子所示：

```xml
<jdbc:initialize-database data-source="dataSource" ignore-failures="DROPS">
    <jdbc:script location="..."/>
</jdbc:initialize-database>
```

在前面的示例中，我们说我们期望有时脚本是针对空数据库运行的，并且脚本中有一些 `DROP` 语句可能会失败。因此失败的 SQL `DROP` 语句将被忽略，但其他失败将导致异常。如果您的 SQL 方言不支持 `DROP…IF EXISTS` （或类似的东西），但是您想无条件地删除所有测试数据，然后重新创建，则此功能非常有用。在那种情况下，第一个脚本通常是一组 `DROP` 语句，然后是一组 `CREATE` 语句。

`ignore-failures` 选项可以被设置为 `NONE` (默认值)，`DROPS` (忽略失败的 drops)，或者 `ALL` (忽略所有失败)。

每条语句应该由 `;` 分隔，如果脚本中不存在 `;` 字符，则语句以换行分隔。你可以通过脚本控制全局或者脚本。如下面例子所示：

```xml
<jdbc:initialize-database data-source="dataSource" separator="@@"> 
    <jdbc:script location="classpath:com/myapp/sql/db-schema.sql" separator=";"/> 
    <jdbc:script location="classpath:com/myapp/sql/db-test-data-1.sql"/>
    <jdbc:script location="classpath:com/myapp/sql/db-test-data-2.sql"/>
</jdbc:initialize-database>
```

这个例子中，两个 `test-data` 脚本使用 `@@` 作为语句分隔符，只有 `db-schema.sql` 使用 `;`。该配置指定默认的分隔符是 `@@` ，同时为 `db-schema` 脚本覆盖了默认设置。

如果来自 XML 命名空间的控制权不能满足你的需求，你可以直接使用 `DataSourceInitializer` 并将其定义为你的应用的组件。

##### 依赖数据库的其它组件的初始化

大量的应用程序（那些在 Spring 上下文启动之后才使用数据库的应用程序）可以使用数据库初始化程序，而不会带来更多麻烦。如果您的应用程序不是其中之一，则可能需要阅读本节的其余部分。

数据库初始化程序依赖于一个 `DataSource` 实例并运行其初始化回调中提供的脚本（类似于 XML bean 定义中的 `init-method`，或者实现 `InitializingBean` 的组件中的 `@PostConstruct` 方法或 `afterPropertiesSet()` 方法。） 如果其他 Bean 依赖于同一数据源并在初始化回调中使用该数据源，则可能存在问题，因为尚未初始化数据。 一个常见的例子是一个高速缓存，它会在应用程序启动时尽可能早地初始化并从数据库加载数据。

为了解决这个问题，你有两种可选方案：改变你的缓存初始化策略到稍后的阶段，或者确保你的数据库初始化程序首先初始化。

如果应用在你的控制之下，改变缓存初始化策略可能比较容易。下面是一些建议：

- 将缓存初始化推迟到第一次使用时，同时也能改善应用启动时间。
- 使缓存或初始化缓存的单独组件实现 `Lifecycle` 或 `SmartLifecycle`。当应用程序上下文启动时，您可以通过设置其 `autoStartup` 标志来自动启动 `SmartLifecycle`，并且可以通过在封闭 (enclosing) 上下文中调用 `ConfigurableApplicationContext.start()` 来手动启动 `Lifecycle`。
- 使用 Spring `ApplicationEvent` 或类似的自定义观察者机制来触发缓存初始化。`ContextRefreshedEvent` 在其准备好使用时（在所有 bean 都初始化之后）总是由上下文发布，因此通常是一个有用的钩子（默认情况下，这就是 `SmartLifecycle` 的工作方式）。

确保首先初始化数据库初始化程序也很容易。关于如何实现这一点的一些建议包括：

- 依靠 Spring `BeanFactory` 的默认行为，即按注册顺序初始化 bean。您可以通过采用 XML 配置中一组对您的应用程序模块进行排序的 `<import/>` 元素的常规做法，并确保首先列出数据库和数据库初始化，来轻松地进行排序。
- 将 `DataSource` 和使用它的业务组件分开，并通过将它们放在单独的 `ApplicationContext` 实例中来控制启动顺序（例如，父上下文包含 `DataSource` ，子上下文包含业务组件）。这种结构在 Spring Web 应用程序中很常见，但可以更普遍地应用。

