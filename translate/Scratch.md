## Multimaps

[`Multimaps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html) 提供了大量通用的操作值得单独介绍。

### `index`

 `Maps.uniqueIndex` 的堂兄， [`Multimaps.index(Iterable, Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#index-java.lang.Iterable-com.google.common.base.Function-) 可以帮助您查找具有某些共同特定属性（不一定是唯一属性）的所有对象。

假设我们要根据字符串的长度对字符串进行分组。

```java
ImmutableSet<String> digits = ImmutableSet.of(
    "zero", "one", "two", "three", "four",
    "five", "six", "seven", "eight", "nine");
Function<String, Integer> lengthFunction = new Function<String, Integer>() {
  public Integer apply(String string) {
    return string.length();
  }
};
ImmutableListMultimap<Integer, String> digitsByLength = Multimaps.index(digits, lengthFunction);
/*
 * digitsByLength maps:
 *  3 => {"one", "two", "six"}
 *  4 => {"zero", "four", "five", "nine"}
 *  5 => {"three", "seven", "eight"}
 */
```

### `invertFrom`

由于 `Multimap` 能够将多个键映射到同一个值，也可以将一个键映射到多个值，它对倒置 `Multimap` 操作非常有用。Guava 提供了 [`invertFrom(Multimap toInvert, Multimap dest)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#invertFrom-com.google.common.collect.Multimap-M-) 来帮助你做到这一点，而没有为你选择一个实现。

*注意*：如果你正在使用 `ImmutableMultimap`，考虑使用 [`ImmutableMultimap.inverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultimap.html#inverse--) 替代。

```java
ArrayListMultimap<String, Integer> multimap = ArrayListMultimap.create();
multimap.putAll("b", Ints.asList(2, 4, 6));
multimap.putAll("a", Ints.asList(4, 2, 1));
multimap.putAll("c", Ints.asList(2, 5, 3));

TreeMultimap<Integer, String> inverse = Multimaps.invertFrom(multimap, TreeMultimap.<String, Integer> create());
// note that we choose the implementation, so if we use a TreeMultimap, we get results in order
/*
 * inverse maps:
 *  1 => {"a"}
 *  2 => {"a", "b", "c"}
 *  3 => {"c"}
 *  4 => {"a", "b"}
 *  5 => {"c"}
 *  6 => {"b"}
 */
```

### `forMap`

需要在 `Map` 上使用 `Multimap` 方法？[`forMap(Map)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#forMap-java.util.Map-) 将 `Map` 视作 `SetMultimap`。这非常有用，比如，与 `Multimaps.invertFrom` 结合使用：

```java
Map<String, Integer> map = ImmutableMap.of("a", 1, "b", 1, "c", 2);
SetMultimap<String, Integer> multimap = Multimaps.forMap(map);
// multimap maps ["a" => {1}, "b" => {1}, "c" => {2}]
Multimap<Integer, String> inverse = Multimaps.invertFrom(multimap, HashMultimap.<Integer, String> create());
// inverse maps [1 => {"a", "b"}, 2 => {"c"}]
```

### Wrappers

`Multimaps` 提供了传统的包装器方法，以及根据您选择的 `Map` 和 `Collection` 实现获取自定义 `Multimap` 实现的工具。

| Multimap type       | Unmodifiable                                                 | Synchronized                                                 | Custom                                                       |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `Multimap`          | [`unmodifiableMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableMultimap-com.google.common.collect.Multimap-) | [`synchronizedMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedMultimap-com.google.common.collect.Multimap-) | [`newMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `ListMultimap`      | [`unmodifiableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableListMultimap-com.google.common.collect.ListMultimap-) | [`synchronizedListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedListMultimap-com.google.common.collect.ListMultimap-) | [`newListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newListMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SetMultimap`       | [`unmodifiableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSetMultimap-com.google.common.collect.SetMultimap-) | [`synchronizedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSetMultimap-com.google.common.collect.SetMultimap-) | [`newSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSetMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SortedSetMultimap` | [`unmodifiableSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`synchronizedSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`newSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSortedSetMultimap-java.util.Map-com.google.common.base.Supplier-) |

自定义的 `Multimap` 实现可让您指定应在返回的 `Multimap` 中使用的特定实现。注意事项包括：

- multimap 假定对图和工厂返回的列表拥有完全所有权。这些对象不应手动更新，提供时应为空，并且不应使用软引用，弱引用或虚引用。

- **不保证**修改 `Multimap` 后 `Map` 的内容是什么样。

- 当任何并发操作更新 multimap 时，即使 multimap 和工厂生成的实例一样，multimap 也不是线程安全的。但是，并发读取操作将正常运行。如有必要，使用 `synchronized` 包装器解决此问题。

- 如果 map，工厂，工厂生成的列表以及 multimap 内容都可序列化，则 multimap 可序列化。

- `Multimap.get(key)` 返回的集合与 `Supplier` 返回的集合的类型不相同，尽管如果供应商返回 `RandomAccess` 列表，则 `Multimap.get(key)` 也将是随机访问。

注意，自定义的 `Multimap` 方法期望一个 `Supplier` 参数来生成新的集合。这是一个编写由 `ListMap` 映射到 `LinkedList` 的 `ListMultimap` 的示例。

```java
ListMultimap<String, Integer> myMultimap = Multimaps.newListMultimap(
  Maps.<String, Collection<Integer>>newTreeMap(),
  new Supplier<LinkedList<Integer>>() {
    public LinkedList<Integer> get() {
      return Lists.newLinkedList();
    }
  });
```

## Tables

 [`Tables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html) 类提供了一些有用的工具。

### `customTable`

相比于 `Multimaps.newXXXMultimap(Map, Supplier)` 工具， [`Tables.newCustomTable(Map, Supplier)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#newCustomTable-java.util.Map-com.google.common.base.Supplier-) 允许你指定一个 `Table` 实现，可以选择使用行或者列映射。

```java
// use LinkedHashMaps instead of HashMaps
Table<String, Character, Integer> table = Tables.newCustomTable(
  Maps.<String, Map<Character, Integer>>newLinkedHashMap(),
  new Supplier<Map<Character, Integer>> () {
    public Map<Character, Integer> get() {
      return Maps.newLinkedHashMap();
    }
  });
```

### `transpose`

 [`transpose(Table)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#transpose-com.google.common.collect.Table-) 方法允许你将 `Table<R, C, V>` 视作 `Table<C, R, V>`。

### Wrappers

这些是您熟悉和喜爱的不可修改的包装器。不过，在大多数情况下，请考虑使用 [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html)。

- [`unmodifiableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableTable-com.google.common.collect.Table-)
- [`unmodifiableRowSortedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableRowSortedTable-com.google.common.collect.RowSortedTable-)