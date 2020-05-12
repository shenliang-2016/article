### 类集合

通常，集合在其他集合上自然支持这些操作，但对可迭代对象不提供支持。

*当输入实际上是一个 Collection 时，这些操作中的每一个都会委托给相应的 Collection 接口方法。*例如，如果将 `Iterables.size` 传递给 `Collection`，它将调用 `Collection.size` 方法而不是通过迭代器遍历。

| Method                                                       | Analogous `Collection` method      | `FluentIterable` equivalent                                  |
| ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------------------ |
| [`addAll(Collection addTo, Iterable toAdd)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#addAll-java.util.Collection-java.lang.Iterable-) | `Collection.addAll(Collection)`    |                                                              |
| [`contains(Iterable, Object)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#contains-java.lang.Iterable-java.lang.Object-) | `Collection.contains(Object)`      | [`FluentIterable.contains(Object)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#contains-java.lang.Object-) |
| [`removeAll(Iterable removeFrom, Collection toRemove)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#removeAll-java.lang.Iterable-java.util.Collection-) | `Collection.removeAll(Collection)` |                                                              |
| [`retainAll(Iterable removeFrom, Collection toRetain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#retainAll-java.lang.Iterable-java.util.Collection-) | `Collection.retainAll(Collection)` |                                                              |
| [`size(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#size-java.lang.Iterable-) | `Collection.size()`                | [`FluentIterable.size()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#size--) |
| [`toArray(Iterable, Class)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#toArray-java.lang.Iterable-java.lang.Class-) | `Collection.toArray(T[])`          | [`FluentIterable.toArray(Class)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toArray-java.lang.Class-) |
| [`isEmpty(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#isEmpty-java.lang.Iterable-) | `Collection.isEmpty()`             | [`FluentIterable.isEmpty()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#isEmpty--) |
| [`get(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#get-java.lang.Iterable-int-) | `List.get(int)`                    | [`FluentIterable.get(int)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#get-int-) |
| [`toString(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#toString-java.lang.Iterable-) | `Collection.toString()`            | [`FluentIterable.toString()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toString--) |

### 流利的可迭代性

除了上面和函数习语 [functional](https://github.com/google/guava/wiki/FunctionalExplained) 中介绍的方法外，`FluentIterable` 还有一些方便的方法可以复制到不可变的集合中：

| Result Type          | Method                                                       |
| -------------------- | ------------------------------------------------------------ |
| `ImmutableList`      | [`toImmutableList()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableList--) |
| `ImmutableSet`       | [`toImmutableSet()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableSet--) |
| `ImmutableSortedSet` | [`toImmutableSortedSet(Comparator)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableSortedSet-java.util.Comparator-) |