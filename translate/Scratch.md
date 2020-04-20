#### 5.6.4. 自定义度量注册

为了注册自定义度量，将 `MeterRegistry` 注入你的组件中，如下面例子所示：

```java
class Dictionary {

    private final List<String> words = new CopyOnWriteArrayList<>();

    Dictionary(MeterRegistry registry) {
        registry.gaugeCollectionSize("dictionary.size", Tags.empty(), this.words);
    }

    // …

}
```

如果你发现在组件或者应用中重复构建一套度量组件，就可以将整套组件封装成为 `MeterBinder` 实现。默认地，来自所有 `MeterBinder` beans 的度量都会自动绑定到 Spring 管理的 `MeterRegistry`。