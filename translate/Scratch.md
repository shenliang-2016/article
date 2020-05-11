## RangeSet

`RangeSet` 描述了 *不连续的，非空的* 范围的一个集合。当添加一个范围到一个可变的 `RangeSet`，任何连接的范围都将合并，而空范围将被忽略。比如：

```java
   RangeSet<Integer> rangeSet = TreeRangeSet.create();
   rangeSet.add(Range.closed(1, 10)); // {[1, 10]}
   rangeSet.add(Range.closedOpen(11, 15)); // disconnected range: {[1, 10], [11, 15)}
   rangeSet.add(Range.closedOpen(15, 20)); // connected range; {[1, 10], [11, 20)}
   rangeSet.add(Range.openClosed(0, 0)); // empty range; {[1, 10], [11, 20)}
   rangeSet.remove(Range.open(5, 10)); // splits [1, 10]; {[1, 5], [10, 10], [11, 20)}
```

注意，如果要合并的范围类似 `Range.closed(1, 10)` 和 `Range.closedOpen(11, 15)`，你必须首先使用 [`Range.canonical(DiscreteDomain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Range.html#canonical-com.google.common.collect.DiscreteDomain-) 对这些范围进行预处理，比如，使用 `DiscreteDomain.integers()`。

**注意**： `RangeSet` 在 GWT 下不支持，也不在 JDK 1.5 反向移植中， `RangeSet` 需要完整使用  JDK 1.6 中的 `NavigableMap` 特性。

### 视图

`RangeSet` 实现支持相当宽泛的视图，包括：

- `complement()`：查看 `RangeSet` 的补集。 `complement` 也是一个 `RangeSet`，因为它也包含不连续的，非空的范围。
- `subRangeSet(Range<C>)`：返回 `RangeSet` 和指定 `Range` 的交集。这会产生传统有序集合的 `headSet`， `subSet`，以及  `tailSet` 视图。
- `asRanges()`：将 `RangeSet` 视作 `Set<Range<C>>` 因而可以通过迭代器遍历。
- `asSet(DiscreteDomain<C>)` (`ImmutableRangeSet` only)：以 `ImmutableSortedSet<C>` 的形式查看 `RangeSet<C>` ，查看范围内的元素，而不是范围本身。（如果 `DiscreteDomain` 和 `RangeSet` 都无上界或无下界，则不支持此操作。）

### 查询

除了视图上的操作外，`RangeSet` 还直接支持多种查询操作，其中最主要的是：

- `contains(C)`：对 `RangeSet` 的最基本操作，查询 `RangeSet` 中的任何范围是否包含指定的元素。

- `rangeContaining(C)`：返回包围指定元素的 `Range` ，如果没有则返回 `null`。

- `encloses(Range<C>)`：很简单，测试 `RangeSet` 中的 `Range` 是否包含指定范围。

- `span()`：返回最小的 `Range`，该 `Range` 将 `RangeSet` 中的每个范围包围起来。

