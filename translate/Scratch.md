### 通用

| Method                                                       | Description                                                  | See Also                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`concat(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#concat-java.lang.Iterable-) | 返回几个可迭代对象的串联的惰性视图。                         | [`concat(Iterable...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#concat-java.lang.Iterable...-) |
| [`frequency(Iterable, Object)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#frequency-java.lang.Iterable-java.lang.Object-) | 返回对象的出现次数。                                         | Compare `Collections.frequency(Collection, Object)`; see [`Multiset`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multiset) |
| [`partition(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#partition-java.lang.Iterable-int-) | 返回可迭代的分区的不可修改的视图，该视图分为指定大小的块。   | [`Lists.partition(List, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#partition-java.util.List-int-), [`paddedPartition(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#paddedPartition-java.lang.Iterable-int-) |
| [`getFirst(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getFirst-java.lang.Iterable-T-) | 返回 iterable 的第一个元素，如果为空，则返回默认值。         | Compare `Iterable.iterator().next()`, [`FluentIterable.first()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#first--) |
| [`getLast(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getLast-java.lang.Iterable-) | 返回 iterable 的最后一个元素，如果为空则抛出 `NoSuchElementException` 快速失败。 | [`getLast(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getLast-java.lang.Iterable-T-), [`FluentIterable.last()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#last--) |
| [`elementsEqual(Iterable, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#elementsEqual-java.lang.Iterable-java.lang.Iterable-) | 如果可迭代对象具有相同顺序的相同元素，则返回 `true`。        | Compare `List.equals(Object)`                                |
| [`unmodifiableIterable(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#unmodifiableIterable-java.lang.Iterable-) | 返回迭代的不可修改的视图。                                   | Compare `Collections.unmodifiableCollection(Collection)`     |
| [`limit(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#limit-java.lang.Iterable-int-) | 返回一个`Iterable`，最多返回指定数量的元素。                 | [`FluentIterable.limit(int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#limit-int-) |
| [`getOnlyElement(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getOnlyElement-java.lang.Iterable-) | 返回 `Iterable` 中的唯一元素。如果 iterable 为空或具有多个元素，则快速失败。 | [`getOnlyElement(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getOnlyElement-java.lang.Iterable-T-) |

```java
Iterable<Integer> concatenated = Iterables.concat(
  Ints.asList(1, 2, 3),
  Ints.asList(4, 5, 6));
// concatenated has elements 1, 2, 3, 4, 5, 6

String lastAdded = Iterables.getLast(myLinkedHashSet);

String theElement = Iterables.getOnlyElement(thisSetIsDefinitelyASingleton);
  // if this set isn't a singleton, something is wrong!
```

