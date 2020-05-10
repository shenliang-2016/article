## Multimap

每个有经验的 Java 开发者可能都体验过实现 `Map<K, List<V>>` 或者 `Map<K, Set<V>>`，然后处理该结构的某些尴尬之处。比如， `Map<K, Set<V>>` 是表示无标签有向图的典型方式。Guava 的 [`Multimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html) 框架使得处理一个键对应多个值的映射关系变得非常简单。 `Multimap` 就是处理一个键关联到任意多个值的关系的通用方法。

有两种方法可以从概念上考虑 Multimap：作为从单个键到单个值的映射的集合：

```
a -> 1
a -> 2
a -> 4
b -> 3
c -> 5
```

或者作为从单个键到值集合的映射：

```
a -> [1, 2, 4]
b -> [3]
c -> [5]
```

通常，最好从第一个视图的角度考虑 `Multimap` 接口，但可以通过 `asMap()` 视图以任何一种方式查看它，该视图返回一个 `Map<K, Collection<V>>`。最重要的是，不存在映射到空集合的键：键要么映射至至少一个值，要么根本不存在于 `Multimap` 中。

但是，您很少直接使用 `Multimap` 接口。 通常，您会使用 `ListMultimap` 或 `SetMultimap`，它们分别将键映射到 `List` 或 `Set`。

