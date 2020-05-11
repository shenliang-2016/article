## BiMap

将值映射回键的传统方法是维护两个单独的映射，并使两个映射保持同步，但这容易出错，并且在映射中已经存在值时会造成极大的混乱。例如：

```java
Map<String, Integer> nameToId = Maps.newHashMap();
Map<Integer, String> idToName = Maps.newHashMap();

nameToId.put("Bob", 42);
idToName.put(42, "Bob");
// what happens if "Bob" or 42 are already present?
// weird bugs can arise if we forget to keep these in sync...
```

一个 [`BiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html) 是这样的一个 `Map<K, V>` ：

- 允许你查看“反向”的 `BiMap<V, K>` 使用 [`inverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#inverse--)
- 保证值是唯一的，使得 [`values()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#values--) 是一个 `Set`

如果你试图将一个键映射到一个已经存在的值，`BiMap.put(key, value)` 将抛出 `IllegalArgumentException` 异常。如果你想要删除任何预先存在的具有特定值的实体，使用 [`BiMap.forcePut(key, value)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#forcePut-java.lang.Object-java.lang.Object-) 。

```java
BiMap<String, Integer> userId = HashBiMap.create();
...

String userForId = userId.inverse().get(id);
```

### 实现

| Key-Value Map Impl | Value-Key Map Impl | Corresponding `BiMap`                                        |
| ------------------ | ------------------ | ------------------------------------------------------------ |
| `HashMap`          | `HashMap`          | [`HashBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashBiMap.html) |
| `ImmutableMap`     | `ImmutableMap`     | [`ImmutableBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableBiMap.html) |
| `EnumMap`          | `EnumMap`          | [`EnumBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/EnumBiMap.html) |
| `EnumMap`          | `HashMap`          | [`EnumHashBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/EnumHashBiMap.html) |

*注意*： `BiMap` 工具，诸如 `synchronizedBiMap` 位于 [`Maps`](https://github.com/google/guava/wiki/CollectionUtilitiesExplained#Maps) 中。