### 8.4. 支持其它构建系统

如果要使用 Maven，Gradle 或 Ant 以外的构建工具，则可能需要开发自己的插件。可执行 jar 需要遵循特定的格式，某些条目需要以未压缩的形式编写（请参阅 [可执行 jar 格式](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar) ，有关详细信息，请参见附录部分）。

Spring Boot Maven 和 Gradle 插件都使用 `spring-boot-loader-tools` 来实际生成 jar。如果需要，可以直接使用此库。

#### 8.4.1. 重新打包压缩包

要重新打包现有的归档文件，使其成为一个独立的可执行归档文件，请使用 `org.springframework.boot.loader.tools.Repackager`。`Repackager` 类采用单个构造函数参数，该参数引用现有的 jar 或 war 归档文件。使用两个可用的 `repackage()` 方法之一来替换原始文件或写入新目标。在重新打包程序运行之前，还可以在其上配置各种设置。

#### 8.4.2. 嵌套类库

重新打包档案时，可以使用 `org.springframework.boot.loader.tools.Libraries` 接口包含对依赖文件的引用。我们这里没有提供任何 `Libraries` 的具体实现，因为它们通常是特定于构建系统的。

如果您的归档文件中已经包含库，则可以使用 `Libraries.NONE`。

#### 8.4.3. 查找主类

如果您不使用 `Repackager.setMainClass()` 指定主类，则重新包装器将使用 [ASM](https://asm.ow2.io/) 来读取类文件，并尝试使用 `public static void main(String[] args)` 方法查找合适的类。如果找到多个候选者，则会引发异常。

#### 8.4.4. 重新打包实现示例

下面的例子展示了一个典型的重新打包实现：

```java
Repackager repackager = new Repackager(sourceJarFile);
repackager.setBackupSource(false);
repackager.repackage(new Libraries() {
            @Override
            public void doWithLibraries(LibraryCallback callback) throws IOException {
                // Build system specific implementation, callback for each dependency
                // callback.library(new Library(nestedFile, LibraryScope.COMPILE));
            }
        });
```

### 8.5. 进一步阅读

如果您对构建工具插件的工作方式感兴趣，可以查看 GitHub 上的 [`spring-boot-tools`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-tools) 模块。有关可执行 jar 格式的更多技术细节，请参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar)。

如果您有与构建相关的特定问题，可以查看 "[how-to](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto)" 指南。
