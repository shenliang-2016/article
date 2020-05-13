## Maps

[`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) 拥有许多很棒的工具值得单独介绍。

### `uniqueIndex`

[`Maps.uniqueIndex(Iterable, Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#uniqueIndex-java.lang.Iterable-com.google.common.base.Function-) 解决了这样的常见情况：一堆对象每个都有一些独特的属性，并且希望能够基于该属性查找那些对象。

假设我们有一堆已知长度唯一的字符串，并且希望能够查找具有特定长度的字符串。

```java
ImmutableMap<Integer, String> stringsByIndex = Maps.uniqueIndex(strings, new Function<String, Integer> () {
    public Integer apply(String string) {
      return string.length();
    }
  });
```

如果字符串长度不是唯一的，参考下面的 `Multimaps.index` 。

### `difference`

[`Maps.difference(Map, Map)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#difference-java.util.Map-java.util.Map-) 可让您比较两个 maps 之间的所有差异。它返回一个 `MapDifference` 对象，该对象将维恩图分解为：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`entriesInCommon()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesInCommon--) | 同时存在于两个映射中的实体，具有同时匹配的键和值。           |
| [`entriesDiffering()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesDiffering--) | 具有相同键，但是值不同的实体。map 中的值是 [`MapDifference.ValueDifference`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.ValueDifference.html) 类型，你可以看到左值和右值。 |
| [`entriesOnlyOnLeft()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesOnlyOnLeft--) | 返回那些键在左 map 中存在而右 map 中不存在的实体。           |
| [`entriesOnlyOnRight()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesOnlyOnRight--) | 返回那些键在右 map 中存在而左 map 中不存在的实体。           |

```java
Map<String, Integer> left = ImmutableMap.of("a", 1, "b", 2, "c", 3);
Map<String, Integer> right = ImmutableMap.of("b", 2, "c", 4, "d", 5);
MapDifference<String, Integer> diff = Maps.difference(left, right);

diff.entriesInCommon(); // {"b" => 2}
diff.entriesDiffering(); // {"c" => (3, 4)}
diff.entriesOnlyOnLeft(); // {"a" => 1}
diff.entriesOnlyOnRight(); // {"d" => 5}
```

### `BiMap` 工具

`BiMap` 上的 Guava 实用程序位于 `Maps` 类中，因为 `BiMap` 也是 `Map`。

| `BiMap` utility                                              | Corresponding `Map` utility        |
| ------------------------------------------------------------ | ---------------------------------- |
| [`synchronizedBiMap(BiMap)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#synchronizedBiMap-com.google.common.collect.BiMap-) | `Collections.synchronizedMap(Map)` |
| [`unmodifiableBiMap(BiMap)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#unmodifiableBiMap-com.google.common.collect.BiMap-) | `Collections.unmodifiableMap(Map)` |

#### 静态工厂

`Maps` 提供了下列静态工厂方法。

| Implementation    | Factories                                                    |
| ----------------- | ------------------------------------------------------------ |
| `HashMap`         | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMap--), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMap-java.util.Map-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMapWithExpectedSize-int-) |
| `LinkedHashMap`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newLinkedHashMap--), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newLinkedHashMap-java.util.Map-) |
| `TreeMap`         | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap--), [from `Comparator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap-java.util.Comparator-), [from `SortedMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap-java.util.SortedMap-) |
| `EnumMap`         | [from `Class`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newEnumMap-java.lang.Class-), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newEnumMap-java.util.Map-) |
| `ConcurrentMap`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newConcurrentMap--) |
| `IdentityHashMap` | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newIdentityHashMap--) |