## 平台环境

应用程序在平台环境中运行，该平台环境由底层操作系统，Java虚拟机，类库以及启动应用程序时提供的各种配置数据定义。本课程描述了应用程序用于检查和配置其平台环境的一些API。包括三个部分：

- [Configuration Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/config.html) 描述用于访问部署应用程序时提供的配置数据的API，或者由应用程序的用户访问的API。
- [System Utilities](https://docs.oracle.com/javase/tutorial/essential/environment/system.html) 描述了`System`和`Runtime`类中定义的各种API。
- [PATH and CLASSPATH](https://docs.oracle.com/javase/tutorial/essential/environment/paths.html) 描述用于配置JDK开发工具和其他应用程序的环境变量。

### 配置工具

本节介绍一些帮助应用程序访问其启动上下文的配置实用程序。

#### 属性

