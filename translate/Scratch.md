##### 自定义应用信息

你可以通过设定 `info.*` Spring 属性自定义通过 `info` 端点暴露的数据。位于 `info` 键之下的所有 `Environment` 属性会自动暴露。比如，你可以添加下面的设定到你的 `application.properties` 文件中：

```properties
info.app.encoding=UTF-8
info.app.java.source=1.8
info.app.java.target=1.8
```

> 除了硬编码这些值，你还可以 [在构建时扩展 info 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-automatic-expansion).
>
>  假定你使用了 Maven，你还可以像下面这样重写上面的例子：
>
> ```properties
> info.app.encoding=@project.build.sourceEncoding@
> info.app.java.source=@java.version@
> info.app.java.target=@java.version@
> ```

##### Git 提交信息

`info` 端点的另一个有用的功能是它能够在构建项目时发布有关 `git` 源代码存储库状态的信息。如果有一个 `GitProperties` bean，则将暴露 `git.branch`，`git.commit.id` 和 `git.commit.time` 属性。

> 如果 `git.properties` 文件存在于类路径根目录下则 `GitProperties` bean 会被自动配置。参考 "[生成 git 信息](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-git-info)" 了解更多细节。

如果你想要显示完整的 git 信息（也就是 `git.properties` 的完整内容），使用 `management.info.git.mode` 属性，如下所示：

```properties
management.info.git.mode=full
```

##### Build Information

If a `BuildProperties` bean is available, the `info` endpoint can also publish information about your build. This happens if a `META-INF/build-info.properties` file is available in the classpath.

> The Maven and Gradle plugins can both generate that file. See "[Generate build information](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-build-info)" for more details.

##### Writing Custom InfoContributors

To provide custom application information, you can register Spring beans that implement the [`InfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java) interface.

The following example contributes an `example` entry with a single value:

```java
import java.util.Collections;

import org.springframework.boot.actuate.info.Info;
import org.springframework.boot.actuate.info.InfoContributor;
import org.springframework.stereotype.Component;

@Component
public class ExampleInfoContributor implements InfoContributor {

    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("example",
                Collections.singletonMap("key", "value"));
    }

}
```

If you reach the `info` endpoint, you should see a response that contains the following additional entry:

```json
{
    "example": {
        "key" : "value"
    }
}
```