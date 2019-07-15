### 关于 ResourceBundle 类

**ResourceBundle 如何关联到 Locale**

从概念上讲，每个`ResourceBundle`是一组共享相同基本名称的相关子类。下面的列表显示了一组相关的子类。`ButtonLabel`是基本名称。基本名称后面的字符表示语言代码，国家/地区代码和`Locale`的变体。例如，`ButtonLabel_en_GB`匹配由英语（`en`）的语言代码和英国的国家代码（`GB`）指定的`Locale`。

```
ButtonLabel
ButtonLabel_de
ButtonLabel_en_GB
ButtonLabel_fr_CA_UNIX
```

要选择适当的`ResourceBundle`，请调用`ResourceBundle.getBundle`方法。下面的示例为与语言为“法语”，国家为“加拿大”和平台为UNIX匹配的`Locale`选择`ButtonLabel``ResourceBundle`。

```java
Locale currentLocale = new Locale("fr", "CA", "UNIX");
ResourceBundle introLabels = ResourceBundle.getBundle(
                                 "ButtonLabel", currentLocale);
```

如果指定的`Locale`的`ResourceBundle`类不存在，`getBundle`尝试找到最接近的匹配。例如，如果`ButtonLabel_fr_CA_UNIX`是所需的类，默认的`Locale`是`en_US`，`getBundle`将按以下顺序查找类：

```
ButtonLabel_fr_CA_UNIX
ButtonLabel_fr_CA
ButtonLabel_fr
ButtonLabel_en_US
ButtonLabel_en
ButtonLabel
```

请注意，`getBundle`在选择基类（`ButtonLabel`）之前，根据默认的`Locale`查找类。如果`getBundle`在前面的类列表中找不到匹配项，它会抛出一个`MissingResourceException`。为避免抛出此异常，应始终提供不带后缀的基类。

**`ListResourceBundle` 和 `PropertyResourceBundle`子类**

抽象类`ResourceBundle`有两个子类：`PropertyResourceBundle`和`ListResourceBundle`。

`PropertyResourceBundle`由属性文件支持。属性文件是包含可翻译文本的纯文本文件。属性文件不是Java源代码的一部分，它们只能包含`String`对象的值。如果需要存储其他类型的对象，请使用`ListResourceBundle`。 [使用属性文件备份ResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html) 部分向您展示了如何使用`PropertyResourceBundle`。

`ListResourceBundle`类使用方便的列表管理资源。每个`ListResourceBundle`都由一个类文件支持。您可以将任何特定于语言环境的对象存储在`ListResourceBundle`中。要添加对其他`Locale`的支持，请创建另一个源文件并将其编译为类文件。 [使用ListResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/list.html) 部分有一个您可能会觉得有帮助的编码示例。

`ResourceBundle`类很灵活。 如果您首先将特定于语言环境的`String`对象放在`PropertyResourceBundle`中，然后决定使用`ListResourceBundle`，那么对您的代码没有任何影响。例如，以下对`getBundle`的调用将为适当的`Locale`检索`ResourceBundle`，无论`ButtonLabel`是由类还是属性文件备份：

```java
ResourceBundle introLabels = ResourceBundle.getBundle(
                                 "ButtonLabel", currentLocale);
```

**键值对**

`ResourceBundle`对象包含一组键值对。当你想从`ResourceBundle`中检索值时，你指定键，它必须是`String`。该值是特定于语言环境的对象。以下示例中的键是`OkKey`和`CancelKey`字符串：

```java
class ButtonLabel_en extends ListResourceBundle {
    // English version
    public Object[][] getContents() {
        return contents;
    }
    static final Object[][] contents = {
        {"OkKey", "OK"},
        {"CancelKey", "Cancel"},
    };
}
```

要从`ResourceBundle`检索`OK` `String`，您可以在调用`getString`时指定相应的键：

```java
String okLabel = ButtonLabel.getString("OkKey");
```

属性文件包含键值对。键位于等号的左侧，值位于右侧。每对都在单独一行上。值可以仅表示“String”对象。以下示例显示名为`ButtonLabel.properties`的属性文件的内容：

```
OkKey = OK
CancelKey = Cancel
```