# 集合工具类

有 JDK Collections 框架使用经验的程序员都了解和喜欢使用  [`java.util.Collections`](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html) 中的工具类。Guava 提供了更多的工具类，它们遵循这样的原则：静态方法适用于所有的集合。这部分内容也是 Guava 类库最流行和最成熟的部分。

与特定接口相对应的方法以相对直观的方式进行分组：

| Interface                                                    | JDK or Guava? | Corresponding Guava utility class                            |
| ------------------------------------------------------------ | ------------- | ------------------------------------------------------------ |
| `Collection`                                                 | JDK           | [`Collections2`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Collections2.html) |
| `List`                                                       | JDK           | [`Lists`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html) |
| `Set`                                                        | JDK           | [`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) |
| `SortedSet`                                                  | JDK           | [`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) |
| `Map`                                                        | JDK           | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| `SortedMap`                                                  | JDK           | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| `Queue`                                                      | JDK           | [`Queues`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Queues.html) |
| [`Multiset`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multiset) | Guava         | [`Multisets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html) |
| [`Multimap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multimap) | Guava         | [`Multimaps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html) |
| [`BiMap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#BiMap) | Guava         | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| [`Table`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Table) | Guava         | [`Tables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html) |

***正在寻找转换，过滤器之类的东西？ 这些东西在函数式习语下的函数式编程文章中。***

## 静态构造器

JDK 7 之前，构造新的范型集合需要讨厌的冗长代码：

```java
List<TypeThatsTooLongForItsOwnGood> list = new ArrayList<TypeThatsTooLongForItsOwnGood>();
```

相信大家都会觉得这样不太好。Guava 提供了静态方法可以使用范型去推断表达式右边的类型：

```java
List<TypeThatsTooLongForItsOwnGood> list = Lists.newArrayList();
Map<KeyType, LongishValueType> map = Maps.newLinkedHashMap();
```

可以肯定的是，JDK 7 中的菱形运算符使此工作不再那么麻烦：

```java
List<TypeThatsTooLongForItsOwnGood> list = new ArrayList<>();
```

但是 Guava 远不止于此。使用工厂方法模式，我们可以非常方便地使用其起始元素初始化集合。

```java
Set<Type> copySet = Sets.newHashSet(elements);
List<String> theseElements = Lists.newArrayList("alpha", "beta", "gamma");
```

此外，借助命名工厂方法的功能（有效的 Java 元素1），我们可以提高将集合初始化为大小的可读性：

```java
List<Type> exactly100 = Lists.newArrayListWithCapacity(100);
List<Type> approx100 = Lists.newArrayListWithExpectedSize(100);
Set<Type> approx100Set = Sets.newHashSetWithExpectedSize(100);
```

下面列出了提供的精确静态工厂方法及其相应的实用程序类。

*注意*： Guava 引入的新集合类型不公开原始构造函数，也不在实用程序类中包含初始化程序。相反，它们直接公开静态工厂方法，例如：

```java
Multiset<String> multiset = HashMultiset.create();
```

