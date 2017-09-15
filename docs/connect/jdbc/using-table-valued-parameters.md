---
title: "使用表值参数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91777796843557cf6c5e6f7667994d7743b608a0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-table-valued-parameters"></a>使用表值参数
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  表值参数提供的数据从客户端应用程序到 SQL Server 的多个行封送而无需多次往返或特殊服务器端逻辑来处理数据的简单办法。 表值参数可用于封装客户端应用程序中的数据行并将数据发送到单个参数化命令中的服务器。 可以随后会作用于通过使用 TRANSACT-SQL 的表变量中存储的传入数据行。  
  
 可以使用标准 TRANSACT-SQL SELECT 语句访问表值参数中的列值。 表值参数为强类型，其结构会自动进行验证。 表值参数的大小仅受服务器内存。  
  
> [!NOTE]  
>  支持表值参数是从 SQL Server 的 Microsoft JDBC Driver 6.0 开始提供。  
  
> [!NOTE]  
>  你无法在表值参数中返回数据。 表值参数是只;不支持 OUTPUT 关键字。  
  
 有关表值参数的详细信息，请参阅以下资源。  
  
|资源|Description|  
|--------------|-----------------|  
|[表值参数 （数据库引擎）](http://go.microsoft.com/fwlink/?LinkId=98363) SQL Server 联机丛书中|描述如何创建和使用表值参数|  
|[用户定义的表类型](http://go.microsoft.com/fwlink/?LinkId=98364)SQL Server 联机丛书中|介绍用于声明表值参数的用户定义表类型|  
|[Microsoft SQL Server 数据库引擎](http://go.microsoft.com/fwlink/?LinkId=120507)CodePlex 部分|包含演示如何使用 SQL Server 特性和功能的示例|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>将多个行传递给在以前版本的 SQL Server  
 表值参数中引入的 SQL Server 2008 之前，将多行数据传递到存储的过程或参数化的 SQL 命令的选项受到限制。 开发人员可以选择将多个行传递到服务器的以下选项：  
  
-   使用一系列单个参数来表示多个列和行数据中的值。 可以使用此方法传递的数据量受允许的参数的数目限制。 最多，SQL Server 过程可以有 2100 个参数。 服务器端逻辑时需要将这些单个值组合为表变量或临时表以进行处理。  
  
-   将多个数据值捆绑到分隔的字符串或 XML 文档，然后将这些文本值传递给过程或语句。 这要求的过程或语句以包含用于验证数据结构和取消捆绑所需的逻辑值。  
  
-   创建一系列的影响多个行的数据修改的单个 SQL 语句。 可将更改单独提交到服务器或组进行批处理。 但是，即使在包含多个语句的批次中提交，每个语句是单独服务器上执行。  
  
-   使用 bcp 实用程序或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)对象加载到表的很多行数据。 尽管这项技术非常高效，但它不支持服务器端处理，除非数据加载到临时表或表变量。  
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  
 表值参数基于使用 TRANSACT-SQL CREATE TYPE 语句定义的强类型表结构。 你必须创建一个表类型和 SQL Server 定义的结构，然后才能在客户端应用程序中使用表值参数。 有关创建表类型的详细信息，请参阅[用户定义表类型](http://go.microsoft.com/fwlink/?LinkID=98364)SQL Server 联机丛书中。  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 在创建后的表类型，您可以声明该类型所基于的表值参数。 以下 TRANSACT-SQL 片段演示了如何声明在存储的过程定义中的表值参数。 请注意，READONLY 关键字用于声明表值参数需要。  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用表值参数 (Transact SQL) 修改数据  
 可以通过执行单个语句影响多个行的基于集的数据修改中使用表值参数。 例如，你可以选择的表值参数中的所有行并将其插入到数据库表，或者可以通过将表值参数联接到要更新的表创建更新语句。  
  
 以下 TRANSACT-SQL UPDATE 语句演示如何通过将其联接到类别表中使用表值参数。 当与 FROM 子句中的联接使用表值参数时，你必须还别名，如下所示，其中的表值参数的别名为"ec":  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 此 TRANSACT-SQL 示例演示如何从用于在单个基于集的操作中执行插入的表值参数中选择行。  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制  
 有几个限制于表值参数：  
  
-   无法将表值参数传递给用户定义函数。  
  
-   表值参数仅可以建立索引以便支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护表值参数的统计信息。  
  
-   表值参数是在 TRANSACT-SQL 代码中以只读的。 无法更新中的表值参数行的列值和无法插入或删除行。 若要修改传递给存储过程或参数化语句表值参数中的数据，必须将数据插入到临时表或表变量。  
  
-   ALTER TABLE 语句不能用于修改表值参数的设计。
-   你可以将流表值参数中的大型对象。  
  
## <a name="configuring-a-table-valued-parameter"></a>配置表值参数  
 从 SQL Server 的 Microsoft JDBC Driver 6.0，使用参数化的语句或参数化的存储的过程支持表值参数。 可以从 SQLServerDataTable，从了结果集填充表值参数，或将其从用户提供 ISQLServerDataRecord 接口的实现。 设置已准备的查询的表值参数，你必须指定必须与以前在服务器上创建具有兼容类型的名称匹配的类型名称。  
  
 下面的两个代码段演示如何使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 以插入数据与配置的表值参数。 此处 sourceTVPObject 可以 SQLServerDataTable 或了结果集或 ISQLServerDataRecord 对象。 这些示例假定连接是一个活动的连接对象。  
  
```  
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```  
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>将表值参数传递作为 SQLServerDataTable 对象  
 从 SQL Server 的 Microsoft JDBC Driver 6.0，SQLServerDataTable 类表示一个内存中表的关系数据。 此示例演示如何构造使用 SQLServerDataTable 对象的内存中数据的表值参数。 代码首先创建 SQLServerDataTable 对象，定义其架构，并且用数据填充表。 然后，代码将配置将此数据表作为表值参数传递到 SQL Server SQLServerPreparedStatement。  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>将表值参数传递作为结果集对象  
 此示例演示如何进行流式处理的数据从了结果集复制到的表值参数行。 此代码首先检索数据的源表中创建 SQLServerDataTable 对象，定义其架构，并且填充具有数据的表。 然后，代码将配置将此数据表作为表值参数传递到 SQL Server SQLServerPreparedStatement。  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>将表值参数传递为 ISQLServerDataRecord 对象  
 从 SQL Server 的 Microsoft JDBC Driver 6.0，新接口 ISQLServerDataRecord 是可用于流式处理 （具体取决于如何用户提供实现的示例） 的数据使用表值参数。 下面的示例演示如何实现 ISQLServerDataRecord 接口以及如何将其作为表值参数传递。 为简单起见，下面的示例将具有硬编码值只是一个行传递给表值参数。 理想情况下，用户可以实现此接口行流处理来自任何源，例如从文本文件。  
  
```  
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
>  请参阅部分**JDBC 驱动程序的表值参数 API**下面有关 Api 可用于设置表值参数的完整列表。  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 驱动程序的表值参数 API  
 **SQLServerMetaData**  
  
 此类表示列的元数据。 它用于在 ISQLServerDataRecord 界面中将列元数据传递给表值参数。 此类中的方法是：  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerMetaData （字符串 columnName、 int sqlType、 int 精度、 int 规模、 布尔 useServerDefault、 布尔 isUniqueKey、 SQLServerSortOrder sortOrder、 int sortOrdinal）|初始化使用指定的列名称、 sql 类型、 精度、 小数位数和服务器默认 SQLServerMetaData 的新实例。 这种形式的构造函数，它允许你指定的列是否在表值参数、 列和排序列的序号的排序顺序中是唯一支持表值参数。 <br><br>useServerDefault-指定此列是否应使用默认服务器值;默认值为 false。<br>isUniqueKey-指示是否表值参数中的列是唯一的;默认值为 false。<br>sortOrder-指示排序顺序的列;默认值为 SQLServerSortOrder.Unspecified。<br>sortOrdinal-指定的排序列; 序号从 0; sortOrdinal 开始默认值为-1。|
|公共 SQLServerMetaData （字符串 columnName，int sqlType）|初始化 SQLServerMetaData 使用的列名称和 sql 类型的新实例。|  
|公共 SQLServerMetaData （字符串 columnName、 int sqlType、 int 精度、 int 缩放）|初始化 SQLServerMetaData 使用列名称，sql 类型、 精度和小数位数的新实例。|  
|公共 SQLServerMetaData (SQLServerMetaData sqlServerMetaData)|另一个 SQLServerMetaData 对象初始化 SQLServerMetaData 从的新实例。|  
|公共字符串 getColumName()|检索的列名称。|  
|公共 int getSqlType()|检索 java sql 类型。|  
|公共 int getPrecision()|检索传递到列的类型的精度。|  
|公共 int getScale()|检索传递到列的类型的小数位数。|  
|公共 SQLServerSortOrder getSortOrder()|检索排序顺序。|
|公共 int getSortOrdinal()|检索排序序号。|
|公共布尔 isUniqueKey()|返回的列是唯一的。|
|公共布尔 useServerDefault()|返回列使用的默认服务器值。|
  
 **SQLServerSortOrder**
 
 枚举定义排序顺序。 可能的值为升序、 降序和未指定。 
  
 **SQLServerDataTable**  
  
 此类表示内存中数据表，以与表值参数一起使用。 此类中的方法是：  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerDataTable()|初始化 SQLServerDataTable 的新实例。|  
|公共迭代器 < 条目\<整数，对象 [] >> getIterator()|检索的数据表的行上的迭代器。|  
|公共 void addColumnMetadata （字符串 columnName，int sqlType）|添加为指定的列的元数据。|  
|公共 void addColumnMetadata （SQLServerDataColumn 列）|添加为指定的列的元数据。|  
|公共 void addRow （对象...值）|将一个数据行添加到数据表。|  
|公共映射\<整数，SQLServerDataColumn > getColumnMetadata()|检索此数据的表的列元数据。|
|公共 void clear （) |清除此数据的表。 |  
  
 **SQLServerDataColumn**  
  
 此类表示由 SQLServerDataTable 表示内存中数据表的列。 此类中的方法是：  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerDataColumn （字符串 columnName，int sqlType）|初始化 SQLServerDataColumn 具有列名称和类型的新实例。|  
|公共字符串 getColumnName()|检索的列名称。|  
|公共 int getColumnType()|检索的列类型。|  
  
 **ISQLServerDataRecord**  
  
 此类表示用户可以实现到表值参数的数据进行流处理的接口。 此接口中的方法是：  
  
|Name|Description|  
|----------|-----------------|  
|公共 SQLServerMetaData getColumnMetaData （int 列）;|检索给定的列索引的列元数据。|  
|公共 int getColumnCount();|检索总列数。|  
|公共对象 [] getRowData();|检索当前行的数据作为对象的数组。|  
|公共布尔 next （);|移动到下一行。 如果移动已成功，否则没有下一行，false，则返回 True。|  
  
 **SQLServerPreparedStatement**  
  
 以下方法已添加到此类，以支持表值参数传递。  
  
|Name|Description|  
|----------|-----------------|  
|公共最终 void setStructured （int parameterIndex、 字符串 tvpName、 SQLServerDataTable tvpDataTbale）|将填充数据表的表值参数。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpDataTable 是源数据表对象。|  
|公共最终 void setStructured （int parameterIndex、 字符串 tvpName、 ResultSet tvpResultSet）|从另一种表中检索的结果集，并用其填充表值参数。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpResultSet 是源结果集对象。|  
|公共最终 void setStructured （int parameterIndex、 字符串 tvpName、 ISQLServerDataRecord tvpDataRecord）|填充表值参数与 ISQLServerDataRecord 对象。 ISQLServerDataRecord 用于流式处理数据，并且用户决定如何使用它。 parameterIndex 是参数索引、 tvpName 是表值参数的名称和 tvpDataRecord 是一个 ISQLServerDataRecord 对象。|  
  
 **SQLServerCallableStatement**  
  
 以下方法已添加到此类，以支持表值参数传递。  
  
|Name|Description|  
|----------|-----------------|  
|（字符串 paratemeterName、 字符串 tvpName、 SQLServerDataTable tvpDataTable） 的公共最终 void setStructured|填充表值参数传递给带数据的表的存储过程。 paratemeterName 是参数的名称、 tvpName 是 TVP 的类型的名称和 tvpDataTable 是数据表对象。|  
|（字符串 paratemeterName、 字符串 tvpName、 ResultSet tvpResultSet） 的公共最终 void setStructured|填充表值参数传递给存储过程与从另一个表中检索的结果集。 paratemeterName 是参数的名称、 tvpName 是 TVP 的类型的名称和 tvpResultSet 是源结果集对象。|  
|（字符串 paratemeterName、 字符串 tvpName、 ISQLServerDataRecord tvpDataRecord） 的公共最终 void setStructured|填充表值参数传递给带 ISQLServerDataRecord 对象的存储过程。 ISQLServerDataRecord 用于流式处理数据，并且用户决定如何使用它。 paratemeterName 是参数的名称、 tvpName 是 TVP 的类型的名称和 tvpDataRecord 是一个 ISQLServerDataRecord 对象。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
