### 日期和时间

----

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

----

`Date`对象表示日期和时间。你不能显示或者打印`Date`对象，而必须首先将其适当地格式化为一个`String` 。那么什么才是“合适的”格式？首先，该格式应该遵循最终用户的`Locale`传统。比如，德国认为`20.4.09`是合法的日期，但是美国人则希望同样的日期显示为`4/20/09`。其次，该格式应该包含必要的信息。比如，一个度量网络性能的程序会报告流逝的毫秒数。一个在线约定日历可能不会展示毫秒数，但是它将显示日或者周。

本节解释格式化日期和时间的各种方法，并且以一种区域敏感的方式进行。如果你使用这些技术，你的程序就能在相应的`Locale`显示正确的日期和时间，同时你的源代码将保持独立于任何特定的`Locale` 。

**[使用预定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/dateFormat.html)**

`DateFormat`类提供了特定于区域的预定义格式化风格，使用非常简单。

**[自定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html)**

使用`SimpleDateFormat`类，你可以创建自定义的特定于区域的格式。

**[修改日期格式符号](https://docs.oracle.com/javase/tutorial/i18n/format/dateFormatSymbols.html)**

使用`DateFormatSymbols`类，你可以改变表示年、月、星期几以及其它格式化元素等名称的符号。

#### 使用预定义格式

----

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

----

 [`DateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormat.html) 类允许你以区域敏感的方式使用预定义风格格式化日期和时间。本节接下来将举例说明如何使用`DateFormat` 类。

**日期**

使用`DateFormat`类格式化日期分两个步骤。首先，使用`getDateInstance`方法创建一个格式化器。然后，调用`format`方法，将返回一个`String` 包含格式化的日期。下面的例子通过调用这两个方法格式化今天的日期：

```java
Date today;
String dateOut;
DateFormat dateFormatter;

dateFormatter = DateFormat.getDateInstance(DateFormat.DEFAULT, currentLocale);
today = new Date();
dateOut = dateFormatter.format(today);

System.out.println(dateOut + " " + currentLocale.toString());

```

代码输出如下。注意，格式化的日期随着`Locale`而变化。由于`DateFormat`是区域敏感的，它负责每个`Locale`的格式化细节：

```
30 juin 2009     fr_FR
30.06.2009       de_DE
Jun 30, 2009     en_US
```

前面的代码例子指定了`DEFAULT`格式化风格。该`DEFAULT`风格正好就是`DateFormat`类提供的预定义格式化风格之一。如下所示：

- DEFAULT
- SHORT
- MEDIUM
- LONG
- FULL

下表展示了每种格式化风格为 U.S. 和法国格式化日期的结果：

| Style     | U.S. Locale            | French Locale      |
| --------- | ---------------------- | ------------------ |
| `DEFAULT` | Jun 30, 2009           | 30 juin 2009       |
| `SHORT`   | 6/30/09                | 30/06/09           |
| `MEDIUM`  | Jun 30, 2009           | 30 juin 2009       |
| `LONG`    | June 30, 2009          | 30 juin 2009       |
| `FULL`    | Tuesday, June 30, 2009 | mardi 30 juin 2009 |

**时间**

`Date`对象同时表示日期和时间。使用`DateFormat`类格式化时间类似于格式化日期，除了你需要使用`getTimeInstance`方法创建格式化器，如下所示：

```java
DateFormat timeFormatter =
    DateFormat.getTimeInstance(DateFormat.DEFAULT, currentLocale);
```

下面的表格展示了用于 U.S. 和德国的各种预定义格式化风格：

| Style     | U.S. Locale    | German Locale |
| --------- | -------------- | ------------- |
| `DEFAULT` | 7:03:47 AM     | 7:03:47       |
| `SHORT`   | 7:03 AM        | 07:03         |
| `MEDIUM`  | 7:03:47 AM     | 07:03:07      |
| `LONG`    | 7:03:47 AM PDT | 07:03:45 PDT  |
| `FULL`    | 7:03:47 AM PDT | 7.03 Uhr PDT  |

**日期和时间**

为了在同一个`String`中显示日期和时间，使用`getDateTimeInstance`方法创建格式化器。第一个参数是日期风格，第二个参数是时间风格。第三个参数是`Locale`。如下所示：

```java
DateFormat formatter = DateFormat.getDateTimeInstance(
                           DateFormat.LONG, 
                           DateFormat.LONG, 
                           currentLocale);
```

下面的表格展示了用于 U.S. 和法国的日期和时间格式化风格：

| Style     | U.S. Locale                           | French Locale                  |
| --------- | ------------------------------------- | ------------------------------ |
| `DEFAULT` | Jun 30, 2009 7:03:47 AM               | 30 juin 2009 07:03:47          |
| `SHORT`   | 6/30/09 7:03 AM                       | 30/06/09 07:03                 |
| `MEDIUM`  | Jun 30, 2009 7:03:47 AM               | 30 juin 2009 07:03:47          |
| `LONG`    | June 30, 2009 7:03:47 AM PDT          | 30 juin 2009 07:03:47 PDT      |
| `FULL`    | Tuesday, June 30, 2009 7:03:47 AM PDT | mardi 30 juin 2009 07 h 03 PDT |

#### 自定义格式

----

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

----

上一节中，介绍了`DateFormat`类提供的格式化风格。大多数情况下，这些预定义格式化已经够用了。然而，如果你希望创建自己的自定义格式，你可以使用 [`SimpleDateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html) 类。

下面的例子展示了`SimpleDateFormat`类的方法。你可以在文件 [`SimpleDateFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/SimpleDateFormatDemo.java) 中找到完整的源码。

**关于模式**

当你创建一个`SimpleDateFormat`对象时，你指定一个模式`String`。模式`String`的内容确定了日期和时间的格式。模式语法的完整描述，参考 [Date Format Pattern Syntax](https://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html#datepattern) 。

下面的代码格式化日期和时间，根据传递给`SimpleDateFormat`构造器的模式`String`。`format`方法返回的`String`包含了用于显示的格式化日期和时间。

```java
Date today;
String output;
SimpleDateFormat formatter;

formatter = new SimpleDateFormat(pattern, currentLocale);
today = new Date();
output = formatter.format(today);
System.out.println(pattern + " " + output);

```

下表展示了上面的代码示例为 U.S. `Locale`产生的格式化输出：

| Pattern                      | Output                        |
| ---------------------------- | ----------------------------- |
| dd.MM.yy                     | 30.06.09                      |
| yyyy.MM.dd G 'at' hh:mm:ss z | 2009.06.30 AD at 08:29:36 PDT |
| EEE, MMM d, ''yy             | Tue, Jun 30, '09              |
| h:mm a                       | 8:29 PM                       |
| H:mm                         | 8:29                          |
| H:mm:ss:SSS                  | 8:28:36:249                   |
| K:mm a,z                     | 8:29 AM,PDT                   |
| yyyy.MMMMM.dd GGG hh:mm aaa  | 2009.June.30 AD 08:29 AM      |

**模式和区域**

`SimpleDateFormat`类是区域敏感的。如果你不使用`Locale`参数实例化`SimpleDateFormat`，它将会按照默认`Locale`格式化日期和时间。格式化模式和`Locale`共同决定最终格式。对于相同的模式，`SimpleDateFormat`可以针对不同的`Locale`生成不同的格式化日期和时间。

下面的代码示例中，模式被硬编码到创建`SimpleDateFormat`对象的语句中：

```java
Date today;
String result;
SimpleDateFormat formatter;

formatter = new SimpleDateFormat("EEE d MMM yy", currentLocale);
today = new Date();
result = formatter.format(today);
System.out.println("Locale: " + currentLocale.toString());
System.out.println("Result: " + result);

```

当`CurrentLocale`被设定为不同的值时，前面的代码会产生如下输出：

```
Locale: fr_FR
Result: mar. 30 juin 09
Locale: de_DE
Result: Di 30 Jun 09
Locale: en_US
Result: Tue 30 Jun 09

```

**日期格式模式语法**

你可以使用下表中列出的符号来设计你自己用于格式化日期和时间的格式化模式：

| Symbol | Meaning              | Presentation  | Example               |
| ------ | -------------------- | ------------- | --------------------- |
| G      | era designator       | Text          | AD                    |
| y      | year                 | Number        | 2009                  |
| M      | month in year        | Text & Number | July & 07             |
| d      | day in month         | Number        | 10                    |
| h      | hour in am/pm (1-12) | Number        | 12                    |
| H      | hour in day (0-23)   | Number        | 0                     |
| m      | minute in hour       | Number        | 30                    |
| s      | second in minute     | Number        | 55                    |
| S      | millisecond          | Number        | 978                   |
| E      | day in week          | Text          | Tuesday               |
| D      | day in year          | Number        | 189                   |
| F      | day of week in month | Number        | 2 (2nd Wed in July)   |
| w      | week in year         | Number        | 27                    |
| W      | week in month        | Number        | 2                     |
| a      | am/pm marker         | Text          | PM                    |
| k      | hour in day (1-24)   | Number        | 24                    |
| K      | hour in am/pm (0-11) | Number        | 0                     |
| z      | time zone            | Text          | Pacific Standard Time |
| '      | escape for text      | Delimiter     | (none)                |
| '      | single quote         | Literal       | '                     |

不是字母的字符被视为带引号的文本。也就是说，即使它们没有包含在单引号内，它们也会出现在格式化文本中。

您指定的符号字母数也决定了格式。例如，如果“zz”模式导致“PDT”，则“zzzz”模式生成“Pacific Daylight Time.”。 下表总结了这些规则：

| Presentation  | Number of Symbols                    | Result                                   |
| ------------- | ------------------------------------ | ---------------------------------------- |
| Text          | 1 - 3                                | abbreviated form, if one exists          |
| Text          | >= 4                                 | full form                                |
| Number        | minimum number of digits is required | shorter numbers are padded with zeros (for a year, if the count of 'y' is 2, then the year is truncated to 2 digits) |
| Text & Number | 1 - 2                                | number form                              |
| Text & Number | 3                                    | text form                                |

