#### 4.11.9. InfluxDB

[InfluxDB](https://www.influxdata.com/) 是一个开源的时间序列数据库，已针对运行监控，应用程序度量，物联网传感器数据和实时分析等领域中的时间序列数据进行快速，高可用性的存储和检索进行了优化。

##### 连接 InfluxDB

Spring Boot 自动配置一个 `InfluxDB` 实例，前提是 `influxdb-java` 客户端位于类路径上，并且设置了数据库的 URL，如以下示例所示：

```properties
spring.influx.url=https://172.0.0.1:8086
```

如果到 InfluxDB 的连接需要用户名和密码，则可以相应地设置 `spring.influx.user` 和 `spring.influx.password` 属性。

InfluxDB 依赖 OkHttp。如果您需要调整 InfluxDB 在后台使用的 HTTP 客户端，则可以注册 `InfluxDbOkHttpClientBuilderProvider` bean。

