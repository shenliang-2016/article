##### 合并复杂类型

如果在多个位置配置了列表，则通过替换整个列表来进行覆盖。

例如，假设一个 `MyPojo` 对象的 `name` 属性和 `description` 属性默认为 `null`。以下示例从 `AcmeProperties` 中公开了 `MyPojo` 对象的列表：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final List<MyPojo> list = new ArrayList<>();

    public List<MyPojo> getList() {
        return this.list;
    }

}
```

考虑下面的配置：

```yaml
acme:
  list:
    - name: my name
      description: my description
---
spring:
  profiles: dev
acme:
  list:
    - name: my another name
```

如果 `dev` 环境配置文件未激活，则 `AcmeProperties.list` 包含一个 `MyPojo` 条目，如先前定义。但是，如果启用了 `dev` 环境配置文件，则 `list`  仍然仅包含一个条目（名称为 `my another name` ，描述为 `null` ）。此配置*不会*将第二个 `MyPojo` 实例添加到列表中，并且不会合并项目。

当在多个配置文件中指定一个 `List` 时，将使用优先级最高的列表（并且只使用那个）。考虑以下示例：

```yaml
acme:
  list:
    - name: my name
      description: my description
    - name: another name
      description: another description
---
spring:
  profiles: dev
acme:
  list:
    - name: my another name
```

在前面的示例中，如果 `dev` 环境配置文件处于活动状态，则 `AcmeProperties.list` 包含*一个* `MyPojo` 条目（名称为 `my another name`，描述为 `null`）。对于 YAML，可以使用逗号分隔的列表和 YAML 列表来完全覆盖列表的内容。

对于 `Map` 属性，您可以绑定从多个来源的属性值。但是，对于多个源中的同一属性，将使用优先级最高的属性值。以下示例从 `AcmeProperties` 中公开了 `Map<String, MyPojo>`：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final Map<String, MyPojo> map = new HashMap<>();

    public Map<String, MyPojo> getMap() {
        return this.map;
    }

}
```

考虑下面的配置：

```yaml
acme:
  map:
    key1:
      name: my name 1
      description: my description 1
---
spring:
  profiles: dev
acme:
  map:
    key1:
      name: dev name 1
    key2:
      name: dev name 2
      description: dev description 2
```

如果 `dev` 环境配置文件未激活，则 `AcmeProperties.map` 包含一个键为 `key1` 的条目（名称为 `my name 1` ，描述为 `my description 1`）。但是，如果启用了 `dev` 配置文件，则 `map` 包含两个条目，其中包含键 `key1`（名称为 `dev name 1`，名称为 `my description 1`）和 `key2`（名称为 `dev name 2`，名称为 `my description 2`）。

> 前述合并规则不仅适用于 YAML 文件，而且适用于所有属性源中的属性。

