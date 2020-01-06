##### Properties 转换

当 Spring Boot 绑定到 `@ConfigurationProperties` bean时，它试图将外部应用程序属性强制转换为正确的类型。如果需要自定义类型转换，则可以提供一个 `ConversionService` bean（带有名为 `conversionService` 的bean）或自定义属性编辑器（通过 `CustomEditorConfigurer` bean）或自定义的 `Converters`（带有定义为 `@ConfigurationPropertiesBinding` 的 bean 定义）。

> 由于在应用程序生命周期中非常早就请求了此 bean，因此请确保限制您的 `ConversionService` 使用的依赖项。通常，您需要的任何依赖项可能在创建时未完全初始化。如果配置键强制不需要自定义的 `ConversionService`，则可能要重命名，而仅依赖于具有 `@ConfigurationPropertiesBinding` 限定的自定义转换器。

###### 转换持续时间

Spring Boot 为表达持续时间提供了专门的支持。如果公开 `java.time.Duration` 属性，则应用程序属性中的以下格式可用：

- 常规的 `long` 表示形式（使用毫秒作为默认单位，除非指定了 `@DurationUnit`）
- 标准的 ISO-8601 格式 [used by `java.time.Duration`](https://docs.oracle.com/javase/8/docs/api//java/time/Duration.html#parse-java.lang.CharSequence-)
- 值和单位相结合的更具可读性的格式（例如，`10s` 表示10秒）

考虑下面的例子：

```java
@ConfigurationProperties("app.system")
public class AppSystemProperties {

    @DurationUnit(ChronoUnit.SECONDS)
    private Duration sessionTimeout = Duration.ofSeconds(30);

    private Duration readTimeout = Duration.ofMillis(1000);

    public Duration getSessionTimeout() {
        return this.sessionTimeout;
    }

    public void setSessionTimeout(Duration sessionTimeout) {
        this.sessionTimeout = sessionTimeout;
    }

    public Duration getReadTimeout() {
        return this.readTimeout;
    }

    public void setReadTimeout(Duration readTimeout) {
        this.readTimeout = readTimeout;
    }

}
```

要指定 30 秒的会话超时，`30`，`PT30S` 和 `30s` 都是等效的。可以用以下任何一种形式指定 500ms 的读取超时：`500`，`PT0.5S` 和 `500ms`。

您也可以使用任何受支持的单位。这些是：

- `ns` 纳秒

- `us` 微秒

- `ms` 毫秒（毫秒）

- `s` 秒

- `m` 分钟

- `h` 小时

- `d` 天

默认单位是毫秒，可以使用 `@DurationUnit` 覆盖，如上面的示例所示。

> 如果您要从仅使用 `Long` 表示持续时间的先前版本进行升级，请确保在转换为 `Duration` 的时间单位不是毫秒的情况下定义单位（使用 `@DurationUnit`）。这样做可以提供透明的升级路径，同时支持更丰富的格式。

###### 转换数据尺寸

Spring Framework 具有一个 `DataSize` 值类型，该值类型以字节为单位表示大小。如果您公开 `DataSize` 属性，则应用程序属性中的以下格式可用：

- 常规的 `long` 表示形式（除非指定了 `@DataSizeUnit`，否则使用字节作为默认单位）

- 将值和单位组合在一起的更具可读性的格式（例如，`10MB` 表示 10 兆字节）

考虑以下示例：

```java
@ConfigurationProperties("app.io")
public class AppIoProperties {

    @DataSizeUnit(DataUnit.MEGABYTES)
    private DataSize bufferSize = DataSize.ofMegabytes(2);

    private DataSize sizeThreshold = DataSize.ofBytes(512);

    public DataSize getBufferSize() {
        return this.bufferSize;
    }

    public void setBufferSize(DataSize bufferSize) {
        this.bufferSize = bufferSize;
    }

    public DataSize getSizeThreshold() {
        return this.sizeThreshold;
    }

    public void setSizeThreshold(DataSize sizeThreshold) {
        this.sizeThreshold = sizeThreshold;
    }

}
```

要指定 10 兆字节的缓冲区大小，`10` 和 `10MB` 是等效的。可以将 256 个字节的大小阈值指定为 `256` 或 `256B`。您也可以使用任何受支持的单位。这些是：

- `B` 表示字节

- `KB` 代表千字节

- `MB` 代表兆字节

- `GB` 代表GB

- `TB`（TB）

默认单位时字节，可以通过使用  `@DataSizeUnit` 覆盖，如上面例子所示。

> 如果您要从仅使用 `Long` 表示大小的先前版本进行升级，请确保在切换至 `DataSize` 而没有使用字节作为单位的情况下定义单位（使用 `@DataSizeUnit`）。这样做可以提供透明的升级路径，同时支持更丰富的格式。

