### 视图

`Multimap` 还支持多种强大的视图。

- [`asMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#asMap--) 将任何 `Multimap<K, V>` 看作 `Map<K, Collection<V>>`。返回的 map 支持 `remove`，同时对返回的集合所作的修改是写穿透的，但是该 map 不支持 `put` 或者 `putAll`。关键是，你可以使用 `asMap().get(key)` 当你希望在不存在的键上使用 `null` 而不是一个新的、可写的空集合时。 (你可以并且应该将 `asMap.get(key)` 转化为合适的集合类型 —— `SetMultimap` 转化为 `Set`  , `ListMultimap` 转化为 `List`  —— 但是类型系统不允许 `ListMultimap` 在这里返回 `Map<K, List<V>>`。)
- [`entries`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#entries--) 将 `Collection<Map.Entry<K, V>>` 看作 `Multimap` 中的所有实体。 (对于 `SetMultimap`，就是一个 `Set`。)
- [`keySet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#keySet--) 将 `Multimap` 中的各异键看作一个 `Set`。
- [`keys`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#keys--) 将 `Multimap` 中的键看作一个 `Multiset`，多重性等于与该键关联的值的数量。元素可以从 `Multiset` 中删除，但不能添加；更改将写穿透。
- [`values()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#values--) 将 `Multimap` 中的所有值看作一个 "扁平的" `Collection<V>`，全部作为一个集合。类似于 `Iterables.concat(multimap.asMap().values())`，但是返回一个完整的 `Collection` 。

### Multimap 不是 Map

 `Multimap<K, V>` 不是 `Map<K, Collection<V>>`，尽管这样的 map 可能被用于 `Multimap` 实现。显著的差异包括：

- `Multimap.get(key)` 始终返回一个非 null，可能为空的集合。这并不意味着 multimap 会花费与该键关联的任何内存，而是返回的集合是一个视图，该视图允许您根据需要添加与键的关联。
- 如果您更喜欢类似 `Map` 的行为，即为不在 multimap 中的键返回 `null`，则使用 `asMap()` 视图来获取 `Map<K, Collection<V>>`。（或者，要从 `ListMultimap` 中获取 `Map<K,`**List**`<V>>` ，请使用静态 [`Multimaps.asMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#asMap-com.google.common.collect.ListMultimap-) 方法。`SetMultimap` 和 `SortedSetMultimap` 也存在类似的方法。）
- `Multimap.containsKey(key)` 当且仅当与指定键相关联的任何元素时为 true。特别是，如果键 `k` 先前与一个或多个从 multimap 移除的值相关联，则 `Multimap.containsKey(k)` 将返回 false。
- `Multimap.entries()` 返回 `Multimap` 中所有键的所有条目。如果需要所有键集合条目，请使用 `asMap().entrySet()`。
- `Multimap.size()` 返回整个 multimap 中的条目数，而不是不同键的数。使用 `Multimap.keySet().size()` 来获取不同键的数量。

### Implementations

`Multimap` provides a wide variety of implementations. You can use it in most places you would have used a `Map<K, Collection<V>>`.

| Implementation                                               | Keys behave like... | Values behave like.. |
| ------------------------------------------------------------ | ------------------- | -------------------- |
| [`ArrayListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ArrayListMultimap.html) | `HashMap`           | `ArrayList`          |
| [`HashMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashMultimap.html) | `HashMap`           | `HashSet`            |
| [`LinkedListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedListMultimap.html) `*` | `LinkedHashMap``*`  | `LinkedList``*`      |
| [`LinkedHashMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedHashMultimap.html)`**` | `LinkedHashMap`     | `LinkedHashSet`      |
| [`TreeMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeMultimap.html) | `TreeMap`           | `TreeSet`            |
| [`ImmutableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableListMultimap.html) | `ImmutableMap`      | `ImmutableList`      |
| [`ImmutableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSetMultimap.html) | `ImmutableMap`      | `ImmutableSet`       |

Each of these implementations, except the immutable ones, support null keys and values.

`*` `LinkedListMultimap.entries()` preserves iteration order across non-distinct key values. See the link for details.

`**` `LinkedHashMultimap` preserves insertion order of entries, as well as the insertion order of keys, and the set of values associated with any one key.

Be aware that not all implementations are actually implemented as a `Map<K, Collection<V>>` with the listed implementations! (In particular, several `Multimap` implementations use custom hash tables to minimize overhead.)

If you need more customization, use [`Multimaps.newMultimap(Map, Supplier)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newMultimap-java.util.Map-com.google.common.base.Supplier-) or the [list](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newListMultimap-java.util.Map-com.google.common.base.Supplier-) and [set](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSetMultimap-java.util.Map-com.google.common.base.Supplier-) versions to use a custom collection, list, or set implementation to back your multimap.