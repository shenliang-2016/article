### 使用属性文件作为 ResourceBundle 后备

本小节逐步讲解名为 [`PropertiesDemo`](https://docs.oracle.com/javase/tutorial/i18n/resbundle/examples/PropertiesDemo.java) 的示例程序。

**1. 创建默认 Properties 文件**

属性文件是一个简单的文本文件。你可以使用任何文本编辑器创建并维护属性文件。

你应该始终都创建默认属性文件。文件名以你的`ResourceBundle`基本名称开头并以`.properties`作为后缀。在`PropertiesDemo`程序中，该基本名称是`LabelBundle`。因而默认属性文件就叫做`LabelsBundle.properties`。该文件包含以下行：

```
# This is the default LabelsBundle.properties file
s1 = computer
s2 = disk
s3 = monitor
s4 = keyboard
```

请注意，在前面的文件中，注释行以井号（＃）开头。其他行包含键值对。键位于等号的左侧，值位于右侧。例如，`s2`是与值`disk`对应的键。键是任意的。我们可以叫它`s2`或者其他东西，比如`msg5`或`diskID`。但是，一旦定义，键就不应该改变，因为它在源代码中被引用。值可能会更改。实际上，当本地化程序员创建新属性文件以容纳其他语言时，他们会将值翻译为各种语言。

**2. 按需创建额外的 Properties 文件**

要支持其他语言环境，本地化程序员将创建一个包含已翻译值的新属性文件。不需要更改源代码，因为您的程序引用了键而不是值。

例如，要添加对德语的支持，您的本地化程序员将转换`LabelsBundle.properties`中的值，并将它们放在名为`LabelsBundle_de.properties`的文件中。请注意，此文件的名称（如默认文件的名称）以基本名称`LabelsBundle`开头，以`.properties`后缀结尾。但是，由于此文件适用于特定的`Locale`，因此基本名称后跟语言代码（de）。`LabelsBundle_de.properties`的内容如下：

```
# This is the LabelsBundle_de.properties file
s1 = Computer
s2 = Platte
s3 = Monitor
s4 = Tastatur
```

`PropertiesDemo` 示例程序连同下面3个属性文件一起发布：

```
LabelsBundle.properties
LabelsBundle_de.properties
LabelsBundle_fr.properties
```

**3. 指定 Locale**

`PropertiesDemo` 程序创建 `Locale` 对象如下：

```java
Locale[] supportedLocales = {
    Locale.FRENCH,
    Locale.GERMAN,
    Locale.ENGLISH
};
```

这些`Locale`对象应与前两个步骤中创建的属性文件匹配。例如，`Locale.FRENCH`对象对应于`LabelsBundle_fr.properties`文件。`Locale.ENGLISH`没有匹配的`LabelsBundle_en.properties`文件，因此将使用默认文件。

**4. 创建 ResourceBundle**

此步骤显示`Locale`，属性文件和`ResourceBundle`的关联方式。要创建`ResourceBundle`，请调用`getBundle`方法，指定基本名称和`Locale`：

```java
ResourceBundle labels = ResourceBundle.getBundle("LabelsBundle", currentLocale);
```

`getBundle`方法首先查找与基本名称和`Locale`匹配的类文件。如果找不到类文件，则检查属性文件。在`PropertiesDemo`程序中，我们使用属性文件而不是类文件来支持`ResourceBundle`。当`getBundle`方法找到正确的属性文件时，它返回一个`PropertyResourceBundle`对象，该对象包含属性文件中的键值对。

**5. 获取本地化的文本**

要从`ResourceBundle`检索已翻译的值，请按如下方式调用`getString`方法：

```java
String value = labels.getString(key);
```

`getString`返回的`String`对应于指定的键。如果存在指定区域设置的属性文件，则`String`使用正确的语言。

**6. 遍历所有的键**

此步骤是可选的。调试程序时，您可能希望获取`ResourceBundle`中所有键的值。`getKeys`方法返回`ResourceBundle`中所有键的`Enumeration`。您可以遍历`Enumeration`并使用`getString`方法获取每个值。以下代码行来自`PropertiesDemo`程序，展示了如何完成此操作：

```java
ResourceBundle labels = ResourceBundle.getBundle("LabelsBundle", currentLocale);
Enumeration bundleKeys = labels.getKeys();

while (bundleKeys.hasMoreElements()) {
    String key = (String)bundleKeys.nextElement();
    String value = labels.getString(key);
    System.out.println("key = " + key + ", " + "value = " + value);
}
```

**7. 运行示例程序**

运行`PropertiesDemo`程序会生成以下输出。前三行显示`getString`为各种`Locale`对象返回的值。当使用`getKeys`方法迭代键时，程序显示最后四行。

```
Locale = fr, key = s2, value = Disque dur
Locale = de, key = s2, value = Platte
Locale = en, key = s2, value = disk

key = s4, value = Clavier
key = s3, value = Moniteur
key = s2, value = Disque dur
key = s1, value = Ordinateur
```

