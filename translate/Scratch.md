# 新的集合类型

Guava 引入了大量 JDK 中没有的新的集合类型，我们发现这些集合类型非常有用。所有这些都旨在与 JDK 集合框架愉快地共存，而不会在 JDK 集合抽象中产生麻烦。

通常，Guava 集合实现非常精确地遵循 JDK 接口协定。

## Multiset

传统的 Java 习惯用法，例如，计算一个单词在文档中出现的次数是这样的：

```java
Map<String, Integer> counts = new HashMap<String, Integer>();
for (String word : words) {
  Integer count = counts.get(word);
  if (count == null) {
    counts.put(word, 1);
  } else {
    counts.put(word, count + 1);
  }
}
```

这很尴尬，容易出错，并且不支持收集各种有用的统计信息，例如单词总数。我们可以做得更好。

Guava 提供了一种新的集合类型 [`Multiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html) ，它支持添加多个相同元素。Wikipedia 在数学中将“多集”定义为"集合概念的一般化，在该概念中，成员可以多次出现在多集中，如在集中并且与元组相反，元素的顺序无关紧要： 多集 {a，a，b} 和 {a，b，a} 相等。”

有两种主要的查看方式：

- 类似于 `ArrayList<E>` 而没有顺序约束：顺序没有意义。
- 类似于 `Map<E, Integer>`，包含元素和出现次数。

Guava 的 `Multiset` API 综合了两种关于 `Multiset` 的看法，如下：

- 当为作为一个普通 `Collection` 时， `Multiset` 的行为更像是无序的 `ArrayList`：
  - 调用 `add(E)` 添加一个给定元素一次。
  - 多集的 `iterator()` 遍历每个元素的每次出现。
  - 多集的 `size()` 所有元素的所有出现次数的总和。
- 附加的查询操作，以及性能特性，类似于你希望从 `Map<E, Integer>` 那里得到的。
  - `count(Object)` 返回有关该元素的数量。对于 `HashMultiset`，时间复杂度 O(1)，对于 `TreeMultiset`，时间复杂度是 O(log n)。
  - `entrySet()` 返回一个 `Set<Multiset.Entry<E>>` ，其行为类似于 `Map` 的 `entrySet`。
  - `elementSet()` 返回一个 `Set<E>` 包含多集中的独特元素，类似于 `keySet()` 之于 `Map`。
  - `Multiset` 实现的内存假定为与其中独特元素数量为线性关系。

值得注意的是，`Multiset` 完全符合 `Collection` 接口的约定，在极少数情况下，JDK 本身具有先例除外——特别是，`TreeMultiset` 与 `TreeSet` 一样，使用比较替代 `Object.equals` 来判断相等。特别是， `Multiset.addAll(Collection)` 在每次出现时都会在 `Collection` 中添加每个元素一次，这比上面 `Map` 方法所需的 `for` 循环要方便得多。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`count(E)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#count-java.lang.Object-) | 计算已添加到此多集的元素的出现次数。                         |
| [`elementSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#elementSet--) | 以 `Set<E>` 的形式查看 `Multiset<E>` 的不同元素。            |
| [`entrySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#entrySet--) | 与 `Map.entrySet()` 类似，返回 `Set<Multiset.Entry<E>>`，其中包含支持 `getElement()` 和 `getCount()` 的条目。 |
| [`add(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#add-java.lang.Object-int-) | 添加指定元素的指定出现次数。                                 |
| [`remove(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#remove-java.lang.Object-int--) | 删除指定元素的指定出现次数。                                 |
| [`setCount(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#setCount-E-int-) | 将指定元素的出现次数设置为指定的非负值。                     |
| `size()`                                                     | 返回 `Multiset` 中所有元素的出现总数。                       |

### Multiset 不是 Map

注意，尽管 `Multiset<E>` 可能是 `Multiset` 实现的一部分，但它不是 `Map<E, Integer>`。`Multiset` 是一种真正的 `Collection` 类型，它满足所有相关的契约义务。其他显着差异包括：

-  `Multiset<E>` 具有仅具有正计数的元素。没有元素可以具有负计数，并且计数为 0 的值被认为不在多集中。它们不会出现在 `elementSet()` 或 `entrySet()` 视图中。
-  `multiset.size()` 返回集合的大小，该大小等于所有元素的计数之和。对于不同元素的数量，使用 `elementSet().size()`。（因此，例如，`add(E)` 将`multiset.size()` 增加一。）
- `multiset.iterator()` 遍历每个元素的每次出现，因此，迭代的长度等于 `multiset.size()`。
- `Multiset<E>` 支持添加元素，删除元素，或者直接设定元素计数。 `setCount(elem, 0)` 等效与删除该元素的所有出现次数。
- `multiset.count(elem)` 对没有出现在多集中的元素永远返回 `0`。

### 实现

Guava 提供了许多 `Multiset` 实现，大致上对应于 JDK map 实现。

| Map                 | Corresponding Multiset                                       | Supports `null` elements |
| ------------------- | ------------------------------------------------------------ | ------------------------ |
| `HashMap`           | [`HashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashMultiset.html) | Yes                      |
| `TreeMap`           | [`TreeMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeMultiset.html) | Yes                      |
| `LinkedHashMap`     | [`LinkedHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedHashMultiset.html) | Yes                      |
| `ConcurrentHashMap` | [`ConcurrentHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ConcurrentHashMultiset.html) | No                       |
| `ImmutableMap`      | [`ImmutableMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultiset.html) | No                       |

### SortedMultiset

[`SortedMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/SortedMultiset.html) 是 `Multiset` 接口的一种变体，支持在指定范围内有效地提取子多集。例如，您可以使用 `latencies.subMultiset(0, BoundType.CLOSED, 100, BoundType.OPEN).size()` 来确定您的网站在 100ms 延迟内的点击次数，然后将其与 `latencies.size()` 进行比较确定整体比例。

`TreeMultiset` 实现 `SortedMultiset` 接口。在撰写本文时，仍在测试 `ImmutableSortedMultiset` 的 GWT 兼容性。