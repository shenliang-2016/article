## Table

```java
Table<Vertex, Vertex, Double> weightedGraph = HashBasedTable.create();
weightedGraph.put(v1, v2, 4);
weightedGraph.put(v1, v3, 20);
weightedGraph.put(v2, v3, 5);

weightedGraph.row(v1); // returns a Map mapping v2 to 4, v3 to 20
weightedGraph.column(v3); // returns a Map mapping v1 to 20, v2 to 5
```

通常，当您尝试一次索引多个键时，您会遇到诸如 `Map<FirstName, Map<LastName, Person>>` 之类的东西，使用起来很丑陋且笨拙。Guava 提供了一种新的集合类型 [`Table`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html) ，它支持任何“行”类型和“列”类型的这种应用场景。`Table` 支持多种视图，可让您从任何角度使用数据，包括：

- [`rowMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#rowMap--)，将 `Table<R, C, V>` 视作 `Map<R, Map<C, V>>`。类似地， [`rowKeySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#rowKeySet--) 返回 `Set<R>`。
- [`row(r)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#row-R-) 返回非空 `Map<C, V>`。写入 `Map` 将会直接写穿透到底层的 `Table`。
- 提供了类似的列方法： [`columnMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#columnMap--)， [`columnKeySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#columnKeySet--)， 和 [`column(c)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#column-C-)。 (基于列的访问效率稍低于基于行的访问。)
- [`cellSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#cellSet--) 返回的视图将 `Table` 视作 [`Table.Cell`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.Cell.html) 集合。 `Cell` 类似于 `Map.Entry`，但是区分行键和列键。

提供了若干种 `Table` 实现，包括：

- [`HashBasedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashBasedTable.html)，由 `HashMap<R, HashMap<C, V>>` 支撑实现。
- [`TreeBasedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeBasedTable.html)，由 `TreeMap<R, TreeMap<C, V>>` 支撑实现。
- [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html)
- [`ArrayTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ArrayTable.html)，要求在构造时指定行和列的完整纬度，但是当表密集时，由二维数组支持，以提高速度和内存效率。`ArrayTable` 的工作方式与其他实现有所不同。有关详细信息，请查阅 Javadoc。