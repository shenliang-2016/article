### 5.5. Loggers

Spring Boot Actuator 包含在运行时查看和配置应用的日志级别的能力。你可以查看整体配置列表或者单个 logger 配置。该配置由显式配置的日志级别以及日志框架赋予的有效的日志级别组成。日志级别可以是：

- `TRACE`
- `DEBUG`
- `INFO`
- `WARN`
- `ERROR`
- `FATAL`
- `OFF`
- `null`

`null` 表示没有显式配置。

#### 5.5.1. 配置 Logger

为了配置给定的 logger，`POST` 一个部分实体到该资源 URI，如下面例子所示：

```json
{
    "configuredLevel": "DEBUG"
}
```

> 要“重置”记录器的特定级别（并使用默认配置），可以将传入 `null` 作为 `configuredLevel` 值。

