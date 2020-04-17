#### 5.6.3. 支持的 Metrics

在适用情况下，Spring Boot 将注册以下核心度量指标：

- JVM metrics，报告下列利用率：
  - 各种内存和缓存池
  - 有关垃圾收集的统计数据
  - 线程利用率
  - 加载/卸载的类的数量
- CPU metrics
- 文件描述符 metrics
- Kafka consumer metrics
- Log4j2 metrics: 记录每个级别记录到 Log4j2 的事件数
- Logback metrics: 记录每个级别记录到 Logback 的事件数
- Uptime metrics: 报告正常运行时间的量度和代表应用程序绝对启动时间的固定量度
- Tomcat metrics (`server.tomcat.mbeanregistry.enabled` 必需设定为 `true` 对所有将被注册的 Tomcat metrics)
- [Spring Integration](https://docs.spring.io/spring-integration/docs/5.2.2.RELEASE/reference/html/system-management.html#micrometer-integration) metrics

