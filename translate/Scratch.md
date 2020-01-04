> 使用 `spring.config.name` 和 `spring.config.location` 可以很早地确定哪些文件必须被加载。必须将它们定义为环境属性（通常是操作系统环境变量，系统属性或命令行参数）。

如果 `spring.config.location` 包含目录（而不是文件），则它们应以 `/` 结尾（在运行时，应在加载之前附加从 `spring.config.name` 生成的名称，包括特定于配置文件的文件名）。在 `spring.config.location` 中指定的文件按原样使用，不支持特定于配置文件的变体，并且被任何特定于配置文件的属性覆盖。

配置位置以相反的顺序搜索。 默认情况下，配置的位置是 `classpath:/,classpath:/config/,file:./,file:./config/`。实际的搜索顺序如下：

1. `file:./config/`
2. `file:./`
3. `classpath:/config/`
4. `classpath:/`

当使用 `spring.config.location` 配置自定义配置位置时，它们将替换默认位置。例如，如果将 `spring.config.location` 配置为值 `classpath:/custom-config/,file:./custom-config/`，则搜索顺序如下：

1. `file:./custom-config/`
2. `classpath:custom-config/`

另外，当使用 `spring.config.additional-location` 配置自定义配置位置时，除了默认位置外，还会使用它们。在默认位置之前会搜索其他位置。例如，如果配置了 `classpath:/custom-config/,file:./custom-config/` 的其他位置，则搜索顺序如下：

1. `file:./custom-config/`
2. `classpath:custom-config/`
3. `file:./config/`
4. `file:./`
5. `classpath:/config/`
6. `classpath:/`

通过此搜索顺序，您可以在一个配置文件中指定默认值，然后在另一个配置文件中有选择地覆盖这些值。您可以在默认位置之一的 `application.properties`（或使用 `spring.config.name` 选择的其他任何基本名称）中为应用程序提供默认值。然后，可以在运行时使用自定义位置之一中的其他文件覆盖这些默认值。

> 如果您使用环境变量而不是系统属性，则大多数操作系统都不允许使用句点分隔的键名，但可以使用下划线（例如，用 `SPRING_CONFIG_NAME` 代替 `spring.config.name`）。

> 如果您的应用程序在容器中运行，则可以使用 JNDI 属性（在 `java:comp/env` 中）或 servlet 上下文初始化参数代替环境变量或系统属性，也可以两者同时使用。

