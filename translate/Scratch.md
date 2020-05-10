## Multimap

m

Every experienced Java programmer has, at one point or another, implemented a `Map<K, List<V>>` or `Map<K, Set<V>>`, and dealt with the awkwardness of that structure. For example, `Map<K, Set<V>>` is a typical way to represent an unlabeled directed graph. Guava's [`Multimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html) framework makes it easy to handle a mapping from keys to multiple values. A `Multimap` is a general way to associate keys with arbitrarily many values.

There are two ways to think of a Multimap conceptually: as a collection of mappings from single keys to single values:

```
a -> 1
a -> 2
a -> 4
b -> 3
c -> 5
```

or as a mapping from unique keys to collections of values:

```
a -> [1, 2, 4]
b -> [3]
c -> [5]
```

In general, the `Multimap` interface is best thought of in terms of the first view, but allows you to view it in either way with the `asMap()` view, which returns a `Map<K, Collection<V>>`. Most importantly, there is no such thing as a key which maps to an empty collection: a key either maps to at least one value, or it is simply not present in the `Multimap`.

You rarely use the `Multimap` interface directly, however; more often you'll use `ListMultimap` or `SetMultimap`, which map keys to a `List` or a `Set` respectively.