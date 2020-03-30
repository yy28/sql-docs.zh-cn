---
title: 使用表值参数 | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dfa8438e7afb1763129748368a7f6e08fa892c3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77575331"
---
# <a name="using-table-valued-parameters"></a>使用表值参数

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

表值参数提供了一将多行数据从客户端应用程序封送到 SQL Server 的种简单方法，而无需进行多次往返或特殊的服务器端逻辑来处理数据。 可使用表值参数来封装客户端应用程序中的数据行，并以单个参数化命令将数据发送到服务器。 传入数据行存储在随后可使用 Transact-SQL 进行操作的表变量中。  
  
可以使用标准的 Transact-SQL SELECT 语句来访问表值参数中的列值。 表值参数为强类型，其结构会自动进行验证。 表值参数的大小仅受服务器内存的限制。  
  
> [!NOTE]  
> 自 Microsoft JDBC Driver 6.0 for SQL Server 起，开始支持表值参数。
>
> 无法返回表值参数中的数据。 表值参数仅限输入；不支持 OUTPUT 关键字。  
  
 若要详细了解表值参数，请参阅以下资源。  
  
| 资源                                                                                                             | 说明                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server 联机丛书中的[表值参数（数据库引擎）](https://go.microsoft.com/fwlink/?LinkId=98363) | 介绍了如何创建和使用表值参数                             |
| SQL Server 联机丛书中的[用户定义的表类型](https://go.microsoft.com/fwlink/?LinkId=98364)                  | 介绍了用于声明表值参数的用户定义的表类型 |
| CodePlex 的 [Microsoft SQL Server 数据库引擎](https://go.microsoft.com/fwlink/?LinkId=120507)一节        | 收录了展示如何使用 SQL Server 特性和功能的示例  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在旧版 SQL Server 中传递多行  

在 SQL Server 2008 中引入表值参数之前，用于将多行数据传递到存储过程或参数化 SQL 命令的选项受到限制。 开发人员可以选择下面的一种方法，将多行传递到服务器：  
  
- 使用一系列单独的参数来表示多列和多行数据中的值。 使用这种方法可以传递的数据量受到允许使用的参数数量限制。 SQL Server 过程最多可以有 2100 个参数。 必须使用服务器端逻辑，将这些单独的值汇编到表变量或临时表中以供处理。  
  
- 将多个数据值绑定到分隔字符串或 XML 文档，然后将这些文本值传递到过程或语句。 这要求过程或语句包含验证数据结构和解除绑定值所需的逻辑。  
  
- 创建一系列单独的 SQL 语句，以执行影响多行的数据修改。 更改可以单独提交给服务器，也可以批量提交给组。 不过，即使是包含多个语句的批量提交，每个语句也是在服务器上单独执行。  
  
- 使用 bcp 实用工具或 [SQLServerBulkCopy](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md) 将多行数据加载到表中。 尽管这种技术非常高效，但它不支持服务器端处理，除非将数据加载到临时表或表变量中。
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  

表值参数基于使用 Transact-SQL `CREATE TYPE` 语句定义的强类型表结构。 必须先在 SQL Server 中创建一个表类型并定义结构，才能在客户端应用程序中使用表值参数。 有关创建表类型的详细信息，请参阅 SQL Server 联机丛书中的[用户定义的表类型](https://go.microsoft.com/fwlink/?LinkID=98364)。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

创建表类型后，可以根据相应类型来声明表值参数。 下面的 Transact-SQL 片段演示如何在存储过程定义中声明表值参数。 请注意，`READONLY` 是声明表值参数所必需的关键字。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用表值参数修改数据 (Transact-SQL)  

表值参数可用于基于集的数据修改，这些修改通过执行一条语句影响多行。 例如，可以选择表值参数中的所有行并将它们插入数据库表，也可以通过将表值参数联接到要更新的表来创建更新语句。  
  
下面的 Transact-SQL UPDATE 语句演示如何通过将表值参数联接到 Categories 表来使用它。 在 FROM 子句中结合使用表值参数和 JOIN 时，还必须对表值参数使用别名。如下所示，表值参数的别名为“ec”：  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

此 Transact-SQL 示例演示如何从表值参数中选择行以在单个基于集的操作中执行 INSERT。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制

表值参数有几个限制：  
  
- 不能将表值参数传递给用户定义的函数。  
  
- 表值参数只能通过被编制索引来支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护表值参数的统计信息。  
  
- 在 Transact-SQL 代码中表值参数是只读的。 既不能更新表值参数行中的列值，也不能插入或删除行。 若要修改表值参数中传递到存储过程或参数化语句的数据，必须将数据插入临时表或表变量。  
  
- 不能使用 ALTER TABLE 语句来修改表值参数的设计。

- 可以在表值参数中流式传输大型对象。  
  
## <a name="configuring-a-table-valued-parameter"></a>配置表值参数

自 Microsoft JDBC Driver 6.0 for SQL Server 起，开始支持将表值参数与参数化语句或参数化存储过程一起配合使用。 可以从 SQLServerDataTable、ResultSet 或用户提供的 ISQLServerDataRecord 接口实现填充表值参数。 如果为准备的查询设置表值参数，必须指定类型名称，此名称必须与先前在服务器上创建的兼容类型的名称一致。  
  
下面两个代码片段展示了如何使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 将表值参数配置为插入数据。 其中的 sourceTVPObject 可以是 SQLServerDataTable、ResultSet 或 ISQLServerDataRecord 对象。 这些示例假定连接是活动的 Connection 对象。  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> 有关可用于设置表值参数的 API 的完整列表，请参阅下面的“JDBC 驱动程序的表值参数 API”  部分。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>将表值参数作为 SQLServerDataTable 对象传递  

自 Microsoft JDBC Driver 6.0 for SQL Server 起，SQLServerDataTable 类开始表示关系数据的内存中表。 下面的示例展示了如何使用 SQLServerDataTable 对象从内存中数据构造表值参数。 首选，此代码创建 SQLServerDataTable 对象，定义它的架构，并使用数据填充表。 然后，此代码配置 SQLServerPreparedStatement，用于将此数据表作为表值参数传递到 SQL Server。  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> 有关可用于设置表值参数的 API 的完整列表，请参阅下面的“JDBC 驱动程序的表值参数 API”  部分。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>将表值参数作为 ResultSet 对象传递  

下面的示例展示了如何将 ResultSet 中的数据行流式传输到表值参数。 首先，代码从 SQLServerDataTable 对象中的源表中检索数据，定义它的架构，并使用数据填充表。 然后，此代码配置 SQLServerPreparedStatement，用于将此数据表作为表值参数传递到 SQL Server。  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> 有关可用于设置表值参数的 API 的完整列表，请参阅下面的“JDBC 驱动程序的表值参数 API”  部分。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>将表值参数作为 ISQLServerDataRecord 对象传递  

自 Microsoft JDBC Driver 6.0 for SQL Server 起，新接口 ISQLServerDataRecord 可用于使用表值参数流式传输数据（具体取决于用户如何实现它）。 下面的示例展示了如何实现 ISQLServerDataRecord 接口，以及如何将它作为表值参数传递。 为简单起见，下面的示例仅将包含硬编码值的一行传递给表值参数。 理想情况下，用户会实现此接口，用于流式传输任何源（例如，文本文件）中的行。  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> 有关可用于设置表值参数的 API 的完整列表，请参阅下面的“JDBC 驱动程序的表值参数 API”  部分。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 驱动程序的表值参数 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

此类表示列的元数据。 它在 ISQLServerDataRecord 接口中使用，以将列元数据传递到表值参数。 此类中的方法为：  

| 名称                                                                                                                                                                             | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 使用指定的列名、SQL 类型、精度、规模和默认服务器值初始化 SQLServerMetaData 的新实例。 这种形式的构造函数支持表值参数，具体是允许你指定列在表值参数中是否唯一、列排序顺序以及排序列序号。 <br/><br/>useServerDefault - 指定此列是否应使用默认服务器值；默认值为 false。<br>isUniqueKey - 指明表值参数中的列是否唯一；默认值为 false。<br>sortOrder - 指明列排序顺序；默认值为 SQLServerSortOrder.Unspecified。<br>sortOrdinal - 指定排序列序号；sortOrdinal 从 0 开始；默认值为 -1。 |
| public SQLServerMetaData(String columnName, int sqlType)                                                                                                                        | 使用列名和 SQL 类型初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData(String columnName, int sqlType, int length)                                                                                                                        | 使用列名、SQL 类型和长度（对于 String 数据）初始化 SQLServerMetaData 的新实例。 长度用于区分大字符串和长度短于 4000 个字符的字符串。 已在 JDBC 驱动程序版本 7.2 中引入。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale)                                                                                              | 使用列名、SQL 类型、精度和规模初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 从另一个 SQLServerMetaData 对象初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 检索列名。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | 检索 Java SQL 类型。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | 检索传递到列的类型的精度。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 检索传递到列的类型的规模。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 检索排序顺序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 检索排序序号。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 返回列是否唯一。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 返回列是否使用默认服务器值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

定义排序顺序的枚举。 可取值为 Ascending、Descending 和 Unspecified。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

此类表示要与表值参数一起使用的内存中数据表。 此类中的方法为：  

| 名称                                                          | 说明                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | 初始化 SQLServerDataTable 的新实例。    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | 检索数据表行上的迭代器。 |
| public void addColumnMetadata(String columnName, int sqlType) | 添加指定列的元数据。              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 添加指定列的元数据。              |
| public void addRow(Object... values)                          | 将一行数据添加到数据表。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | 检索此数据表的列元数据。       |
| public void clear()                                           | 清除此数据表。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

此类表示由 SQLServerDataTable 表示的内存中数据表的列。 此类中的方法为：  

| 名称                                                       | 说明                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn(String columnName, int sqlType) | 使用列名和类型初始化 SQLServerDataColumn 的新实例。 |
| public String getColumnName()                              | 检索列名。                                                       |
| public int getColumnType()                                 | 检索列类型。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

此类表示用户可以实现的接口，用于将数据流式传输到表值参数。 此接口中的方法为：  
  
| 名称                                                    | 说明                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 检索给定列索引的列元数据。                                               |
| public int getColumnCount();                            | 检索总列数。                                                                  |
| public Object[] getRowData();                           | 获取作为对象数组的当前行的数据。                                          |
| public boolean next();                                  | 移到下一行。 如果移动成功且有下一行，则返回 True，否则返回 False。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

为了支持传递表值参数，已将下面的方法添加到此类。  

| 名称                                                                                                    | 说明                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | 使用数据表填充表值参数。 parameterIndex 是参数索引，tvpName 是表值参数的名称，tvpDataTable 是源数据表对象。                                                                                                          |
| public final void setStructured(int parameterIndex, String tvpName, ResultSet tvpResultSet)             | 使用从另一个表检索到的 ResultSet 填充表值参数。 parameterIndex 是参数索引，tvpName 是表值参数的名称，tvpResultSet 是源结果集对象。                                                                               |
| public final void setStructured(int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | 使用 ISQLServerDataRecord 对象填充表值参数。 ISQLServerDataRecord 用于流式传输数据，由用户决定如何使用它。 parameterIndex 是参数索引，tvpName 是表值参数的名称，tvpDataRecord 是 ISQLServerDataRecord 对象。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

为了支持传递表值参数，已将下面的方法添加到此类。  
  
| 名称                                                                                                        | 说明                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | 使用数据表填充传递到存储过程的表值参数。 paratemeterName 是参数名称，tvpName 是类型 TVP 的名称，tvpDataTable 是数据表对象。                                                                                                                 |
| public final void setStructured(String paratemeterName, String tvpName, ResultSet tvpResultSet)             | 使用从另一个表检索到的 ResultSet 填充传递到存储过程的表值参数。 paratemeterName 是参数名称，tvpName 是类型 TVP 的名称，tvpResultSet 是源数据集对象。                                                                              |
| public final void setStructured(String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | 使用 ISQLServerDataRecord 对象填充传递到存储过程的表值参数。 ISQLServerDataRecord 用于流式传输数据，由用户决定如何使用它。 paratemeterName 是参数名称，tvpName 是类型 TVP 的名称，tvpDataRecord 是 ISQLServerDataRecord 对象。 |

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
