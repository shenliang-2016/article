# Googel Guava User Guide

https://github.com/google/guava/wiki

Joshua O'Madadhain edited this page on 25 Oct 2016 · [5 revisions](https://github.com/google/guava/wiki/Home/_history)

## 介绍

Guava 项目包含若干个 Google 核心类库，这些类库用在 Java 项目中：集合，缓存，基本数据类型支持，并发类库，通用注解，字符串处理，I/O，等等。这些工具趋势都是 Google 的开发人员每天在生产服务开发中使用的。

不过通读 Javadoc 并不是学习如何使用一个类库的高效方法。这里我们尝试提供了一份更具可读性和趣味性的读物来解释一些最流行和最强大的 Guava 特性。

本 wiki 是一个进行中的项目，其中很多部分仍然在持续更新中。

- 基础工具：使得使用 Java 语言更具乐趣。
  - [使用和避免 null](https://github.com/google/guava/wiki/UsingAndAvoidingNullExplained): `null` 是模棱两可的，可能导致令人迷惑的错误，或者就是淡出的令人不爽。许多 Guava 的工具类拒绝接受 `null` 并对其执行快速失败，而不是默默接受。
  - [预定义条件](https://github.com/google/guava/wiki/PreconditionsExplained): 最简单的方式为你的方法测试预定义条件。
  - [通用对象方法](https://github.com/google/guava/wiki/CommonObjectUtilitiesExplained): 简化 `Object` 方法的实现，比如 `hashCode()` 和 `toString()`。
  - [排序](https://github.com/google/guava/wiki/OrderingExplained): Guava 强大的 "链式 `Comparator`" 类。
  - [Throwables](https://github.com/google/guava/wiki/ThrowablesExplained): 对异常和错误的处理和检查的简化。
- 集合：Guava 对 JDK 集合生态系统的扩展。这是 Guava 最成熟和流行的部分。
  - [不可变集合](https://github.com/google/guava/wiki/ImmutableCollectionsExplained)，用于防御性编程，常量集合，以及改善性能。
  - [新的集合类型](https://github.com/google/guava/wiki/NewCollectionTypesExplained)，用于 JDK 集合尚未覆盖的应用场景。主要包括：multisets, multimaps, tables, bidirectional maps, 等等。
  - [强大的集合工具类](https://github.com/google/guava/wiki/CollectionUtilitiesExplained)，用于 `java.util.Collections`  未提供的通用集合操作。
  - [扩展工具](https://github.com/google/guava/wiki/CollectionHelpersExplained): 编写 `Collection` decorator? 实现 `Iterator`? 我们可以使其更简单。
- Graphs：用于建模 [graph](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))-structured 数据的类库，也就是说，实体以及它们之间的关系。关键特性包括：
  - [Graph](https://github.com/google/guava/wiki/GraphsExplained#graph): 其中的边是没有 id 和其它信息的实体的图。
  - [ValueGraph](https://github.com/google/guava/wiki/GraphsExplained#valuegraph): 其中的边拥有不唯一的值的图。
  - [Network](https://github.com/google/guava/wiki/GraphsExplained#network): 其中的边是唯一对象的图。
  - 支持可变和不可变图，有向图和无向图，以及若干其它属性。
- [缓存](https://github.com/google/guava/wiki/CachesExplained): 本地缓存，保证正确的行为，同时支持各种不同的超时失效行为。
- [功能习语](https://github.com/google/guava/wiki/FunctionalExplained): 尽管很少见，Guava 的功能习语可以显著简化代码。
- 并发：强大而简单的抽象，使得编写并发代码变得简单。
  - [ListenableFuture](https://github.com/google/guava/wiki/ListenableFutureExplained): Futures, 携带当它们被完成时会被调用的回调。
  - [Service](https://github.com/google/guava/wiki/ServiceExplained): 启动和关闭相关操作，为您处理困难的状态逻辑。
- [Strings](https://github.com/google/guava/wiki/StringsExplained): 一些非常有用的字符串工具类：切分，连接，填充，等等。
- [Primitives](https://github.com/google/guava/wiki/PrimitivesExplained): 基本数据类型操作，比如 `int` 和 `char`，JDK 并未提供这些操作，包括某些类型的无符号变体。
- [Ranges](https://github.com/google/guava/wiki/RangesExplained): Guava 的强大 API 用于 `Comparable` 类型的范围操作，包括连续数据类型和离散数据类型。
- [I/O](https://github.com/google/guava/wiki/IOExplained): 简化的 I/O 操作，特别是针对 Java 5 中 6 的 I/O 流和文件操作。
- [Hashing](https://github.com/google/guava/wiki/HashingExplained): 比 `Object.hashCode()` 提供的更复杂哈希的工具，包括 Bloom 过滤器。
- [EventBus](https://github.com/google/guava/wiki/EventBusExplained): 组件之间的发布-订阅式通信，而无需组件之间进行显式注册。
- [Math](https://github.com/google/guava/wiki/MathExplained): JDK 未提供经过优化，经过全面测试的数学实用程序。
- [Reflection](https://github.com/google/guava/wiki/ReflectionExplained): 用于 Java 反射功能的 Guava 实用程序。
- 提示：使用 Guava 使您的应用程序按您希望的方式工作。
  - [哲学Philosophy](https://github.com/google/guava/wiki/PhilosophyExplained): Guava 是什么而不是什么，以及我们的目标。
  - [在构建中使用 Guava](https://github.com/google/guava/wiki/UseGuavaInYourBuild), 使用的构建系统包括 Maven, Gradle, 等等。
  - [使用 ProGuard](https://github.com/google/guava/wiki/UsingProGuardWithGuava) 避免将你不需要的 Guava 部分打包进入你的 JAR 中。
  - [Apache Commons equivalents](https://github.com/google/guava/wiki/ApacheCommonCollectionsEquivalents), 帮助您从使用 Apache Commons Collections 转换代码。
  - [兼容性](https://github.com/google/guava/wiki/Compatibility), Guava 不同版本之间的细节差异。
  - [Idea Graveyard](https://github.com/google/guava/wiki/IdeaGraveyard), 功能请求已被最终拒绝。
  - [Friends](https://github.com/google/guava/wiki/FriendsOfGuava), 我们喜欢并欣赏的开源项目。
  - [HowToContribute](https://github.com/google/guava/wiki/HowToContribute), 如何为 Guava 做贡献。

**注意：**要讨论此 wiki 的内容，请仅使用 Guava 讨论邮件列表。

## 基础工具

### 使用和避免 `null`

> *"Null sucks."* -[Doug Lea](http://en.wikipedia.org/wiki/Doug_Lea)
>
> *"I call it my billion-dollar mistake."* - [Sir C. A. R. Hoare](http://en.wikipedia.org/wiki/C._A._R._Hoare), on his invention of the null reference

不小心使用 `null` 会导致各种各样的错误。通过研究 Google 代码库，我们发现 95％ 的集合中不支持包含任何 `null` 值，而让它们快速失败而不是默默地接受 `null` 会对开发人员有所帮助。

另外，`null` 是令人不愉快的模棱两可。`null` 返回值应该是什么意思很不明确，例如，`Map.get(key)` 可以返回 `null`，要么是因为映射中的值为 `null`，要么就是该值不在映射中 。Null 可能意味着失败，可能意味着成功，几乎可以意味着任何事情。使用 `null` 以外的东西可以使您的意思更清楚。

也就是说，有时候 `null` 是正确正确的用法。就内存和速度而言，`null` 很节约资源，并且在对象数组中不可避免。但是在应用程序代码中，与库相反，它是混乱，棘手的怪异错误以及令人不快的歧义的主要来源—例如，当 `Map.get` 返回 `null` 时，可能意味着该值不存在，或者该值存在且为 `null`。最关键的是，`null` 完全不能表示 `null` 值的含义。

由于这些原因，只要有可用的 `null` 友好解决方案，Guava 的许多实用程序都被设计为在存在 `null` 的情况下快速失败，而不是允许使用 `null` 。另外，Guava 提供了许多便利，既可以在必要时简化使用 `null` 的工作，又可以帮助您避免使用 `null`。

#### 具体案例

如果您尝试在 `Set` 中使用 `null` 值或在 `Map` 中作为键，请不要使用；如果在查找操作期间显式使用特殊的 `null`，则更清楚（不足为奇）。

如果要在 Map 中使用 `null` 作为值，请忽略该条目；单独保存一组非空键（或空键）。将 `Map` 包含该键对应的项（值为空）的情况与 `Map` 没有该键对应的项的情况混合起来很容易。最好将这些键分开，并考虑与键关联的值为 `null` 时，它对您的应用程序意味着什么。

如果您在 `List` 中使用空值-如果列表稀疏，您可能宁愿使用 `Map<Integer, E>`？这实际上可能更有效，并且可能实际上可以更准确地满足您的应用程序需求。

考虑是否存在可以使用的自然“空对象”，有时候是如此。例如，如果它是一个枚举，请添加一个常量以表示您期望 `null` 表示的含义。例如，`java.math.RoundingMode` 具有一个 `UNNECESSARY` 值，以指示“不进行舍入，如果需要舍入则抛出异常”。

如果您确实需要 `null` 值，并且在使用 `null` 敌对的 `collection` 实现时遇到问题，请使用其他实现。例如，使用 `Collections.unmodifiableList(Lists.newArrayList())` 而不是 `ImmmableableList`。

#### Optional

程序员使用 `null` 的许多情况是为了表明某种缺席：也许在有值，无值或找不到值的地方。例如，如果未找到键值，则 `Map.get` 返回 `null`。

`Optional<T>` 是用非 `null` 值替换可为空的 `T` 引用的一种方法。一个 `Optional` 可能包含一个非空的 `T` 引用（在这种情况下，我们说该引用是“存在”），或者可能不包含任何内容（在这种情况下，我们说该引用是“不存在”），永远不表示“包含 null”。

```java
Optional<Integer> possible = Optional.of(5);
possible.isPresent(); // returns true
possible.get(); // returns 5
```

`Optional` 并不是与其他编程环境中任何现有 "option" 或 "maybe" 构造的直接类似物，尽管它可能具有某些相似之处。

我们在这里列出了一些最常见的 `Optional` 操作。

##### 创建 Optional

`Optional` 包含下表中的静态方法。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`Optional.of(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of-T-) | 创建一个包含给定的非空值，或者对 null 快速失败的 Optional 。 |
| [`Optional.absent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#absent--) | 返回某类型的一个不存在的 Optional 。                         |
| [`Optional.fromNullable(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#fromNullable-T-) | 将给定的可能为 null 的引用转换为 Optional，将 non-null 视为存在，将 null 视为不存在。 |

##### 查询方法

这些都是基于特定 `Optional<T>` 值的非静态方法。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`boolean isPresent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#isPresent--) | 如果该 `Optional` 包含一个非空实例则返回 `true` 。           |
| [`T get()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#get--) | 返回包含的 `T` 实例，该实例必须存在； 否则，抛出 `IllegalStateException`。 |
| [`T or(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#or-T-) | 返回此`Optional` 中的当前值，如果没有，则返回指定的默认值。  |
| [`T orNull()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#orNull--) | 返回此 `Optional` 中的当前值，如果没有，则返回 `null` 。是 `fromNullable` 的逆运算。 |
| [`Set asSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#asSet--) | 如果有一个实例，则返回一个不可变的单例 `Set`，其中包含 `Optional` 中的实例，否则返回一个空的不可变集。 |

`Optional` 还提供了一些其它通用方法，查看文档了解有关细节。

##### 重点是什么？

除了给 `null` 一个 *name* 带来的可读性提高之外，`Optional` 的最大优点是它的防呆能力。如果您要完全编译程序，它会迫使您积极考虑不存在的情况，因为您必须主动展开 `Optional` 并解决该情况。Null 使得简单地忘记事情变得异常容易，尽管 FindBugs 有所帮助，但我们认为它几乎不能解决问题。

当您**返回**可能存在或可能不存在的值时，这一点尤其重要。您（和其他人）更有可能忘记 `other.method(a, b)` 可能返回空值，而您可能会忘记 `a` 在实现 `other.method` 时可能为 `null`。返回 `Optional` 使调用者无法忘记这种情况，因为调用者必须自己打开对象才能编译代码。

#### 便利方法

无论何时，如果你想要用某些默认值替换 `null` 值，使用 [`MoreObjects.firstNonNull(T, T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/MoreObjects.html#firstNonNull-T-T-)。正如方法名称所暗示的，如果两个输入参数都是 null，该方法将快速失败并抛出 `NullPointerException`。如果你正在使用 `Optional`，那么有个更好的替代品—比如， `first.or(second)`。

在 `Strings` 中提供了一些处理可能为 `null` 的 `String` 值的方法。具体来说，我们提供恰当的名称：

- [`emptyToNull(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#emptyToNull-java.lang.String-)
- [`isNullOrEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#isNullOrEmpty-java.lang.String-)
- [`nullToEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#nullToEmpty-java.lang.String-)

我们想强调的是，这些方法主要用于与使 null 字符串和空字符串相等的令人讨厌的 API 进行接口。每次*您*编写将 null 字符串和空字符串放在一起的代码时，Guava 团队都会哭泣。（如果 null 字符串和空字符串在含义上是积极不同的，那会更好，但是将它们视为同一件事是一种令人不安的常见代码味道。）

### Preconditions

Guava 提供了大量的 precondition 检查工具。我们强烈推荐你静态导入它们。

每个方法都有三种变体：

1. 没有额外参数。所有抛出的异常都不携带错误信息。
2. 一个额外的 `Object` 参数。所有抛出的异常都携带错误信息 `object.toString()`。
3. 一个额外的 `String` 参数，以及任意数量的额外 `Object` 参数。此行为类似于 printf，但是为了 GWT 兼容性和执行效率，只允许 `%s` 占位符。
   - 注意：`checkNotNull`，`checkArgument` 和 `checkState` 具有大量重载，这些重载采用基本数据类型参数和 `Object` 参数的组合，而不是 varargs 数组—在绝大多数情况下这允许上述调用避免基本数据类型装箱和 varags 数组分配。

第三种变体的例子：

```
checkArgument(i >= 0, "Argument was %s but expected nonnegative", i);
checkArgument(i < j, "Expected i < j, but %s >= %s", i, j);
```

| Signature (not including extra args)                         | Description                                                  | Exception thrown on failure |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------- |
| [`checkArgument(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkArgument-boolean-) | 检查布尔值是否为 `true`。用于验证方法的参数。                | `IllegalArgumentException`  |
| [`checkNotNull(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkNotNull-T-) | 检查值是否不为 `null`。直接返回值，因此可以内联使用 `checkNotNull(value)`。 | `NullPointerException`      |
| [`checkState(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState-boolean-) | 检查对象的某些状态，而不依赖于方法参数。 例如，`Iterator`可能会使用它来检查是否在调用 `remove` 之前调用了`next`。 | `IllegalStateException`     |
| [`checkElementIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkElementIndex-int-int-) | 检查 `index` 是否为指定大小的列表，字符串或数组中的有效 *element* 索引。元素索引的范围可以从 0（含0）到 `size`（不含）。您不直接传递列表，字符串或数组；你只要通过它的大小。返回 `index`。 | `IndexOutOfBoundsException` |
| [`checkPositionIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkPositionIndex-int-int-) | 检查`index`是否为指定大小的列表，字符串或数组中的有效“位置”索引。位置索引的范围可以从 0（含0）到 `size`（含）。 您不直接传递列表，字符串或数组；你只传递它的大小。返回`index`。 | `IndexOutOfBoundsException` |
| [`checkPositionIndexes(int start, int end, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkPositionIndexes-int-int-int-) | 检查 `[start, end)` 是具有指定大小的列表，字符串或数组的有效子范围。带有自己的错误消息。 | `IndexOutOfBoundsException` |

由于某些原因，我们更倾向于使用来自 Apache Commons 类库的工具来更新上面示例中的 preconditions 检查。主要原因：

- 静态导入后，Guave 方法清晰明了。 `checkNotNull` 可以清楚地说明正在执行的操作以及抛出的异常。
- `checkNotNull` 校验之后返回它的参数，允许跟构造方法调用放在一行的写法： `this.field = checkNotNull(field);`。
- 简单的， varargs "printf-style" 异常信息。(这个优点也是为何我们推荐继续使用 `checkNotNull` 在 [`Objects.requireNonNull`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#requireNonNull(java.lang.Object,java.lang.String)))

我们建议您将  preconditions  分成不同的行，这可以帮助您确定调试时哪个前提条件失败。此外，您还应该提供有用的错误消息，当每项检查单独执行时，此消息会更容易。