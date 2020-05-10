### 构造

创建 `Multimap` 的最直接的方式是使用 [`MultimapBuilder`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MultimapBuilder.html)，允许你配置应该如何表示你的键和值。比如：

```java
// creates a ListMultimap with tree keys and array list values
ListMultimap<String, Integer> treeListMultimap =
    MultimapBuilder.treeKeys().arrayListValues().build();

// creates a SetMultimap with hash keys and enum set values
SetMultimap<Integer, MyEnum> hashEnumMultimap =
    MultimapBuilder.hashKeys().enumSetValues(MyEnum.class).build();
```

你也可以选择直接使用实现类上的 `create()` 方法，但是我们并不太建议使用 `MultimapBuilder`。

### 修改

[`Multimap.get(key)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#get-K-) 返回与特定键关联的值视图，即使不存在。对于 `ListMultimap`，它返回一个 `List`，对于 `SetMultimap`，它返回一个 `Set`。

修改会写入底层的 `Multimap`。比如：

```java
Set<Person> aliceChildren = childrenMultimap.get(alice);
aliceChildren.clear();
aliceChildren.add(bob);
aliceChildren.add(carol);
```

其它更直接的修改 multimap 的方法包括：

| Signature                                                    | Description                                                  | Equivalent                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`put(K, V)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#put-K-V-) | 添加一个键到值的关联。                                       | `multimap.get(key).add(value)`                               |
| [`putAll(K, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#putAll-K-java.lang.Iterable-) | 依次添加键到每个值的关联。                                   | `Iterables.addAll(multimap.get(key), values)`                |
| [`remove(K, V)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#remove-java.lang.Object-java.lang.Object-) | 删除一个从 `key` 到 `value` 的关联，如果 multimap 改变则返回 `true` 。 | `multimap.get(key).remove(value)`                            |
| [`removeAll(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#removeAll-java.lang.Object-) | 删除并返回与指定键关联的所有值。返回的集合可能可以修改，也可以不可修改，但是对其进行修改不会影响 multimap。（返回适当的集合类型。） | `multimap.get(key).clear()`                                  |
| [`replaceValues(K, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#replaceValues-K-java.lang.Iterable-) | 清除所有与 `key` 关联的值，并将 `key` 设置为与每个`values` 关联。返回先前与该键关联的值。 | `multimap.get(key).clear(); Iterables.addAll(multimap.get(key), values)` |