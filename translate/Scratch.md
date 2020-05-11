## ClassToInstanceMap

有时候，你的 map 键不全都是相同的类型：它们本身是数据类型本身，你希望将它们映射到该类型的值。Guava 提供了 [`ClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html) 来实现这一目的。

除了扩展 `Map` 接口， `ClassToInstanceMap` 提供了方法 [`T getInstance(Class)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html#getInstance-java.lang.Class-) 和 [`T putInstance(Class, T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html#putInstance-java.lang.Class-java.lang.Object-)，这样就消除了不愉快转型的需求，同时增强了类型安全性。

`ClassToInstanceMap` 拥有一个类型参数，典型地名为 `B`，表示 map 管理的类型的上界。比如：

```java
ClassToInstanceMap<Number> numberDefaults = MutableClassToInstanceMap.create();
numberDefaults.putInstance(Integer.class, Integer.valueOf(0));
```

从技术上讲，`ClassToInstanceMap<B>` 实现了 `Map<Class<? extends B>, B>` ，或换句话说，就是从 B 的子类到 B 的实例的映射。这会使 `ClassToInstanceMap` 中涉及的泛型类型引起混淆，但请记住，`B` 始终是 map 中的类型的上界，通常，`B` 只是 `Object`。

Guava 提供了名为 [`MutableClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MutableClassToInstanceMap.html) 和 [`ImmutableClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableClassToInstanceMap.html) 的非常有用的实现。

**重要**：类似于任何其它 `Map<Class, Object>`， `ClassToInstanceMap` 可以包含基本数据类型实体，基本数据类型以及它对应的包装类可以映射到不同的值。