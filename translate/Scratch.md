### 8.2. Spring Boot Gradle 插件

Spring Boot Gradle 插件在 Gradle 中提供了 Spring Boot 支持，可让您打包可执行 jar 或 war 归档文件，运行 Spring Boot 应用程序以及使用 `spring-boot-dependencies` 提供的依赖管理。它需要 Gradle 5.x（也支持4.10，但该支持在将来的版本中将删除）。请参阅插件的文档以了解更多信息：

- 参考文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html/) 和 [PDF](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/pdf/spring-boot-gradle-plugin-reference.pdf))
- [API](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/api/)

### 8.3. Spring Boot AntLib 模块

Spring Boot AntLib 模块为 Apache Ant 提供了基本的 Spring Boot 支持。您可以使用该模块创建可执行 jar。要使用该模块，您需要在 `build.xml` 中声明一个附加的 `spring-boot` 名称空间，如以下示例所示：

```xml
<project xmlns:ivy="antlib:org.apache.ivy.ant"
    xmlns:spring-boot="antlib:org.springframework.boot.ant"
    name="myapp" default="build">
    ...
</project>
```

你需要记住使用 `-lib` 选项启动 Ant ，如下面例子所示：

```
$ ant -lib <folder containing spring-boot-antlib-2.2.2.RELEASE.jar>
```

> “使用Spring Boot” 部分包含 [将 Apache Ant 与 `spring-boot-antlib` 一起使用](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-ant) 的更完整示例。

#### 8.3.1. Spring Boot Ant 任务

一旦 `spring-boot-antlib` 命名空间被声明，下面的附加任务将可用：

- [`spring-boot:exejar`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-ant-exejar)
- [`spring-boot:findmainclass`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-ant-findmainclass)

##### `spring-boot:exejar`

你可以使用 `exejar` 任务创建 Spring Boot 可执行 jar。该任务支持下列属性：

| Attribute     | Description             | Required                                |
| :------------ | :---------------------- | :-------------------------------------- |
| `destfile`    | 需要创建的目标 jar 文件 | Yes                                     |
| `classes`     | Java 类文件的根目录     | Yes                                     |
| `start-class` | 需要运行的应用主类      | No *(默认是找到的第一个声明主方法的类)* |

下面的嵌套元素可以用于该任务：

| Element     | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `resources` | 一个或者多个 [Resource Collections](https://ant.apache.org/manual/Types/resources.html#collection) 描述一系列 [Resources](https://ant.apache.org/manual/Types/resources.html) 应该被添加到要创建的 jar 文件内容中。 |
| `lib`       | 一个或者多个 [Resource Collections](https://ant.apache.org/manual/Types/resources.html#collection) 应该被添加到组成应用的运行时依赖类路径的 jar 类库集合中。 |

##### 示例

本节展示两个 Ant 任务的示例。

指定启动类

```xml
<spring-boot:exejar destfile="target/my-application.jar"
        classes="target/classes" start-class="com.example.MyApplication">
    <resources>
        <fileset dir="src/main/resources" />
    </resources>
    <lib>
        <fileset dir="lib" />
    </lib>
</spring-boot:exejar>
```

探测启动类

```xml
<exejar destfile="target/my-application.jar" classes="target/classes">
    <lib>
        <fileset dir="lib" />
    </lib>
</exejar>
```

#### 8.3.2. `spring-boot:findmainclass`

`exejar` 在内部使用 `findmainclass` 任务来查找声明 `main` 的类。如有必要，您也可以在构建中直接使用此任务。支持以下属性：

| Attribute     | Description                   | Required                      |
| :------------ | :---------------------------- | :---------------------------- |
| `classesroot` | Java 类文件的根目录           | Yes *(除非指定了主类)*        |
| `mainclass`   | 能够用于短路 `main` 类搜索    | No                            |
| `property`    | 应该与结果一起设置的 Ant 属性 | No *(如果未指定，将记录结果)* |

##### 示例

本节包含三个使用 `findmainclass` 的示例。

查找并记录

```xml
<findmainclass classesroot="target/classes" />
```

查找并设置

```xml
<findmainclass classesroot="target/classes" property="main-class" />
```

覆盖并设置

```xml
<findmainclass mainclass="com.example.MainClass" property="main-class" />
```