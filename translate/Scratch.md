### 将JDBC与GUI API结合使用

示例`CoffeesFrame.java`演示了如何将JDBC与GUI API集成，特别是Swing API。它在表中显示`COFFEES`数据库表的内容，并包含允许您向表中添加行的字段和按钮。以下是此示例的屏幕截图：

![Screenshot of Sample CoffeeFrames.java](https://docs.oracle.com/javase/tutorial/figures/jdbc/coffeesframe.gif)

该示例包含五个文本字段，这些字段对应于`COFFEES`表中的每个列。它还包含三个按钮：

 - **向表中添加行**：根据在文本字段中输入的数据向样本表中添加行。
 - **更新数据库**：根据样本表中的数据更新表`COFFEES`。
 - **放弃更改**：检索`COFFEES`表的内容，替换样本表中的现有数据。

此示例（需要`CoffeesTableModel`）演示了将JDBC与Swing API集成的以下常规步骤：

1. 实现`TableModel`接口
2. 实现`RowSetListener`接口
3. 布置Swing组件
4. 为示例中的按钮添加监听器

**实现 `javax.swing.event.TableModel` 接口**

`TableModel`接口使Java Swing应用程序能够管理`JTable`对象中的数据。示例`CoffeesTableModel.java`实现了此接口。它指定`JTable`对象应如何从`RowSet`对象检索数据并将其显示在表中。

**注意：**尽管此示例在Swing应用程序中显示`COFFEES`表的内容，但`CoffeesTableModel`类应适用于任何SQL表，前提是其数据可以使用String对象表示。（但是，必须为其他SQL表修改允许用户向`COFFEES`添加行的字段，这些字段在`CoffeesFrame`类中指定。）

在实现接口`TableModel`的方法之前，`CoffeeTableModel`类的构造函数初始化这些实现的方法所需的各种成员变量，如下所示：

```java
public CoffeesTableModel(CachedRowSet rowSetArg)
    throws SQLException {

    this.coffeesRowSet = rowSetArg;
    this.metadata = this.coffeesRowSet.getMetaData();
    numcols = metadata.getColumnCount();

    // Retrieve the number of rows.
    this.coffeesRowSet.beforeFirst();
    this.numrows = 0;
    while (this.coffeesRowSet.next()) {
        this.numrows++;
    }
    this.coffeesRowSet.beforeFirst();
}
```

下面描述了在此构造函数中初始化的成员变量：

 -  `CachedRowSet coffeesRowSet`：存储表`COFFEES`的内容。
     此示例使用`RowSet`对象，特别是`CachedRowSet`对象，而不是`ResultSet`对象，原因有两个。`CachedRowSet`对象使应用程序的用户可以更改其中包含的数据，而无需连接到数据库。此外，由于`CachedRowSet`对象是JavaBeans组件，因此它可以在发生某些事件时通知其他组件。在此示例中，当新行添加到`CachedRowSet`对象时，它会通知正在表中呈现其数据的Swing组件以刷新自身并显示新行。
 -  `ResultSetMetaData`元数据：检索表`COFFEES`中的列数以及每个列的名称。
 -  `int numcols, numrows`：分别在表`COFFEES`中存储列数和行数。

`CoffeesTableModel.java`示例从`TableModel`接口实现以下方法：

 -  `Class <?> getColumnClass(int columnIndex)`：返回列中所有单元格值的最具体的超类。
 -  `int getColumnCount()`：返回模型中的列数。
 -  `String getColumnName(int columnIndex)`：返回参数`columnIndex`指定的列的名称。
 -  `int getRowCount()`：返回模型中的行数。
 -  `Object getValueAt(int rowIndex, int columnIndex)`：返回列`columnIndex`和行`rowIndex`的交集处的单元格的值。
 -  `boolean isCellEditable(int rowIndex, int columnIndex)`：如果可以编辑`rowIndex`列和行`columnIndex`的交集处的单元格，则返回`true`。

以下方法尚未实现，因为此示例不允许用户直接编辑表的内容：

 -  `void addTableModelListener(TableModelListener l)`：向每次发生数据模型更改时通知的列表添加监听器。
 -  `void removeTableModelListener(TableModelListener l)`：从每次发生数据模型更改时通知的列表中删除监听器。
 -  `void setValueAt(Object aValue, int rowIndex, int columnIndex)`：将列`columnIndex`与行`rowIndex`的交集处的单元格中的值设置为对象`aValue`。

**实现 `getColumnCount` 和 `getRowCount`**

方法`getColumnCount`和`getRowCount`分别返回成员变量`numcols`和`numrows`的值：

```java
public int getColumnCount() {
    return numcols;
}

public int getRowCount() {
    return numrows;
}
```

**实现 `getColumnClass`**

`getColumnClass`方法返回指定列的数据类型。为简单起见，此方法返回`String`类，从而将表中的所有数据转换为`String`对象。`JTable`类使用此方法确定如何在GUI应用程序中呈现数据。

```java
public Class getColumnClass(int column) {
    return String.class;
}
```

**实现 `getColumnName`**

`getColumnName`方法返回指定列的名称。`JTable`类使用此方法标记其每个列。

```java
public String getColumnName(int column) {
    try {
        return this.metadata.getColumnLabel(column + 1);
    } catch (SQLException e) {
        return e.toString();
    }
}
```

**实现 `getColumnAt`**

`getColumnAt`方法检索行集`coffeesRowSet`中指定行和列的值。`JTable`类使用此方法填充其表。请注意，SQL开始将其行和列编号为1，但`TableModel`接口从0开始；这就是为什么`rowIndex`和`columnIndex`值增加1的原因。

```java
public Object getValueAt(int rowIndex, int columnIndex) {

    try {
        this.coffeesRowSet.absolute(rowIndex + 1);
        Object o = this.coffeesRowSet.getObject(columnIndex + 1);
        if (o == null)
            return null;
        else
            return o.toString();
    } catch (SQLException e) {
        return e.toString();
    }
}
```

**实现 `isCellEditable`**

因为此示例不允许用户直接编辑表的内容（行由另一个窗口控件添加），所以无论`rowIndex`和`columnIndex`的值如何，此方法都返回`false`：

```java
public boolean isCellEditable(int rowIndex, int columnIndex) {
    return false;
}
```

**实现 `javax.sql.RowSetListener`**

类`CoffeesFrame`只从接口`RowSetListener`实现一个方法，`rowChanged`。当用户向表中添加行时，将调用此方法。

```java
public void rowChanged(RowSetEvent event) {

    CachedRowSet currentRowSet =
        this.myCoffeesTableModel.coffeesRowSet;

    try {
        currentRowSet.moveToCurrentRow();
        myCoffeesTableModel = new CoffeesTableModel(
            myCoffeesTableModel.getCoffeesRowSet());
        table.setModel(myCoffeesTableModel);

    } catch (SQLException ex) {

        JDBCTutorialUtilities.printSQLException(ex);

        // Display the error in a dialog box.

        JOptionPane.showMessageDialog(
            CoffeesFrame.this,
            new String[] {
                // Display a 2-line message
                ex.getClass().getName() + ": ",
                ex.getMessage()
            }
        );
    }
}
```

此方法更新GUI应用程序中的表。

**布置 Swing 组件**

`CoffeesFrame`类的构造函数初始化并布置Swing组件。以下语句检索`COFFEES`表的内容，将内容存储在`CachedRowSet`对象`myCachedRowSet`中，并初始化`JTable` Swing组件：

```java
CachedRowSet myCachedRowSet = getContentsOfCoffeesTable();
myCoffeesTableModel = new CoffeesTableModel(myCachedRowSet);
myCoffeesTableModel.addEventHandlersToRowSet(this);

// Displays the table   
table = new JTable(); 
table.setModel(myCoffeesTableModel);
```

如前所述，此示例使用`RowSet`对象（尤其是`CachedRowSet`对象）而不是`ResultSet`对象来表示`COFFEES`表的内容。

方法`CoffeesFrame.getContentsOfCoffeesTable`检索表`COFFEES`的内容。

方法`CoffeesTableModel.addEventHandlersToRowSet`将`CoffeesFrame`类中定义的事件处理程序（方法`rowChanged`）添加到行集成员变量`CoffeesTableModel.coffeesRowSet`。这使得类`CoffeesFrame`能够通知任何事件的行集`coffeesRowSet`，特别是当用户单击“将行添加到表”，“更新数据库”或“放弃更改”按钮时。当行集`coffeesRowSet`被通知其中一个更改时，将调用方法`CoffeesFrame.rowChanged`。

语句`table.setModel`（`myCoffeesTableModel`）指定它使用`CoffeesTableModel`对象`myCoffeesTableModel`来填充`JTable` Swing组件表。

以下语句指定`CoffeesFrame`类使用布局`GridBagLayout`来布局其Swing组件：

```java
Container contentPane = getContentPane();
contentPane.setComponentOrientation(
    ComponentOrientation.LEFT_TO_RIGHT);
contentPane.setLayout(new GridBagLayout());
GridBagConstraints c = new GridBagConstraints();
```

有关使用布局`GridBagLayout`的更多信息，请参见 [Creating a GUI With JFC/Swing](https://docs.oracle.com/javase/tutorial/uiswing/index.html)  中的 [How to Use GridBagLayout](https://docs.oracle.com/javase/tutorial/uiswing/layout/gridbag.html) 。

请参阅`CoffeesFrame.java`的源代码，以了解如何将此示例的Swing组件添加到布局`GridBagLayout`中。

**为按钮添加监听器**

以下语句将一个监听器添加到“向表中添加行”按钮：

```java
button_ADD_ROW.addActionListener(
    new ActionListener() {
      
    public void actionPerformed(ActionEvent e) {

        JOptionPane.showMessageDialog(
            CoffeesFrame.this, new String[] {
                "Adding the following row:",
                "Coffee name: [" +
                textField_COF_NAME.getText() +
                "]",
                "Supplier ID: [" +
                textField_SUP_ID.getText() + "]",
                "Price: [" +
                textField_PRICE.getText() + "]",
                "Sales: [" +
                textField_SALES.getText() + "]",
                "Total: [" +
                textField_TOTAL.getText() + "]"
            }
        );

        try {
            myCoffeesTableModel.insertRow(
                textField_COF_NAME.getText(),
                Integer.parseInt(textField_SUP_ID.getText().trim()),
                Float.parseFloat(textField_PRICE.getText().trim()),
                Integer.parseInt(textField_SALES.getText().trim()),
                Integer.parseInt(textField_TOTAL.getText().trim())
            );
        } catch (SQLException sqle) {
            displaySQLExceptionDialog(sqle);
        }
    }
});
```

当用户单击此按钮时，它将执行以下操作：

 - 创建一个消息对话框，显示要添加到表中的行。
 - 调用方法`CoffeesTableModel.insertRow`，它将行添加到成员变量`CoffeesTableModel.coffeesRowSet`。

如果抛出`SQLException`，则方法`CoffeesFrame.displaySQLExceptionDialog`将创建一个消息对话框，显示`SQLException`的内容。

以下语句将一个监听器添加到“更新数据库“按钮：

```java
button_UPDATE_DATABASE.addActionListener(
    new ActionListener() {
        public void actionPerformed(ActionEvent e) {
            try {
                myCoffeesTableModel.coffeesRowSet.acceptChanges();
                msgline.setText("Updated database");
            } catch (SQLException sqle) {
                displaySQLExceptionDialog(sqle);
                // Now revert back changes
                try {
                    createNewTableModel();
                    msgline.setText("Discarded changes");
                } catch (SQLException sqle2) {
                    displaySQLExceptionDialog(sqle2);
                }
            }
        }
    }
);
```

当用户单击此按钮时，将使用行集`myCoffeesTableModel.coffeesRowSet`的内容更新表`COFFEES`。

以下语句为”撤销修改“按钮添加了一个监听器：

```java
button_DISCARD_CHANGES.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        try {
            createNewTableModel();
        } catch (SQLException sqle) {
            displaySQLExceptionDialog(sqle);
        }
    }
});
```

当用户单击此按钮时，将调用方法`CoffeesFrame.createNewTableModel`，该方法使用`COFFEES`表的内容重新填充`JTable`组件。

