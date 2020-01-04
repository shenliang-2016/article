#### 4.2.1. 配置随机值

`RandomValuePropertySource` 可用于注入随机值（例如，注入密码或测试用例）。它可以产生整数，longs，uuid 或字符串，如以下示例所示：

```properties
my.secret=${random.value}
my.number=${random.int}
my.bignumber=${random.long}
my.uuid=${random.uuid}
my.number.less.than.ten=${random.int(10)}
my.number.in.range=${random.int[1024,65536]}
```

`random.int*` 语法是 `OPEN value (,max) CLOSE` ，其中 `OPEN,CLOSE` 是任何字符，而 `value,max` 是整数。如果提供了 `max`，则 `value` 为最小值，而 `max` 为最大值（不包括）。

#### 4.2.2. 访问命令行属性

默认情况下，`SpringApplication` 会将任何命令行选项参数（即以 `--` 开头的参数，例如 `--server.port=9000`）转换为 `property` 并将其添加到 Spring `Environment` 中。如前所述，命令行属性始终优先于其他属性源。

如果您不希望将命令行属性添加到 `Environment` 中，则可以使用 `SpringApplication.setAddCommandLineProperties(false)` 禁用它们。