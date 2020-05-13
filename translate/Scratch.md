## Multisets

标准 `Collection` 操作，比如 `containsAll`，忽略 multiset 中的元素数目，而只关心元素是否存在于 multiset 中。 [`Multisets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html) 提供了提供许多操作，这些操作考虑了 multiset 中元素的多重性。

| Method                                                       | Explanation                                                  | Difference from `Collection` method                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`containsOccurrences(Multiset sup, Multiset sub)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#containsOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 返回 `true` 如果 `sub.count(o) <= super.count(o)` 对所有 `o`。 | `Collection.containsAll`  忽略数目，仅仅测试元素是否包含在其中。 |
| [`removeOccurrences(Multiset removeFrom, Multiset toRemove)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#removeOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 对于 `toRemove` 中元素的每次出现，从 `removeFrom` 中移除一个出现。 | `Collection.removeAll` 移除任何出现在 `toRemove` 中的元素的所有出现。 |
| [`retainOccurrences(Multiset removeFrom, Multiset toRetain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#retainOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 保证 `removeFrom.count(o) <= toRetain.count(o)` 对所有的 `o`。 | `Collection.retainAll` 保留任何在 `toRetain` 中出现过的元素的所有出现。 |
| [`intersection(Multiset, Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#intersection-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 返回两个多集相交的视图，替代 `retainOccurrences` 的一种非破坏性方法。 | 没有类似物。                                                 |

```java
Multiset<String> multiset1 = HashMultiset.create();
multiset1.add("a", 2);

Multiset<String> multiset2 = HashMultiset.create();
multiset2.add("a", 5);

multiset1.containsAll(multiset2); // returns true: all unique elements are contained,
  // even though multiset1.count("a") == 2 < multiset2.count("a") == 5
Multisets.containsOccurrences(multiset1, multiset2); // returns false

multiset2.removeOccurrences(multiset1); // multiset2 now contains 3 occurrences of "a"

multiset2.removeAll(multiset1); // removes all occurrences of "a" from multiset2, even though multiset1.count("a") == 2
multiset2.isEmpty(); // returns true
```

 `Multisets` 中的其他工具包括：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`copyHighestCountFirst(Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#copyHighestCountFirst-com.google.common.collect.Multiset-) | 返回 multiset 的不可变副本，该副本以递减的频率顺序遍历元素。 |
| [`unmodifiableMultiset(Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#unmodifiableMultiset-com.google.common.collect.Multiset-) | 返回 multiset 的不可变视图。                                 |
| [`unmodifiableSortedMultiset(SortedMultiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#unmodifiableSortedMultiset-com.google.common.collect.SortedMultiset-) | 返回排序 multiset 的不可变视图。                             |

```java
Multiset<String> multiset = HashMultiset.create();
multiset.add("a", 3);
multiset.add("b", 5);
multiset.add("c", 1);

ImmutableMultiset<String> highestCountFirst = Multisets.copyHighestCountFirst(multiset);

// highestCountFirst, like its entrySet and elementSet, iterates over the elements in order {"b", "a", "c"}
```

