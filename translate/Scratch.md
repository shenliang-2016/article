#### 4.28.5. 创建你自己的启动器

一个类库的完整 Spring Boot 启动器可能包含下列组件：

- 包含自动配置代码的 `autoconfigure` 模块。
- `starter` 模块，提供 `autoconfigure` 模块所需的依赖、类库以及任何附加的有用以来。简而言之，添加启动器应该提供开始使用该类库所需的所有条件。

> 如果你不需要分开管理自动配置和依赖管理，你就可以将两者组合为一个模块。

##### 命名

您应确保为启动器提供适当的名称空间。即使使用不同的 Maven`groupId`，也不要以`spring-boot`开头模块名称。将来，我们可能会为您自动配置的内容提供官方支持。

根据经验，应在启动器后命名一个组合模块。例如，假设您要为 `acme` 创建启动器，并命名自动配置模块 `acme-spring-boot-autoconfigure` 和启动器 `acme-spring-boot-starter`。如果只有一个将两者结合的模块，则将其命名为 `acme-spring-boot-starter`。