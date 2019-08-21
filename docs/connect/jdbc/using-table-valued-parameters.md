---
title: 使用表值参数 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98863afb5a47eddfd311563bd03a1c7c7120b161
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025709"
---
# <a name="using-table-valued-parameters"></a>使用表值参数

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

表值参数提供了一将多行数据从客户端应用程序封送到 SQL Server 的种简单方法，而无需进行多次往返或特殊的服务器端逻辑来处理数据。 可使用表值参数来封装客户端应用程序中的数据行，并以单个参数化命令将数据发送到服务器。 传入数据行存储在随后可使用 Transact-SQL 进行操作的表变量中。  
  
可以使用标准 Transact-sql SELECT 语句来访问表值参数中的列值。 表值参数为强类型, 其结构会自动进行验证。 表值参数的大小仅受服务器内存限制。  
  
> [!NOTE]  
> 从 Microsoft JDBC Driver 6.0 开始, 为 SQL Server 提供表值参数支持。
>
> 不能返回表值参数中的数据。 表值参数是只可输入的;不支持 OUTPUT 关键字。  
  
 有关表值参数的详细信息, 请参阅以下资源。  
  
| 资源                                                                                                             | 描述                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server 联机丛书中的[表值参数 (数据库引擎)](https://go.microsoft.com/fwlink/?LinkId=98363) | 介绍如何创建和使用表值参数                             |
| SQL Server 联机丛书中的[用户定义表类型](https://go.microsoft.com/fwlink/?LinkId=98364)                  | 描述用于声明表值参数的用户定义表类型 |
| CodePlex 的[Microsoft SQL Server 数据库引擎](https://go.microsoft.com/fwlink/?LinkId=120507)部分        | 包含演示如何使用 SQL Server 特性和功能的示例  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在早期版本的 SQL Server 中传递多个行  

在将表值参数引入 SQL Server 2008 之前, 将多行数据传递到存储过程或参数化 SQL 命令的选项受到限制。 开发人员可以从以下选项中进行选择, 以便将多个行传递到服务器:  
  
- 使用一系列单独参数来表示多个数据列和行中的值。 使用此方法可以传递的数据量受允许的参数数目的限制。 SQL Server 过程最多可以有2100个参数。 需要服务器端逻辑将这些各个值组合到一个表变量或临时表中进行处理。  
  
- 将多个数据值捆绑为分隔字符串或 XML 文档, 然后将这些文本值传递到过程或语句。 这要求过程或语句包括验证数据结构和 unbundling 值所需的逻辑。  
  
- 为影响多行的数据修改创建一系列单独的 SQL 语句。 可以将更改单独提交给服务器或将其成批提交到组。 但是, 即使在包含多个语句的批处理中提交, 也会在服务器上单独执行每条语句。  
  
- 使用 bcp 实用工具或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)对象将多行数据加载到表中。 尽管此方法非常有效, 但它不支持服务器端处理, 除非将数据加载到临时表或表变量中。  
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  

表值参数基于使用 transact-sql `CREATE TYPE`语句定义的强类型表结构。 在客户端应用程序中使用表值参数之前, 必须创建表类型并定义 SQL Server 中的结构。 有关创建表类型的详细信息, 请参阅 SQL Server 联机丛书中的[用户定义表类型](https://go.microsoft.com/fwlink/?LinkID=98364)。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

创建表类型后, 可以基于该类型声明表值参数。 下面的 Transact-sql 代码段演示如何在存储过程定义中声明表值参数。 请注意, `READONLY`声明表值参数需要使用关键字。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>修改包含表值参数的数据 (Transact-sql)  

通过执行单个语句, 可以在影响多行的基于集的数据修改中使用表值参数。 例如, 您可以选择表值参数中的所有行并将其插入到数据库表中, 也可以通过将表值参数联接到您要更新的表来创建 update 语句。  
  
下面的 Transact-sql UPDATE 语句演示如何通过将表值参数联接到 "类别" 表来使用它们。 在 FROM 子句中将表值参数与 JOIN 一起使用时, 还必须对其进行别名, 如下所示, 表值参数的别名为 "ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

此 Transact-sql 示例演示如何从表值参数中选择行以在单个基于集的操作中执行插入操作。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制

表值参数有几个限制:  
  
- 不能将表值参数传递给用户定义的函数。  
  
- 表值参数只能索引为支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护表值参数的统计信息。  
  
- 在 Transact-sql 代码中, 表值参数是只读的。 不能在表值参数的行中更新列值, 也不能插入或删除行。 若要在表值参数中修改传递到存储过程或参数化语句的数据, 必须将数据插入临时表或表变量中。  
  
- 不能使用 ALTER TABLE 语句来修改表值参数的设计。

- 可以在表值参数中流式传输大型对象。  
  
## <a name="configuring-a-table-valued-parameter"></a>配置表值参数

从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 参数化的语句或参数化的存储过程支持表值参数。 可以从 SQLServerDataTable、从结果集中或从用户提供的 ISQLServerDataRecord 接口实现中填充表值参数。 为已准备好的查询设置表值参数时, 必须指定类型名称, 该名称必须与先前在服务器上创建的兼容类型的名称相匹配。  
  
下面两个代码片段演示了如何使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 将表值参数配置为插入数据。 此处的 sourceTVPObject 可以是 SQLServerDataTable、ResultSet 或 ISQLServerDataRecord 对象。 这些示例假定连接是活动的连接对象。  

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
> 有关可用于设置表值参数的 Api 的完整列表, 请参阅下面**的 JDBC 驱动程序的表值参数 API**部分。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>以 SQLServerDataTable 对象的形式传递表值参数  

从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, SQLServerDataTable 类表示关系数据的内存中表。 此示例演示如何使用 SQLServerDataTable 对象从内存中数据构造表值参数。 代码首先创建一个 SQLServerDataTable 对象, 定义其架构并使用数据填充该表。 然后, 该代码将配置一个将此数据表作为表值参数传递到 SQL Server 的 SQLServerPreparedStatement。  

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
> 有关可用于设置表值参数的 Api 的完整列表, 请参阅下面**的 JDBC 驱动程序的表值参数 API**部分。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>将表值参数作为结果集对象传递  

此示例演示如何将数据集的数据行流处理到表值参数。 代码首先从源表中检索数据, 并创建 SQLServerDataTable 对象, 定义其架构并使用数据填充该表。 然后, 该代码将配置一个将此数据表作为表值参数传递到 SQL Server 的 SQLServerPreparedStatement。  

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
> 有关可用于设置表值参数的 Api 的完整列表, 请参阅下面**的 JDBC 驱动程序的表值参数 API**部分。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>以 ISQLServerDataRecord 对象的形式传递表值参数  

从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 使用表值参数, 可以使用新的接口 ISQLServerDataRecord 来处理数据 (取决于用户为其提供实现的方式)。 下面的示例演示如何实现 ISQLServerDataRecord 接口, 以及如何将其作为表值参数进行传递。 为简单起见, 下面的示例只向表值参数传递一个包含硬编码值的行。 理想情况下, 用户将实现此接口, 以便从任何源 (例如, 文本文件) 对行进行流式处理。  

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
> 有关可用于设置表值参数的 Api 的完整列表, 请参阅下面**的 JDBC 驱动程序的表值参数 API**部分。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 驱动程序的表值参数 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

此类表示列的元数据。 它在 ISQLServerDataRecord 接口中用于将列元数据传递给表值参数。 此类中的方法是:  

| “属性”                                                                                                                                                                             | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData (String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 使用指定的列名称、sql 类型、精度、小数位数和服务器默认值初始化 SQLServerMetaData 的新实例。 这种形式的构造函数通过允许您指定列在表值参数中是唯一的、列的排序顺序以及排序列的序号, 来支持表值参数。 <br/><br/>useServerDefault-指定此列是否应使用默认服务器值;默认值为 false。<br>isUniqueKey-指示表值参数中的列是否唯一;默认值为 false。<br>sortOrder-指示列的排序顺序;默认值为 SQLServerSortOrder。<br>sortOrdinal-指定排序列的序号;sortOrdinal 从0开始;默认值为-1。 |
| public SQLServerMetaData (String columnName, int sqlType)                                                                                                                        | 使用列名称和 sql 类型初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData (String columnName, int sqlType, int length)                                                                                                                        | 使用列名称、sql 类型和长度 (对于字符串数据) 初始化 SQLServerMetaData 的新实例。 长度用于区分字符串长度小于4000个字符的字符串。 在 JDBC 驱动程序的7.2 版中引入。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData (String columnName, int sqlType, int precision, int scale)                                                                                              | 使用列名称、sql 类型、精度和小数位数初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 从另一个 SQLServerMetaData 对象初始化 SQLServerMetaData 的新实例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 检索列名。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | 检索 java sql 类型。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision ()                                                                                                                                                        | 检索传递到列的类型的精度。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 检索传递到列的类型的小数位数。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 检索排序顺序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 检索排序序号。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 返回列是否唯一。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 返回列是否使用默认服务器值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

定义排序顺序的枚举。 可能的值包括升序、降序和未指定。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

此类表示要用于表值参数的内存中数据表。 此类中的方法是:  

| “属性”                                                          | 描述                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | 初始化 SQLServerDataTable 的新实例。    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | 检索数据表中的行的迭代器。 |
| public void addColumnMetadata(String columnName, int sqlType) | 为指定列添加元数据。              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 为指定列添加元数据。              |
| public void addRow (对象 .。。分隔                          | 将一行数据添加到数据表。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | 检索此数据表的列元数据。       |
| public void clear()                                           | 清除此数据表。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

此类表示 SQLServerDataTable 所表示的内存中数据表的列。 此类中的方法是:  

| “属性”                                                       | 描述                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn (String columnName, int sqlType) | 使用列名称和类型初始化 SQLServerDataColumn 的新实例。 |
| public String getColumnName()                              | 检索列名。                                                       |
| public int getColumnType()                                 | 检索列类型。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

此类表示一个接口, 用户可以实现该接口以将数据流式传输到表值参数。 此接口中的方法为:  
  
| “属性”                                                    | 描述                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 检索给定列索引的列元数据。                                               |
| public int getColumnCount();                            | 检索总列数。                                                                  |
| public Object[] getRowData();                           | 获取作为对象数组的当前行的数据。                                          |
| public boolean next();                                  | 移到下一行。 如果移动成功并且有下一行, 则返回 True, 否则返回 false。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

已将以下方法添加到此类, 以支持传递表值参数。  

| “属性”                                                                                                    | 描述                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured (int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | 使用数据表填充表值参数。 parameterIndex 是参数索引, tvpName 是表值参数的名称, 而 tvpDataTable 是源数据表对象。                                                                                                          |
| public final void setStructured (int parameterIndex, String tvpName, ResultSet tvpResultSet)             | 使用从另一个表检索到的结果集填充表值参数。 parameterIndex 是参数索引, tvpName 是表值参数的名称, tvpResultSet 为源结果集对象。                                                                               |
| public final void setStructured (int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | 使用 ISQLServerDataRecord 对象填充表值参数。 ISQLServerDataRecord 用于流式传输数据, 用户决定如何使用它。 parameterIndex 是参数索引, tvpName 是表值参数的名称, 而 tvpDataRecord 是 ISQLServerDataRecord 对象。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

已将以下方法添加到此类, 以支持传递表值参数。  
  
| “属性”                                                                                                        | 描述                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured (String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | 使用数据表填充传递到存储过程的表值参数。 paratemeterName 是参数的名称, tvpName 是 TVP 类型的名称, tvpDataTable 是数据表对象。                                                                                                                 |
| public final void setStructured (String paratemeterName, String tvpName, ResultSet tvpResultSet)             | 使用从另一个表检索到的结果集来填充传递到存储过程的表值参数。 paratemeterName 是参数的名称, tvpName 是 TVP 类型的名称, tvpResultSet 是源结果集对象。                                                                              |
| public final void setStructured (String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | 使用 ISQLServerDataRecord 对象填充传递到存储过程的表值参数。 ISQLServerDataRecord 用于流式传输数据, 用户决定如何使用它。 paratemeterName 是参数的名称, tvpName 是 TVP 类型的名称, tvpDataRecord 是 ISQLServerDataRecord 对象。 |

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
