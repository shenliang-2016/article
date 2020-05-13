## Multimaps

[`Multimaps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html) provides a number of general utility operations that deserve individual explanation.

### `index`

The cousin to `Maps.uniqueIndex`, [`Multimaps.index(Iterable, Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#index-java.lang.Iterable-com.google.common.base.Function-) answers the case when you want to be able to look up all objects with some particular attribute in common, which is not necessarily unique.

Let's say we want to group strings based on their length.

```
ImmutableSet<String> digits = ImmutableSet.of(
    "zero", "one", "two", "three", "four",
    "five", "six", "seven", "eight", "nine");
Function<String, Integer> lengthFunction = new Function<String, Integer>() {
  public Integer apply(String string) {
    return string.length();
  }
};
ImmutableListMultimap<Integer, String> digitsByLength = Multimaps.index(digits, lengthFunction);
/*
 * digitsByLength maps:
 *  3 => {"one", "two", "six"}
 *  4 => {"zero", "four", "five", "nine"}
 *  5 => {"three", "seven", "eight"}
 */
```

### `invertFrom`

Since `Multimap` can map many keys to one value, and one key to many values, it can be useful to invert a `Multimap`. Guava provides [`invertFrom(Multimap toInvert, Multimap dest)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#invertFrom-com.google.common.collect.Multimap-M-) to let you do this, without choosing an implementation for you.

*NOTE:* If you are using an `ImmutableMultimap`, consider [`ImmutableMultimap.inverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultimap.html#inverse--) instead.

```
ArrayListMultimap<String, Integer> multimap = ArrayListMultimap.create();
multimap.putAll("b", Ints.asList(2, 4, 6));
multimap.putAll("a", Ints.asList(4, 2, 1));
multimap.putAll("c", Ints.asList(2, 5, 3));

TreeMultimap<Integer, String> inverse = Multimaps.invertFrom(multimap, TreeMultimap.<String, Integer> create());
// note that we choose the implementation, so if we use a TreeMultimap, we get results in order
/*
 * inverse maps:
 *  1 => {"a"}
 *  2 => {"a", "b", "c"}
 *  3 => {"c"}
 *  4 => {"a", "b"}
 *  5 => {"c"}
 *  6 => {"b"}
 */
```

### `forMap`

Need to use a `Multimap` method on a `Map`? [`forMap(Map)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#forMap-java.util.Map-) views a `Map` as a `SetMultimap`. This is particularly useful, for example, in combination with `Multimaps.invertFrom`.

```
Map<String, Integer> map = ImmutableMap.of("a", 1, "b", 1, "c", 2);
SetMultimap<String, Integer> multimap = Multimaps.forMap(map);
// multimap maps ["a" => {1}, "b" => {1}, "c" => {2}]
Multimap<Integer, String> inverse = Multimaps.invertFrom(multimap, HashMultimap.<Integer, String> create());
// inverse maps [1 => {"a", "b"}, 2 => {"c"}]
```

### Wrappers

`Multimaps` provides the traditional wrapper methods, as well as tools to get custom `Multimap` implementations based on `Map` and `Collection` implementations of your choice.

| Multimap type       | Unmodifiable                                                 | Synchronized                                                 | Custom                                                       |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `Multimap`          | [`unmodifiableMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableMultimap-com.google.common.collect.Multimap-) | [`synchronizedMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedMultimap-com.google.common.collect.Multimap-) | [`newMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `ListMultimap`      | [`unmodifiableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableListMultimap-com.google.common.collect.ListMultimap-) | [`synchronizedListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedListMultimap-com.google.common.collect.ListMultimap-) | [`newListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newListMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SetMultimap`       | [`unmodifiableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSetMultimap-com.google.common.collect.SetMultimap-) | [`synchronizedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSetMultimap-com.google.common.collect.SetMultimap-) | [`newSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSetMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SortedSetMultimap` | [`unmodifiableSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`synchronizedSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`newSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSortedSetMultimap-java.util.Map-com.google.common.base.Supplier-) |

The custom `Multimap` implementations let you specify a particular implementation that should be used in the returned `Multimap`. Caveats include:

- The multimap assumes complete ownership over of map and the lists returned by factory. Those objects should not be manually updated, they should be empty when provided, and they should not use soft, weak, or phantom references.
- **No guarantees are made** on what the contents of the `Map` will look like after you modify the `Multimap`.
- The multimap is not threadsafe when any concurrent operations update the multimap, even if map and the instances generated by factory are. Concurrent read operations will work correctly, though. Work around this with the `synchronized` wrappers if necessary.
- The multimap is serializable if map, factory, the lists generated by factory, and the multimap contents are all serializable.
- The collections returned by `Multimap.get(key)` are *not* of the same type as the collections returned by your `Supplier`, though if you supplier returns `RandomAccess` lists, the lists returned by `Multimap.get(key)` will also be random access.

Note that the custom `Multimap` methods expect a `Supplier` argument to generate fresh new collections. Here is an example of writing a `ListMultimap` backed by a `TreeMap` mapping to `LinkedList`.

```
ListMultimap<String, Integer> myMultimap = Multimaps.newListMultimap(
  Maps.<String, Collection<Integer>>newTreeMap(),
  new Supplier<LinkedList<Integer>>() {
    public LinkedList<Integer> get() {
      return Lists.newLinkedList();
    }
  });
```

## Tables

The [`Tables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html) class provides a few handy utilities.

### `customTable`

Comparable to the `Multimaps.newXXXMultimap(Map, Supplier)` utilities, [`Tables.newCustomTable(Map, Supplier)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#newCustomTable-java.util.Map-com.google.common.base.Supplier-) allows you to specify a `Table` implementation using whatever row or column map you like.

```
// use LinkedHashMaps instead of HashMaps
Table<String, Character, Integer> table = Tables.newCustomTable(
  Maps.<String, Map<Character, Integer>>newLinkedHashMap(),
  new Supplier<Map<Character, Integer>> () {
    public Map<Character, Integer> get() {
      return Maps.newLinkedHashMap();
    }
  });
```

### `transpose`

The [`transpose(Table)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#transpose-com.google.common.collect.Table-) method allows you to view a `Table<R, C, V>` as a `Table<C, R, V>`.

### Wrappers

These are the familiar unmodifiability wrappers you know and love. Consider, however, using [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html) instead in most cases.

- [`unmodifiableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableTable-com.google.common.collect.Table-)
- [`unmodifiableRowSortedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableRowSortedTable-com.google.common.collect.RowSortedTable-)

