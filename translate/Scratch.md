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

Notably, `Multiset` is fully consistent with the contract of the `Collection` interface, save in rare cases with precedent in the JDK itself -- specifically, `TreeMultiset`, like `TreeSet`, uses comparison for equality instead of `Object.equals`. In particular, `Multiset.addAll(Collection)` adds one occurrence of each element in the `Collection` for each time it appears, which is much more convenient than the for loop required by the `Map` approach above.

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`count(E)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#count-java.lang.Object-) | Count the number of occurrences of an element that have been added to this multiset. |
| [`elementSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#elementSet--) | View the distinct elements of a `Multiset<E>` as a `Set<E>`. |
| [`entrySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#entrySet--) | Similar to `Map.entrySet()`, returns a `Set<Multiset.Entry<E>>`, containing entries supporting `getElement()` and `getCount()`. |
| [`add(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#add-java.lang.Object-int-) | Adds the specified number of occurrences of the specified element. |
| [`remove(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#remove-java.lang.Object-int--) | Removes the specified number of occurrences of the specified element. |
| [`setCount(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#setCount-E-int-) | Sets the occurrence count of the specified element to the specified nonnegative value. |
| `size()`                                                     | Returns the total number of occurrences of all elements in the `Multiset`. |

### Multiset Is Not A Map

Note that `Multiset<E>` is *not* a `Map<E, Integer>`, though that might be part of a `Multiset` implementation. `Multiset` is a true `Collection` type, and satisfies all of the associated contractual obligations. Other notable differences include:

- A `Multiset<E>` has elements with positive counts only. No element can have negative counts, and values with count `0` are considered to not be in the multiset. They do not appear in the `elementSet()` or `entrySet()` view.
- `multiset.size()` returns the size of the collection, which is equal to the sum of the counts of all elements. For the number of distinct elements, use `elementSet().size()`. (So, for example, `add(E)` increases `multiset.size()` by one.)
- `multiset.iterator()` iterates over each occurrence of each element, so the length of the iteration is equal to `multiset.size()`.
- `Multiset<E>` supports adding elements, removing elements, or setting the count of elements directly. `setCount(elem, 0)` is equivalent to removing all occurrences of the element.
- `multiset.count(elem)` for an element not in the multiset always returns `0`.

### Implementations

Guava provides many implementations of `Multiset`, which *roughly* correspond to JDK map implementations.

| Map                 | Corresponding Multiset                                       | Supports `null` elements |
| ------------------- | ------------------------------------------------------------ | ------------------------ |
| `HashMap`           | [`HashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashMultiset.html) | Yes                      |
| `TreeMap`           | [`TreeMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeMultiset.html) | Yes                      |
| `LinkedHashMap`     | [`LinkedHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedHashMultiset.html) | Yes                      |
| `ConcurrentHashMap` | [`ConcurrentHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ConcurrentHashMultiset.html) | No                       |
| `ImmutableMap`      | [`ImmutableMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultiset.html) | No                       |

### SortedMultiset

[`SortedMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/SortedMultiset.html) is a variation on the `Multiset` interface that supports efficiently taking sub-multisets on specified ranges. For example, you could use `latencies.subMultiset(0, BoundType.CLOSED, 100, BoundType.OPEN).size()` to determine how many hits to your site had under 100ms latency, and then compare that to `latencies.size()` to determine the overall proportion.

`TreeMultiset` implements the `SortedMultiset` interface. At the time of writing, `ImmutableSortedMultiset` is still being tested for GWT compatibility.