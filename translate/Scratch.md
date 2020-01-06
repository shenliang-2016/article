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

| Property                            | Note                                                      |
| :---------------------------------- | :-------------------------------------------------------- |
| `acme.my-project.person.first-name` | 短横线隔开式，推荐使用在 `.properties` 和 `.yml` 文件中。 |
| `acme.myProject.person.firstName`   | 标准驼峰形式。                                            |
| `acme.my_project.person.first_name` | 下划线表示法，可以用于 `.properties` 和 `.yml` 文件中。   |
| `ACME_MYPROJECT_PERSON_FIRSTNAME`   | 大写形式，当使用系统环境变量时推荐使用这种形式。          |

> 记号中的 `prefix`值必须是短横线隔开形式(由短横线 `-` 隔开的小写字母，如 `acme.my-project.person`) 。

| Property Source | Simple                                                   | List                                                         |
| :-------------- | :------------------------------------------------------- | :----------------------------------------------------------- |
| Properties 文件 | 驼峰形式，短横线隔开形式或者下划线记法                   | 使用 `[]` 的标准列表语法或者逗号分隔的值列表                 |
| YAML 文件       | 驼峰形式，短横线隔开形式或者下划线记法                   | 标准 YAML 列表语法或者逗号分隔的值列表                       |
| 环境变量        | 以下划线作为定界符的大写格式。不得在属性名称中使用 `_`。 | 由下划线包围的数值，比如 `MY_ACME_1_OTHER = my.acme[1].other` |
| 系统属性        | 驼峰形式，短横线隔开形式或者下划线记法                   | 使用 `[]` 的标准列表语法或者逗号分隔的值列表                 |

> 我们建议，如果可能的话，属性以小写的短横线分隔格式存储，例如 `my.property-name = acme`。

绑定到 `Map` 属性时，如果 `key` 包含小写字母数字字符或 `-` 以外的任何内容，则需要使用方括号表示法，以便保留原始值。如果键没有被 `[]` 包围，则所有非字母数字或 `-` 的字符都将被删除。例如，考虑将以下属性绑定到 `Map`：

```yaml
acme:
  map:
    "[/key1]": value1
    "[/key2]": value2
    /key3: value3
```

上面的属性将会被绑定到 `Map` ，其中包含 `/key1`, `/key2` 和 `key3` 。

> 对于 YAML 文件，方括号需要用引号包围起来，以便正确解析 keys。

