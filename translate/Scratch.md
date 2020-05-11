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

Note that to merge ranges like `Range.closed(1, 10)` and `Range.closedOpen(11, 15)`, you must first preprocess ranges with [`Range.canonical(DiscreteDomain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Range.html#canonical-com.google.common.collect.DiscreteDomain-), e.g. with `DiscreteDomain.integers()`.

**NOTE**: `RangeSet` is not supported under GWT, nor in the JDK 1.5 backport; `RangeSet` requires full use of the `NavigableMap` features in JDK 1.6.

### Views

`RangeSet` implementations support an extremely wide range of views, including:

- `complement()`: views the complement of the `RangeSet`. `complement` is also a `RangeSet`, as it contains disconnected, nonempty ranges.
- `subRangeSet(Range<C>)`: returns a view of the intersection of the `RangeSet` with the specified `Range`. This generalizes the `headSet`, `subSet`, and `tailSet` views of traditional sorted collections.
- `asRanges()`: views the `RangeSet` as a `Set<Range<C>>` which can be iterated over.
- `asSet(DiscreteDomain<C>)` (`ImmutableRangeSet` only): Views the `RangeSet<C>` as an `ImmutableSortedSet<C>`, viewing the elements in the ranges instead of the ranges themselves. (This operation is unsupported if the `DiscreteDomain` and the `RangeSet` are both unbounded above or both unbounded below.)

### Queries

In addition to operations on its views, `RangeSet` supports several query operations directly, the most prominent of which are:

- `contains(C)`: the most fundamental operation on a `RangeSet`, querying if any range in the `RangeSet` contains the specified element.
- `rangeContaining(C)`: returns the `Range` which encloses the specified element, or `null` if there is none.
- `encloses(Range<C>)`: straightforwardly enough, tests if any `Range` in the `RangeSet` encloses the specified range.
- `span()`: returns the minimal `Range` that `encloses` every range in this `RangeSet`.