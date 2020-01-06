##### 第三方配置

除了使用 `@ConfigurationProperties` 注解类之外，您还可以在公共 `@Bean` 方法上使用它。当您要将属性绑定到你控制范围之外的第三方组件时，这样做特别有用。

要通过 `Environment` 属性配置 bean，请在其 bean 注册中添加 `@ConfigurationProperties`，如以下示例所示：

```java
@ConfigurationProperties(prefix = "another")
@Bean
public AnotherComponent anotherComponent() {
    ...
}
```

任何以 `another` 前缀定义的 JavaBean 属性都被映射到该 `AnotherComponent` bean上，类似于前面的 `AcmeProperties` 示例。

##### 宽松绑定

Spring Boot 使用一些宽松的规则来将 `Environment` 属性绑定到 `@ConfigurationProperties` bean，因此 `Environment` 属性名称和 bean 属性名称之间不需要完全匹配。有用的常见示例包括破折号分隔的环境属性（例如，`context-path` 绑定到 `contextPath`）和大写的环境属性（例如，`PORT` 绑定到 `port`）。

作为示例，考虑下面的 `@ConfigurationProperties` 类：

```java
@ConfigurationProperties(prefix="acme.my-project.person")
public class OwnerProperties {

    private String firstName;

    public String getFirstName() {
        return this.firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

}
```

上面的代码可以使用下面的属性名：

| Property                            | Note                                                         |
| :---------------------------------- | :----------------------------------------------------------- |
| `acme.my-project.person.first-name` | Kebab case, which is recommended for use in `.properties` and `.yml` files. |
| `acme.myProject.person.firstName`   | Standard camel case syntax.                                  |
| `acme.my_project.person.first_name` | Underscore notation, which is an alternative format for use in `.properties` and `.yml` files. |
| `ACME_MYPROJECT_PERSON_FIRSTNAME`   | Upper case format, which is recommended when using system environment variables. |

> The `prefix` value for the annotation *must* be in kebab case (lowercase and separated by `-`, such as `acme.my-project.person`).

| Property Source       | Simple                                                       | List                                                         |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Properties Files      | Camel case, kebab case, or underscore notation               | Standard list syntax using `[ ]` or comma-separated values   |
| YAML Files            | Camel case, kebab case, or underscore notation               | Standard YAML list syntax or comma-separated values          |
| Environment Variables | Upper case format with underscore as the delimiter. `_` should not be used within a property name | Numeric values surrounded by underscores, such as `MY_ACME_1_OTHER = my.acme[1].other` |
| System properties     | Camel case, kebab case, or underscore notation               | Standard list syntax using `[ ]` or comma-separated values   |

> We recommend that, when possible, properties are stored in lower-case kebab format, such as `my.property-name=acme`.

When binding to `Map` properties, if the `key` contains anything other than lowercase alpha-numeric characters or `-`, you need to use the bracket notation so that the original value is preserved. If the key is not surrounded by `[]`, any characters that are not alpha-numeric or `-` are removed. For example, consider binding the following properties to a `Map`:

```yaml
acme:
  map:
    "[/key1]": value1
    "[/key2]": value2
    /key3: value3
```

The properties above will bind to a `Map` with `/key1`, `/key2` and `key3` as the keys in the map.

> For YAML files, the brackets need to be surrounded by quotes for the keys to be parsed properly.