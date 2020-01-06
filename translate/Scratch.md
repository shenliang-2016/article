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

###### Converting Data Sizes

Spring Framework has a `DataSize` value type that expresses a size in bytes. If you expose a `DataSize` property, the following formats in application properties are available:

- A regular `long` representation (using bytes as the default unit unless a `@DataSizeUnit` has been specified)
- A more readable format where the value and the unit are coupled (e.g. `10MB` means 10 megabytes)

Consider the following example:

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

To specify a buffer size of 10 megabytes, `10` and `10MB` are equivalent. A size threshold of 256 bytes can be specified as `256` or `256B`.

You can also use any of the supported units. These are:

- `B` for bytes
- `KB` for kilobytes
- `MB` for megabytes
- `GB` for gigabytes
- `TB` for terabytes

The default unit is bytes and can be overridden using `@DataSizeUnit` as illustrated in the sample above.

> If you are upgrading from a previous version that is simply using `Long` to express the size, make sure to define the unit (using `@DataSizeUnit`) if it isn’t bytes alongsidethe switch to `DataSize`. Doing so gives a transparent upgrade path while supporting a much richer format.