#### 8.1.2. 打包可执行 jar 和 war 文件

一旦 `spring-boot-maven-plugin` 被包含在你的 `pom.xml` 中，它将会自动尝试通过使用 `spring-boot:repackage` 目标重新打包压缩包来使得它们可执行。你应该通过使用常规的 `packaging` 元素配置你的项目打包为 jar 或者 war ，如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>jar</packaging>
    <!-- ... -->
</project>
```

Spring 的 `package` 阶段会增强您现有的存档。可以通过使用配置选项来指定要启动的主类，如下所示，也可以通过向清单添加 `Main-Class` 属性来指定。如果您未指定主类，则插件会使用`public static void main(String[] args)` 方法搜索类。

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <mainClass>com.example.app.Main</mainClass>
    </configuration>
</plugin>
```

为了构建并运行项目组件，使用下面的命令：

```
$ mvn package
$ java -jar target/mymodule-0.0.1-SNAPSHOT.jar
```

要构建既可执行又可部署到外部容器的 war 文件，您需要将嵌入式容器的相关性标记为 “provided”，如以下示例所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>war</packaging>
    <!-- ... -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- ... -->
    </dependencies>
</project>
```

> 参考 “[Create a Deployable War File](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-create-a-deployable-war-file)” 部分了解创建可部署 war 文件的更多细节。

高级配置选项和示例可以在 [plugin info page](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/maven-plugin/) 上找到。