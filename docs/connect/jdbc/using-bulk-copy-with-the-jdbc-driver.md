---
title: 通过 JDBC Driver 使用大容量复制 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: df92d111897336fdcb40fad59cb5aafec3a52b6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803361"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>通过 JDBC 驱动程序使用大容量复制

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft SQL Server 包含一个名为 bcp 的受欢迎的命令行实用工具，以便将较大文件快速大容量复制到 SQL Server 数据库的表或视图中  。 SQLServerBulkCopy 类允许你采用 Java 编写可提供类似功能的代码解决方案。 还有其他方法可将数据加载到 SQL Server 表（例如，INSERT 语句）中，但 SQLServerBulkCopy 提供的性能优势明显超过它们。  
  
SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 但数据源并不局限于 SQL Server；可以使用任何数据源，只要数据可以使用 ResultSet、RowSet 或 ISQLServerBulkRecord 实现进行读取即可。  
  
通过使用 SQLServerBulkCopy 类，你可以执行：  
  
- 单次大容量复制操作  
  
- 多次大容量复制操作  
  
- 对事务进行的大容量复制操作  
  
> [!NOTE]  
> 使用 Microsoft JDBC Driver 4.1 for SQL Server 或更早版本（不支持 SQLServerBulkCopy 类）时，可以改为执行 SQL Server Transact-SQL BULK INSERT 语句。  
  
## <a name="bulk-copy-example-setup"></a>大容量复制示例设置  

SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 本文所示的代码示例使用 SQL Server 示例数据库 AdventureWorks。 为避免改变现有表，代码示例将数据写入必须一开始就创建的表中。  
  
BulkCopyDemoMatchingColumns 表和 BulkCopyDemoDifferentColumns 表均基于 AdventureWorks Production.Products 表。 在使用这些表的代码示例中，将数据从 Production.Products 表添加到其中一个示例表。 在该示例说明如何将列从源数据映射到目标表时，使用 BulkCopyDemoDifferentColumns 表；BulkCopyDemoMatchingColumns 适用于大多数其他示例。  
  
多个代码示例演示如何使用一个 SQLServerBulkCopy 类写入多个表。 对于这些示例，BulkCopyDemoOrderHeader 和 BulkCopyDemoOrderDetail 表将用作目标表。 这些表基于 AdventureWorks 中的 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 表。  
  
> [!NOTE]  
> 提供的 SQLServerBulkCopy 代码示例演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 TRANSACT-SQL INSERT ...用于复制数据的 SELECT 语句。  

### <a name="table-setup"></a>表设置  

若要创建正确运行代码示例所需的表，必须在 SQL Server 数据库中运行以下 Transact-SQL 语句。  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobject
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>单次大容量复制操作

执行 SQL Server 大容量复制操作的最简单方法是针对数据库执行单次操作。 默认情况下，大容量复制操作作为独立的操作执行：复制操作以非事务的方式执行，不可对其进行回滚。  
  
> [!NOTE]  
> 如果在发生错误时需要回滚全部或部分大容量复制，可以使用 SQLServerBulkCopy 托管的事务，或者在现有事务内执行大容量复制操作。  
> 有关详细信息，请参阅[事务和大容量复制操作](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#transaction-and-bulk-copy-operations)  
  
 执行大容量复制操作的常规步骤如下：  
  
1. 连接到源服务器并获取要复制的数据。 如果可从 ResultSet 对象或 ISQLServerBulkRecord 实现检索数据，则数据还可以来自其他源。  
  
2. 连接到目标服务器（除非希望 SQLServerBulkCopy 为你建立连接）  。  
  
3. 创建 SQLServerBulkCopy 对象，通过 setBulkCopyOptions 设置任何必要的属性  。  
  
4. 调用 setDestinationTableName 方法以指示用于大容量插入操作的目标表  。  
  
5. 调用 writeToServer 方法之一  。  
  
6. 可以通过 setBulkCopyOptions 更新属性，并再次调用 writeToServer（如有必要）   。  
  
7. 调用 close，或将大容量复制操作包装在 try-with-resources 语句内  。  
  
> [!CAUTION]  
> 我们建议使源列与目标列数据类型相匹配。 如果数据类型不匹配，则 SQLServerBulkCopy 会尝试将每个源值转换为目标数据类型。 转换可能会影响性能，也可能会导致意外错误。 例如，在多数情况下，Double 数据类型可转换为 Decimal 数据类型，但并非总是如此。  
  
### <a name="example"></a>示例

下面的应用程序演示了如何使用 SQLServerBulkCopy 类加载数据。 在此示例中，ResultSet 用于将数据从 SQL Server AdventureWorks 数据库中的 Production.Product 表复制到同一数据库中的一个类似表。  
  
> [!IMPORTANT]  
> 除非已按[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)中所述创建了工作表，否则将不会运行此示例。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 TRANSACT-SQL INSERT ...用于复制数据的 SELECT 语句。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>使用 Transact-SQL 执行大容量复制操作

下面的示例说明了如何使用 executeUpdate 方法执行 BULK INSERT 语句。  
  
> [!NOTE]  
> 数据源的文件路径相对于服务器。 服务器进程必须有权访问该路径，才能成功执行大容量复制操作。  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>多次大容量复制操作  

可以使用 SQLServerBulkCopy 类的单个实例执行多次大容量复制操作。 如果复制之间的操作参数已更改（例如，目标表的名称），必须首先更新它们，之后再对任何 writeToServer 方法进行任何后续调用，如以下示例所示。 除非已明确更改，否则将所有属性值保持为与给定实例的较早大容量复制上的属性值相同。  

> [!NOTE]  
> 与每个操作使用单独实例相比，使用 SQLServerBulkCopy 的同一实例执行多次大容量复制操作通常效率更高。  
  
在使用同一 SQLServerBulkCopy 对象执行多次大容量复制操作时，对于每个操作中的源信息或目标信息相同与否没有限制。 但是，必须确保每次写入服务器时正确设置列关联信息。  
  
> [!IMPORTANT]  
> 除非已按[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)中所述创建了工作表，否则将不会运行此示例。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 TRANSACT-SQL INSERT ...用于复制数据的 SELECT 语句。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>事务和大容量复制操作

 大容量复制操作可以作为独立操作或作为多步事务的一部分执行。 后面这个选项使你能够在同一事务中执行多个大容量复制操作，以及执行其他数据库操作（例如插入、更新和删除），同时仍能够提交或回滚整个事务。  
  
 默认情况下，大容量复制操作作为独立的操作执行。 大容量复制操作以非事务方式执行，不可以对其进行回滚。 如果在发生错误时需要回滚全部或部分大容量复制，可以使用 SQLServerBulkCopy 托管的事务，或者在现有事务内执行大容量复制操作。  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>执行非事务大容量复制操作

下面的应用程序演示了非事务大容量复制操作在操作中途遇到错误时将发生什么情况。  
  
在示例中，源表和目标表均包含名为 ProductID 的标识列  。 该代码首先通过删除所有行，然后插入知道其 ProductID 存在于源表中的一行，准备目标表  。 默认情况下，在目标表中为添加的每个行生成一个标识列的新值。 在此示例中，在打开连接时设置某个选项，该选项用于强制执行大容量加载过程以改为使用源表中的标识值。  
  
执行大容量复制操作，并将 BatchSize 属性设置为 10  。 当操作遇到无效行时，将引发异常。 在此第一个示例中，大容量复制操作是非事务的。 将提交在发生错误之前复制的所有批；将回滚包含重复项的批，并且在处理任何其他批之前中止大容量复制操作。  
  
> [!NOTE]  
> 除非已按[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)中所述创建了工作表，否则将不会运行此示例。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 TRANSACT-SQL INSERT ...用于复制数据的 SELECT 语句。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>在事务中执行专用的生成复制操作 

默认情况下，大容量复制操作是其自己的事务。 当想要执行专用的大容量复制操作时，请使用连接字符串创建 SQLServerBulkCopy 的新实例。 在此方案中，将创建大容量复制操作，然后提交或回滚该事务。 可以在 SQLServerBulkCopyOptions 中显式指定 UseInternalTransaction 选项，以便使大容量复制操作在其自己的事务中以显式方式执行，从而导致每批大容量复制操作在单独的事务中执行   。  
  
> [!NOTE]  
> 因为不同批在不同的事务中执行，因此如果在大容量复制操作期间出现错误，将回滚当前批中的所有行，但之前批中的行将保留在数据库中。  
  
在 BulkCopyNonTransacted 中指定 UseInternalTransaction 选项时，大容量复制操作将包含在较大的外部事务中   。 发生主键冲突错误时，将回滚整个事务，并且不会向目标表添加任何行。

```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>使用现有事务

可以将已启用事务的 Connection 对象作为参数传递在 SQLServerBulkCopy 构造函数中。 在这种情况下，大容量复制操作在现有事务中执行，并且不对事务状态进行任何更改（即，既不提交也不中止该事务）。 这允许应用程序将大容量复制操作包含在带有其他数据库操作的事务中。 如果由于出现错误需要回滚整个大容量复制操作，或者如果大容量复制应作为可以回滚的较大过程的一部分执行，你可以在大容量复制操作之后随时对 Connection 对象执行回滚。  
  
下面的应用程序与 BulkCopyNonTransacted  类似，但有一个例外：在此示例中，大容量复制操作包含在较大的外部事务中。 发生主键冲突错误时，将回滚整个事务，并且不会向目标表添加任何行。

> [!NOTE]  
> 除非已按[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)中所述创建了工作表，否则将不会运行此示例。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 TRANSACT-SQL INSERT ...用于复制数据的 SELECT 语句。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>从 CSV 文件进行大容量复制  

 下面的应用程序演示了如何使用 SQLServerBulkCopy 类加载数据。 在此示例中，CSV 文件用于将从 SQL Server AdventureWorks 数据库中的 Production.Product 表导出的数据复制到数据库中的一个类似表。  
  
> [!IMPORTANT]  
> 除非已按[表设置](../../ssms/download-sql-server-management-studio-ssms.md)中所述创建了工作表来获得该表，否则将不会运行此示例。  
  
1. 打开 SQL Server Management Studio 并连接到带有 AdventureWorks 数据库的 SQL Server  。  
  
2. 展开数据库，右键单击“AdventureWorks 数据库”，再依次选择“任务”  和“导出数据”  ...  
  
3. 对于数据源，请选择允许你连接到 SQL Server（例如 SQL Server Native Client 11.0）的“数据源”、检查配置，然后选择“下一步”    
  
4. 对于目标，请选择“平面文件目标”并输入含有目标的“文件名”（例如，C:\Test\TestBulkCSVExample.csv）   。 检查“格式”是否已分隔，“文本限定符”是否为无，并启用“在第一个数据行中显示列名称”，然后选择“下一步”      
  
5. 依次选择“编写查询以指定要传输的数据”和“下一步”   。  输入你的 SQL 语句  SELECT ProductID, Name, ProductNumber FROM Production.Product 并选择“下一步”   
  
6. 检查配置：可以将行分隔符保留为 {CR}{LF}，并将列分隔符保留为逗号 {,}。  选择“编辑映射”  ，并检查每个列的数据“类型”  是否正确（例如，整数用于 ProductID，而 Unicode 字符串则用于其他列）。  
  
7. 跳到“完成”，并运行导出  。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-always-encrypted-columns"></a>大容量复制 Always Encrypted 列  

从 Microsoft JDBC Driver 6.0 for SQL Server 开始，Always Encrypted 列支持大容量复制。  
  
根据大容量复制选项以及源和目标表的加密类型，JDBC 驱动程序可以透明地解密并加密数据，或者按原样发送加密数据。 例如，将加密列的数据大容量复制到未加密列时，驱动程序会透明地解密数据，然后将其发送给 SQL Server。 同样，将未加密列（或者 CSV 文件）的数据大容量复制到加密列时，驱动程序会透明地加密数据，然后将其发送给 SQL Server。 如果源和目标均已加密，则根据 allowEncryptedValueModifications 大容量复制选项，驱动程序将按原样发送数据，或解密数据并在将其发送到 SQL Server 之前再次对其进行加密  。  
  
有关详细信息，请参阅下面的 allowEncryptedValueModifications 大容量复制选项，和[结合使用 JDBC Driver 和 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  。  
  
> [!IMPORTANT]  
> 将 CSV 文件中的数据大容量复制到加密列时 Microsoft JDBC Driver 6.0 for SQL Server 的限制：  
>
> 日期和时间类型仅支持 Transact-SQL 默认字符串文字格式  
>
> 不支持 DATETIME 和 SMALLDATETIME 数据类型  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>用于 JDBC 驱动程序的大容量复制 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy 

使你可以有效地大容量加载带有来自其他源的数据的 SQL Server 表。  
  
Microsoft SQL Server 包含名为“bcp”的受欢迎的命令提示符实用工具，用于将数据从一个表移到另一个表（无论是在一台服务器上还是在服务器之间进行移动）。 SQLServerBulkCopy 类允许你采用 Java 编写可提供类似功能的代码解决方案。 还有其他方法可将数据加载到 SQL Server 表（例如，INSERT 语句）中，但 SQLServerBulkCopy 提供的性能优势明显超过它们。  
  
SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 但数据源并不局限于 SQL Server；可以使用任何数据源，只要数据可以使用 ResultSet 实例或 ISQLServerBulkRecord 实现进行读取即可。  
  
| 构造函数                             | 描述                                                                                                                                                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SQLServerBulkCopy(Connection)           | 使用指定的 SQLServerConnection 开放实例初始化 SQLServerBulkCopy 类的新实例。 如果 Connection 已启用事务，将在该事务内执行复制操作。 |
| SQLServerBulkCopy(String connectionURL) | 基于提供的 connectionURL，初始化并打开 SQLServerConnection 的新实例。 构造函数使用 SQLServerConnection 来初始化 SQLServerBulkCopy 类的新实例。                     |
  
| 属性                    | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| String DestinationTableName | 服务器上的目标表的名称。<br /><br /> 如果在调用 writeToServer 时尚未设置 DestinationTableName，将引发 SQLServerException。<br /><br /> DestinationTableName 名称包含三个部分 (\<database>.\<owningschema>.\<name>)。 可以使用表名称的数据库和所属架构（如果选择）对表名称进行限定。 但是，如果表名称使用下划线（“_”）或任何其他特殊字符，则必须使用方括号将名称括起来以对其进行转义。 有关详细信息，请参阅 SQL Server 联机丛书中的“标识符”。 |
| ColumnMappings              | 列映射定义数据源中的列与目标中的列之间的关系。<br /><br /> 如果未定义映射，将基于序号位置隐式映射该列。 对于这种方式，源架构和目标架构必须匹配。 如果它们不匹配，将引发异常。<br /><br /> 如果映射不为空，则并非数据源中存在的每一列均需要指定。 将忽略那些未映射的列。<br /><br /> 可以按名称或序号引用源列和目标列。               |
  
| 方法                                                                | 描述                                                                                                                                                                |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Void addColumnMapping((int sourceColumn, int destinationColumn)       | 使用序号指定源列和目标列来添加一个新的列映射。                                                                                  |
| Void addColumnMapping ((int sourceColumn, String destinationColumn)   | 对源列使用序号，对目标列使用列名，来添加一个新的列映射。                                                            |
| Void addColumnMapping ((String sourceColumn, int destinationColumn)   | 使用列名描述源列，同时使用序号指定目标列，来添加一个新的列映射。                                             |
| Void addColumnMapping (String sourceColumn, String destinationColumn) | 使用列名指定源列和目标列，来添加一个新的列映射。                                                                              |
| Void clearColumnMappings()                                            | 清除列映射的内容。                                                                                                                                |
| Void close()                                                          | 关闭 SQLServerBulkCopy 实例。                                                                                                                                     |
| SQLServerBulkCopyOptions getBulkCopyOptions()                         | 检索当前的 SQLServerBulkCopyOptions 集。                                                                                                                     |
| String getDestinationTableName()                                      | 检索当前的目标表名称。                                                                                                                               |
| Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)         | 根据提供的选项更新 SQLServerBulkCopy 实例的行为。                                                                                  |
| Void setDestinationTableName(String tableName)                        | 设置目标表的名称。                                                                                                                                    |
| Void writeToServer(ResultSet sourceData)                              | 将提供的 ResultSet 中的所有行都复制到由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定的目标表中。                           |
| Void writeToServer(RowSet sourceData)                                 | 将提供的 RowSet 中的所有行都复制到由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定的目标表中。                              |
| Void writeToServer(ISQLServerBulkRecord sourceData)                   | 将提供的 ISQLServerBulkRecord 实现中的所有行都复制到由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定的目标表中。 |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 控制 writeToServer 方法在 SQLServerBulkCopy 实例中的行为方式的设置集合。  
  
| 构造函数                | 描述                                                                                              |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCopyOptions() | 使用所有设置的默认值初始化 SQLServerBulkCopyOptions 类的新实例。 |
  
 Getter 和 setter 存在以下选项：  
  
| 选项                                   | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | ，则“默认”                                                              |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Boolean CheckConstraints                 | 在插入数据的同时检查约束。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | False - 不会检查约束                                   |
| Boolean FireTriggers                     | 当指定后，导致服务器对于行插入数据库触发插入触发器。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | False - 不会触发触发器                                        |
| Boolean KeepIdentity                     | 保留源标识值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | False - 由目标分配标识值              |
| Boolean KeepNulls                        | 无论默认值的设置为何，在目标表中都将保留 null 值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | False - null 值将替换为默认值（适用默认值的位置）。 |
| Boolean TableLock                        | 获取大容量复制操作期间的大容量更新锁定。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | False - 使用行锁定。                                          |
| Boolean UseInternalTransaction           | 当指定后，每批大容量复制操作将在事务中进行。 如果 SQLServerBulkCopy 使用现有连接（由构造函数指定），将引发 SQLServerException。  如果 SQLServerBulkCopy 已创建专用连接，将启用事务。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | False - 没有事务                                               |
| Int BatchSize                            | 每批中的行数。 在每批结束时，会将批中的行发送到服务器。<br /><br /> 当处理完 BatchSize 行或没有要发送到目标数据源的更多行时，即表示批已完成。  在已声明 SQLServerBulkCopy 实例而 UseInternalTransaction 选项不生效的情况下，会将行发送到服务器 BatchSize 行一次，但不执行任何与事务相关的操作。 如果 UseInternalTransaction 有效，每批行作为单独的事务插入。                                                                                                                                                                                                                                                                                                                                                                                                                                           | 0 - 指示每个 writeToServer 操作是单个批    |
| Int BulkCopyTimeout                      | 操作在多少秒内完成才不算超时。值为 0 表示没有限制；大容量复制将无限期等待。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 60 秒。                                                          |
| Boolean allowEncryptedValueModifications | Microsoft JDBC Driver 6.0 for SQL Server（或更高版本）提供该选项。<br /><br /> 指定后，allowEncryptedValueModifications 即可在表或数据库之间大容量复制加密数据，无需解密数据  。 通常，应用程序将从一个表中的加密列中选择数据并且无需密该数据（应用将连接到其列加密设置关键字设置为禁用的数据库），然后会使用此选项批量插入数据，这些数据仍然是加密的。 有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。<br /><br /> 指定 allowEncryptedValueModifications  时需谨慎，因为这可能会导致损坏数据库，因为驱动程序不会检查数据是否确实已加密，也不会检查是否使用与目标列相同的加密类型、算法和密钥对数据进行了正确加密。 |
  
 getters 和 setters：  
  
| 方法                                                                            | 描述                                                                                                                                                                               |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Boolean isCheckConstraints()                                                       | 指示是否在插入数据时检查约束。                                                                                                      |
| Void setCheckConstraints(Boolean checkConstraints)                                 | 设置是否在插入数据时检查约束。                                                                                                           |
| Boolean isFireTriggers()                                                           | 指示服务器是否应对插入数据库的行触发插入触发器。                                                                                    |
| Void setFireTriggers(Boolean fireTriggers)                                         | 设置是否应将服务器设置为对插入数据库的行触发触发器。                                                                                     |
| Boolean isKeepIdentity()                                                           | 指示是否保留任何源标识值。                                                                                                                          |
| Void setKeepIdentity(Boolean keepIdentity)                                         | 设置是否保留标识值。                                                                                                                                          |
| Boolean isKeepNulls()                                                              | 指示是否在目标表中保留空值，而不考虑默认值的设置，或者是否应将其替换为默认值（如果适用）。 |
| Void setKeepNulls(Boolean keepNulls)                                               | 设置是否在目标表中保留空值，而不考虑默认值的设置，或者是否应将其替换为默认值（如果适用）。      |
| Boolean isTableLock()                                                              | 指示 SQLServerBulkCopy 是否应在大容量复制操作期间获取大容量更新锁。                                                                         |
| Void setTableLock(Boolean tableLock)                                               | 设置 SQLServerBulkCopy 是否应在大容量复制操作期间获取大容量更新锁。                                                                              |
| Boolean isUseInternalTransaction()                                                 | 指示每批大容量复制操作是否将在事务中进行。                                                                                                  |
| Void setUseInternalTranscation(Boolean useInternalTransaction)                     | 设置每批大容量复制操作是否将在事务中进行。                                                                                               |
| Int getBatchSize()                                                                 | 获取每批的行数。 在每批结束时，会将批中的行发送到服务器                                                                             |
| Void setBatchSize(int batchSize)                                                   | 设置每批的行数。 在每批结束时，会将批中的行发送到服务器。                                                                            |
| Int getBulkCopyTimeout()                                                           | 获取超时之前要完成操作的秒数。                                                                                                             |
| Void  setBulkCopyTimeout(int timeout)                                              | 设置超时之前要完成操作的秒数。                                                                                                             |
| boolean isAllowEncryptedValueModifications()                                       | 指示是启用还是禁用 allowEncryptedValueModifications 设置。                                                                                                        |
| void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications) | 配置用于大容量复制 Always Encrypted 列的 allowEncryptedValueModifications 设置。                                                                         |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 ISQLServerBulkRecord 接口可用于创建读取来自任何源（如文件）的数据的类，并且允许 SQLServerBulkCopy 实例大容量加载带有该数据的 SQL Server 表。  
  
| 接口方法                   | 描述                                                                                                                                                                                                                                                                                            |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Set\<Integer> getColumnOrdinals()   | 获取此数据记录中所表示的每个列的序号。                                                                                                                                                                                                                              |
| String getColumnName(int column)    | 获取给定列的名称。                                                                                                                                                                                                                                                                      |
| Int getColumnType(int column)       | 获取给定列的 JDBC 数据类型。                                                                                                                                                                                                                                                            |
| Int getPrecision(int column)        | 获取给定列的精度。                                                                                                                                                                                                                                                                |
| Object[] getRowData()               | 获取作为对象数组的当前行的数据。<br /><br /> 每个对象必须匹配 Java 语言类型，该类型用于代表针对给定列指示的 JDBC 数据类型。  有关详细信息，请参阅“‘了解 JDBC Driver 数据类型”，以了解相应映射。 |
| Int getScale(int column)            | 获取给定列的小数位数。                                                                                                                                                                                                                                                                    |
| Boolean isAutoIncrement(int column) | 指示列是否表示一个标识列。                                                                                                                                                                                                                                            |
| Boolean next()                      | 前移到下一数据行。                                                                                                                                                                                                                                                                         |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

简单实现可用于从分隔文件（其中每一行表示一行数据）中读取基本 Java 数据类型的 ISQLServerBulkRecord 接口。  
  
实现说明和限制：  
  
1. 因为数据一次读取一行，可用内存将限制任何给定行中允许的最大数据量。  
  
2. 不支持流式处理大型数据类型（例如，varchar(max)、varbinary(max)、nvarchar(max)、sqlxml、ntext）。  
  
3. 为 CSV 文件指定的分隔符不应显示在数据中的任意位置，并且如果该分隔符是 Java 正则表达式中限制使用的字符，应对其正确转义。  
  
4. 在 CSV 文件实现中，将双引号视为数据的一部分。 例如，如果分隔符是逗号，行 hello,"world","hello,world" 被视为包含具有以下值的四列：hello、“world”、“hello 和 world”。  
  
5. 新的换行符用作行终止符，并且不允许出现在数据中的任意位置。  
  
| 构造函数                                                                                                                                                                 | 描述                                                                                                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, String, boolean) | 初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用提供的分隔符和编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，则该文件中的第一行将分析为列名称。  如果编码为 NULL，将使用默认编码。            |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, boolean)                           | 初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用逗号分隔符和提供的编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，则该文件中的第一行将分析为列名称。  如果编码为 NULL，将使用默认编码。 |
| SQLServerBulkCSVFileRecord(String fileToParse, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, boolean)                                                    | 初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用逗号分隔符和默认编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，则该文件中的第一行将分析为列名称。                                                           |
  
| 方法                                                                                                 | 描述                                                                                         |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| Void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)  | 为文件中的给定列添加元数据。                                                     |
| Void close()                                                                                           | 释放与文件读取器关联的任何资源。                                             |
| Void setTimestampWithTimezoneFormat(DateTim eFormatter dateTimeFormatter                               | 将用于分析来自文件的时间戳数据格式设置为 java.sql.Types.TIMESTAMP_WITH_TIMEZONE。 |
| Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter) | 将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。           |
| Void setTimeWithTimezoneFormat(DateTimeForm atter dateTimeFormatter)                                   | 将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。           |
| Void setTimeWithTimezoneFormat(String timeFormat)                                                      | 将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。           |
  
## <a name="see-also"></a>另请参阅  

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
