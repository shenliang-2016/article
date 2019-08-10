### 比较字符串

通过文本排序的应用程序执行频繁的字符串比较。例如，报表生成器在按字母顺序对字符串列表进行排序时执行字符串比较。

如果您的应用程序受众仅限于说英语的人，则可以使用`String.compareTo`方法执行字符串比较。 `String.compareTo`方法对两个字符串中的 Unicode 字符进行二进制比较。但是，对于大多数语言，不能依赖此二进制比较来对字符串进行排序，因为 Unicode 值与字符的相对顺序不对应。

幸运的是，[`Collator`](https://docs.oracle.com/javase/8/docs/api/java/text/Collator.html) 类允许您的应用程序对不同语言执行字符串比较。在本节中，您将学习如何在排序文本时使用`Collator`类。

**[执行区域无关的比较](https://docs.oracle.com/javase/tutorial/i18n/text/locale.html)**

排序规则定义字符串的排序顺序。这些规则因语言环境而异，因为各种自然语言对单词的排序方式不同。使用`Collator`类提供的预定义排序规则，您可以以与语言环境无关的方式对字符串进行排序。

**[自定义排序规则](https://docs.oracle.com/javase/tutorial/i18n/text/rule.html)**

在某些情况下，`Collator`类提供的预定义排序规则可能不适合您。例如，您可能希望使用`Collator`对其不支持的语言环境的语言对字符串进行排序。在这种情况下，您可以定义自己的排序规则，并将它们分配给`RuleBasedCollator`对象。

**[改进排序性能](https://docs.oracle.com/javase/tutorial/i18n/text/perform.html)**

使用`CollationKey`类，可以提高字符串比较的效率。此类将`String`对象转换为按照给定`Collator`的规则排序的键。

#### 执行区域无关比较

排序规则定义字符串的排序顺序。这些规则因语言环境而异，因为各种自然语言对单词的排序方式不同。您可以使用`Collator`类提供的预定义排序规则来以与语言环境无关的方式对字符串进行排序。

要实例化`Collator`类，请调用`getInstance`方法。通常，您为默认的`Locale`创建一个`Collator`，如下例所示：

```java
Collator myDefaultCollator = Collator.getInstance();
```

你也可以在创建`Collator`时指定一个特定的`Locale`，如下所示：

```java
Collator myFrenchCollator = Collator.getInstance(Locale.FRENCH);
```

`getInstance`方法返回一个`RuleBasedCollator`，它是`Collator`的具体子类。 `RuleBasedCollator`包含一组规则，用于确定您指定的语言环境的字符串的排序顺序。这些规则是为每个区域设置预定义的。因为规则封装在`RuleBasedCollator`中，所以您的程序不需要特殊的例程来处理随语言变化的排序规则。

您调用`Collator.compare`方法来执行与语言环境无关的字符串比较。当第一个字符串参数小于，等于或大于第二个字符串参数时，`compare`方法返回小于，等于或大于零的整数。下表包含对`Collator.compare`的一些示例调用：

| Example                            | Return Value | Explanation                 |
| ---------------------------------- | ------------ | --------------------------- |
| `myCollator.compare("abc", "def")` | `-1`         | `"abc"` is less than "def"  |
| `myCollator.compare("rtf", "rtf")` | `0`          | the two strings are equal   |
| `myCollator.compare("xyz", "abc")` | `1`          | "xyz" is greater than "abc" |

在执行排序操作时使用`compare`方法。名为[`CollatorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/CollatorDemo.java) 的示例程序使用`compare`方法对英语和法语单词数组进行排序。此程序显示当您使用两个不同的 collators 对相同的单词列表进行排序时会发生什么：

```java
Collator fr_FRCollator = Collator.getInstance(new Locale("fr","FR"));
Collator en_USCollator = Collator.getInstance(new Locale("en","US"));
```

排序方法称为`sortStrings`，可以与任何`Collator`一起使用。请注意，`sortStrings`方法调用`compare`方法：

```java
public static void sortStrings(Collator collator, String[] words) {
    String tmp;
    for (int i = 0; i < words.length; i++) {
        for (int j = i + 1; j < words.length; j++) { 
            if (collator.compare(words[i], words[j]) > 0) {
                tmp = words[i];
                words[i] = words[j];
                words[j] = tmp;
            }
        }
    }
}
```

英语`Collator`对单词进行了如下排序：

```
peach
péché
pêche
sin
```

根据法语的排序规则，前面的列表顺序错误。在法语中，péché应该在排序列表中跟随pêche。法语`Collator`正确排序单词数组，如下所示：

```
peach
pêche
péché
sin
```

#### 自定义排序规则

上一节讨论了如何使用区域设置的预定义规则来比较字符串。这些排序规则确定字符串的排序顺序。如果预定义的排序规则不符合您的需要，您可以设计自己的规则并将它们分配给`RuleBasedCollator`对象。

自定义的排序规则包含在传递给`RuleBasedCollator`构造函数的`String`对象中。这是一个简单的例子：

```java
String simpleRule = "< a < b < c < d";
RuleBasedCollator simpleCollator =  new RuleBasedCollator(simpleRule);
```

对于前一个例子中的`simpleCollator`对象，`a`小于`b`，小于`c`，依此类推。比较字符串时，`simpleCollator.compare`方法引用这些规则。用于构造排序规则的完整语法比这个简单示例更灵活，更复杂。有关语法的完整说明，请参阅[`RuleBasedCollator`](https://docs.oracle.com/javase/8/docs/api/java/text/RuleBasedCollator.html) 类的 API 文档。

下面的示例使用两个 collators 对西班牙语单词列表进行排序。此示例的完整源代码位于[`RulesDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/RulesDemo.java) 中。

`RulesDemo`程序首先定义英语和西班牙语的排序规则。该程序将以传统方式对西班牙语单词进行排序。当按照传统规则进行排序时，字母`ch`和`ll`及其大写等价物在排序顺序中各自具有自己的位置。这些字符对在比较它们时就好像是一个字符。例如，`ch`作为单个字母按照排序顺序中的`cz`排序。请注意两个 collators 的规则有何不同：

```java
String englishRules = (
    "< a,A < b,B < c,C < d,D < e,E < f,F " +
    "< g,G < h,H < i,I < j,J < k,K < l,L " +
    "< m,M < n,N < o,O < p,P < q,Q < r,R " +
    "< s,S < t,T < u,U < v,V < w,W < x,X " +
    "< y,Y < z,Z");

String smallnTilde = new String("\u00F1");    // ñ
String capitalNTilde = new String("\u00D1");  // Ñ

String traditionalSpanishRules = (
    "< a,A < b,B < c,C " +
    "< ch, cH, Ch, CH " +
    "< d,D < e,E < f,F " +
    "< g,G < h,H < i,I < j,J < k,K < l,L " +
    "< ll, lL, Ll, LL " +
    "< m,M < n,N " +
    "< " + smallnTilde + "," + capitalNTilde + " " +
    "< o,O < p,P < q,Q < r,R " +
    "< s,S < t,T < u,U < v,V < w,W < x,X " +
    "< y,Y < z,Z");
```

以下代码行创建了 collators 并调用了 sort 例程：

```java
try {
    RuleBasedCollator enCollator = new RuleBasedCollator(englishRules);
    RuleBasedCollator spCollator =
        new RuleBasedCollator(traditionalSpanishRules);

    sortStrings(enCollator, words);
    printStrings(words);
    System.out.println();

    sortStrings(spCollator, words);
    printStrings(words);
} catch (ParseException pe) {
    System.out.println("Parse exception for rules");
}
```

称为`sortStrings`的排序例程是通用的。它将根据任何`Collator`对象的规则对任何单词数组进行排序：

```java
public static void sortStrings(Collator collator, String[] words) {
    String tmp;
    for (int i = 0; i < words.length; i++) {
        for (int j = i + 1; j < words.length; j++) {
            if (collator.compare(words[i], words[j]) > 0) {
                tmp = words[i];
                words[i] = words[j];
                words[j] = tmp;
            }
        }
    }
}
```

使用英语排序规则排序时，单词数组如下：

```
chalina
curioso
llama
luz
```

将前面的列表与以下列表进行比较，后者根据传统的西班牙语排序规则进行排序：

```
curioso
chalina
luz
llama
```