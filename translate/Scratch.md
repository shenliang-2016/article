## RangeMap

`RangeMap` 是一个集合类型，描述了从不相交的非空范围到值的映射。与 `RangeSet` 不同，`RangeMap` 从不“合并”相邻的映射，即使相邻的范围被映射到相同的值。例如：

```java
RangeMap<Integer, String> rangeMap = TreeRangeMap.create();
rangeMap.put(Range.closed(1, 10), "foo"); // {[1, 10] => "foo"}
rangeMap.put(Range.open(3, 6), "bar"); // {[1, 3] => "foo", (3, 6) => "bar", [6, 10] => "foo"}
rangeMap.put(Range.open(10, 20), "foo"); // {[1, 3] => "foo", (3, 6) => "bar", [6, 10] => "foo", (10, 20) => "foo"}
rangeMap.remove(Range.closed(5, 11)); // {[1, 3] => "foo", (3, 5) => "bar", (11, 20) => "foo"}
```

### 视图

`RangeMap` 提供两种视图：

- `asMapOfRanges()`：将 `RangeMap` 视作 `Map<Range<K>, V>`。这可以被用于，比如，遍历 `RangeMap`。
- `subRangeMap(Range<K>)`：将 `RangeMap` 与特定 `Range` 的交集视作 `RangeMap`。这产生了传统的 `headMap`, `subMap`, 和 `tailMap` 操作。