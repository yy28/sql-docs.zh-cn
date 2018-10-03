---
title: 使用表值参数 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 134b5eef527b375e9107149ead9d55ab08933363
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598385"
---
# <a name="using-table-valued-parameters"></a>使用表值参数

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

表值参数提供了一将多行数据从客户端应用程序封送到 SQL Server 的种简单方法，而无需进行多次往返或特殊的服务器端逻辑来处理数据。 可使用表值参数来封装客户端应用程序中的数据行，并以单个参数化命令将数据发送到服务器。 然后可以操作通过使用 TRANSACT-SQL 在表变量中存储传入的数据行。  
  
可使用标准 TRANSACT-SQL SELECT 语句访问表值参数中的列值。 表值参数为强类型，其结构会自动验证。 表值参数的大小仅受服务器内存。  
  
> [!NOTE]  
> 可从 Microsoft JDBC Driver 6.0 for SQL Server 开始对表值参数的支持。
>
> 您无法在表值参数中返回数据。 表值参数是只;不支持 OUTPUT 关键字。  
  
 有关表值参数的详细信息，请参阅以下资源。  
  
| 资源                                                                                                             | 描述                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [表值参数 （数据库引擎）](http://go.microsoft.com/fwlink/?LinkId=98363) SQL Server 联机丛书中 | 介绍如何创建和使用表值参数                             |
| [用户定义表类型](http://go.microsoft.com/fwlink/?LinkId=98364)SQL Server 联机丛书中                  | 说明用于声明表值参数的用户定义表类型 |
| [Microsoft SQL Server 数据库引擎](http://go.microsoft.com/fwlink/?LinkId=120507)CodePlex 部分        | 包含演示如何使用 SQL Server 特征和功能的示例  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>将多个行传递给在以前版本的 SQL Server 中  

到 SQL Server 2008 引入了表值参数之前，用于将多行数据传递到存储的过程或参数化的 SQL 命令的选项受到限制。 开发人员可以选择从以下选项用于将多个行传递到服务器：  
  
- 使用一系列的每个参数来表示多个列和行数据中的值。 可以通过使用此方法传递的数据量受允许的参数的数目。 最多，SQL Server 过程可以有 2100年参数。 服务器端逻辑时需要这些单个值组合为一个表变量或临时表以进行处理。  
  
- 多个数据值捆绑到分隔的字符串或 XML 文档，然后将这些文本值传递给过程或语句。 这要求过程或语句以包括用于验证的数据结构和取消捆绑所需的逻辑值。  
  
- 创建一系列的单个 SQL 语句影响多个行的数据修改。 可以单独提交到服务器或组进行批处理的更改。 但是，即使在包含多个语句的批处理中提交，每个语句是单独在服务器上执行。  
  
- 使用 bcp 实用程序或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)对象加载到表中的很多行数据。 尽管这项技术非常有效，但它不支持服务器端处理，除非将数据加载到临时表或表变量。  
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  

使用 TRANSACT-SQL 定义的强类型表结构为基础表值参数`CREATE TYPE`语句。 您必须创建一个表类型和 SQL Server 中定义的结构，然后才能在客户端应用程序中使用表值参数。 有关创建表类型的详细信息，请参阅[用户定义表类型](http://go.microsoft.com/fwlink/?LinkID=98364)SQL Server 联机丛书中。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

在创建后的表类型，可以声明该类型所基于的表值参数。 下面的 TRANSACT-SQL 片段演示如何声明中的存储的过程定义的表值参数。 请注意，`READONLY`关键字是所必需的声明表值参数。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用表值参数 (Transact SQL) 修改数据  

可以通过执行一条语句影响多个行的基于集的数据修改中使用表值参数。 例如，可以选择的表值参数中的所有行并将它们插入到数据库表，或者可以通过将表值参数联接到想要更新的表创建的 update 语句。  
  
下面的 TRANSACT-SQL UPDATE 语句演示如何通过将其联接到 Categories 表使用表值参数。 与 FROM 子句中的联接使用表值参数时，您必须还别名，如下所示，其中表值参数的别名为"ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

此 TRANSACT-SQL 示例演示如何从表值参数以在单个基于集的操作中执行 INSERT 中选择行。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制

有表值参数的几个限制：  
  
- 不能将表值参数传递给用户定义的函数。  
  
- 表值参数仅可编制索引以支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护表值参数的统计信息。  
  
- 表值参数是在 TRANSACT-SQL 代码中以只读的。 无法更新中的表值参数行的列值并不能插入或删除行。 若要修改传递给存储过程或参数化语句表值参数中的数据，您必须将数据插入到临时表或表变量。  
  
- 不能使用 ALTER TABLE 语句来修改表值参数的设计。

- 您可以流式表值参数中的大型对象。  
  
## <a name="configuring-a-table-valued-parameter"></a>配置表值参数

从 Microsoft JDBC Driver 6.0 for SQL Server，使用参数化的语句或参数化存储的过程支持表值参数。 表值参数可以是从 SQLServerDataTable，从结果集填充或从用户提供 ISQLServerDataRecord 接口的实现。 设置已准备的查询的表值参数，必须指定类型名称必须匹配先前创建的服务器上的兼容类型的名称。  
  
以下两个代码片段演示了如何配置使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 以插入数据的表值参数。 此处 sourceTVPObject 可以 SQLServerDataTable 或结果集或 ISQLServerDataRecord 对象。 这些示例假定连接是活动的连接对象。  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
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
> 请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>将表值参数传递作为 SQLServerDataTable 对象  

从 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerDataTable 类表示一个内存中表的关系数据。 此示例演示如何构造使用 SQLServerDataTable 对象的内存中数据的表值参数。 代码首先创建一个 SQLServerDataTable 对象、 定义其架构和使用数据填充表。 然后，代码配置 SQLServerPreparedStatement 将该表的数据作为表值参数传递到 SQL Server。  

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
> 请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>将表值参数传递作为结果集对象  

此示例演示如何将流式传输的数据从一个结果集复制到表值参数行。 代码首先从源表中检索数据创建 SQLServerDataTable 对象，将定义其架构以及使用数据填充表。 然后，代码配置 SQLServerPreparedStatement 将该表的数据作为表值参数传递到 SQL Server。  

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
> 请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>将表值参数传递作为 ISQLServerDataRecord 对象  

从 Microsoft JDBC Driver 6.0 for SQL Server，新界面 ISQLServerDataRecord 是可用于流式处理数据 （具体取决于如何用户提供它的实现） 使用表值参数。 下面的示例演示如何实现 ISQLServerDataRecord 接口以及如何将其作为表值参数传递。 为简单起见，下面的示例将只是一个具有硬编码值的行传递给表值参数。 理想情况下，用户可以实现此接口行流处理从任何源，例如从文本文件。  

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
> 请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 驱动程序的表值参数 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

此类表示列的元数据。 它使用 ISQLServerDataRecord 界面中将传递给表值参数列元数据。 此类中的方法是：  

| “属性”                                                                                                                                                                             | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公共 SQLServerMetaData （字符串 columnName、 int sqlType、 int 精度、 int 规模、 布尔 useServerDefault、 布尔 isUniqueKey、 SQLServerSortOrder sortOrder、 int sortOrdinal） | 初始化使用指定的列名称、 sql 类型、 精度、 小数位数和服务器默认 SQLServerMetaData 的新实例。 这种形式的构造函数通过允许您指定的列是否在表值参数、 列和排序列的序号的排序顺序中是唯一支持表值参数。 <br/><br/>useServerDefault-指定此列是否应使用默认服务器值;默认值为 false。<br>isUniqueKey-指示表值参数中的列是唯一的;默认值为 false。<br>sortOrder-指示排序顺序的列;默认值为 SQLServerSortOrder.Unspecified。<br>sortOrdinal-指定序号的列排序;从 0; sortOrdinal 开始默认值为-1。 |
| 公共 SQLServerMetaData （字符串 columnName，int sqlType）                                                                                                                        | 初始化 SQLServerMetaData 使用列名称和 sql 类型的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 公共 SQLServerMetaData （字符串 columnName，int sqlType、 int 精度，int 规模）                                                                                              | 初始化 SQLServerMetaData 使用列名称、 sql 类型、 精度和小数位数的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 公共 SQLServerMetaData (SQLServerMetaData sqlServerMetaData)                                                                                                                    | 初始化 SQLServerMetaData 从另一个 SQLServerMetaData 对象的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 公共字符串 getColumName()                                                                                                                                                     | 检索的列名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 公共 int getSqlType()                                                                                                                                                          | 检索 java sql 类型。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 公共 int getPrecision()                                                                                                                                                        | 检索传递给列的类型的精度。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 公共 int getScale()                                                                                                                                                            | 检索传递给列的类型的小数位数。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 公共 SQLServerSortOrder getSortOrder()                                                                                                                                         | 检索排序顺序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 公共 int getSortOrdinal()                                                                                                                                                      | 检索排序序号。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 公共布尔 isUniqueKey()                                                                                                                                                     | 返回列是否唯一。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 公共布尔 useServerDefault()                                                                                                                                                | 返回列使用的默认服务器值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

一个枚举值，定义排序顺序。 可能的值为升序、 降序和未指定。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

此类表示一个内存中数据表与表值参数一起使用。 此类中的方法是：  

| “属性”                                                          | 描述                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| 公共 SQLServerDataTable()                                   | 初始化 SQLServerDataTable 的新实例。    |
| 公共迭代器 < 条目\<整数，Object [] >> getIterator()      | 检索数据的表的行上的迭代器。 |
| public void addColumnMetadata （字符串 columnName，int sqlType） | 添加指定的列的元数据。              |
| public void addColumnMetadata （SQLServerDataColumn 列）     | 添加指定的列的元数据。              |
| public void addRow （对象...值）                          | 将一个数据行添加到数据表。              |
| 公共映射\<整数、 SQLServerDataColumn > getColumnMetadata() | 检索此数据的表的列元数据。       |
| public void clear （)                                           | 清除此数据表。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

此类表示 SQLServerDataTable 所代表的内存中数据表格的列。 此类中的方法是：  

| “属性”                                                       | 描述                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| 公共 SQLServerDataColumn （字符串 columnName，int sqlType） | 初始化 SQLServerDataColumn 具有列名称和类型的新实例。 |
| 公共字符串 getColumnName()                              | 检索的列名称。                                                       |
| 公共 int getColumnType()                                 | 检索的列类型。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

此类表示用户可将流数据到表值参数来实现的接口。 在此接口的方法是：  
  
| “属性”                                                    | 描述                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 公共 SQLServerMetaData getColumnMetaData （int 列）; | 检索给定的列索引的列元数据。                                               |
| 公共 int getColumnCount();                            | 检索的总列数。                                                                  |
| 公共对象 [] getRowData();                           | 获取作为对象数组的当前行的数据。                                          |
| 公共布尔 next （);                                  | 移动到下一行。 如果移动成功且否则没有下一个行，false，则返回 True。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

将以下方法已添加到此类，以支持表值参数传递。  

| “属性”                                                                                                    | 描述                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公共最终 void setStructured （int parameterIndex，字符串 tvpName，SQLServerDataTable tvpDataTbale）    | 填充数据表的表值参数。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpDataTable 是源数据的表对象。                                                                                                          |
| 公共最终 void setStructured （int parameterIndex，字符串 tvpName，结果集 tvpResultSet）             | 使用从其他表中检索一个结果集填充表值参数。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpResultSet 是源结果集对象。                                                                               |
| 公共最终 void setStructured （int parameterIndex，字符串 tvpName，ISQLServerDataRecord tvpDataRecord） | 填充表值参数与 ISQLServerDataRecord 对象。 ISQLServerDataRecord 用于流式处理数据，并且用户决定如何使用它。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpDataRecord 是 ISQLServerDataRecord 对象。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

将以下方法已添加到此类，以支持表值参数传递。  
  
| “属性”                                                                                                        | 描述                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公共最终 void setStructured （字符串 paratemeterName，字符串 tvpName，SQLServerDataTable tvpDataTable）    | 填充表值参数传递给带数据的表的存储过程。 paratemeterName 是参数的名称、 tvpName 是 TVP，该类型的名称和 tvpDataTable 是数据的表对象。                                                                                                                 |
| 公共最终 void setStructured （字符串 paratemeterName，字符串 tvpName，结果集 tvpResultSet）             | 填充表值参数传递给存储过程与从另一个表中检索到的结果集。 paratemeterName 是参数的名称、 tvpName 是 TVP，该类型的名称和 tvpResultSet 是源结果集对象。                                                                              |
| 公共最终 void setStructured （字符串 paratemeterName，字符串 tvpName，ISQLServerDataRecord tvpDataRecord） | 填充表值参数传递给存储过程与 ISQLServerDataRecord 对象。 ISQLServerDataRecord 用于流式处理数据，并且用户决定如何使用它。 paratemeterName 是参数的名称、 tvpName 是 TVP，该类型的名称和 tvpDataRecord 是 ISQLServerDataRecord 对象。 |

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
