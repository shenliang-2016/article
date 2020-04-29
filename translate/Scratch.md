#### 7.2.2. 具有多个源文件的应用程序

您可以对所有接受文件输入的命令使用 “shell globbing”。这样可以使您从单个目录使用多个文件，如以下示例所示：

```
$ spring run *.groovy
```

#### 7.2.3. 打包你的应用

您可以使用 `jar` 命令将您的应用程序打包到一个独立的可执行 jar 文件中，如以下示例所示：

```
$ spring jar my-app.jar *.groovy
```

产生的 jar 包含编译应用程序所产生的类以及应用程序的所有依赖关系，以便可以使用 `java -jar` 来运行它。jar 文件还包含来自应用程序的类路径的条目。您可以使用 `--include` 和 `--exclude` 添加和删除 jar 的显式路径。两者都用逗号分隔，并且都接受前缀 “+” 和 “-” 形式，以表示应将其从默认值中删除。默认包括以下内容：

```
public/**, resources/**, static/**, templates/**, META-INF/**, *
```

默认排除项如下：

```
.*, repository/**, build/**, target/**, **/*.jar, **/*.groovy
```

在命令行上输入 `spring help jar` 以获得更多信息。

