---
title: "使用 JDBC 驱动程序的大容量复制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 4edc1b7348e9b34c924236819f0122ea5277d3e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>通过 JDBC 驱动程序使用大容量复制
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft SQL Server 包括一个名为的常用命令行实用工具**bcp**为快速批量将大型文件复制到 SQL Server 数据库中表或视图。 SQLServerBulkCopy 类可以编写提供类似的功能的 java 代码解决方案。 还有其他方式将数据载入 SQL Server 表 （例如 INSERT 语句） 但 SQLServerBulkCopy 提供它们中有显著的性能优势。  
  
 SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 但数据源并不局限于 SQL Server；可以使用任何数据源，只要数据可以使用 ResultSet、RowSet 或 ISQLServerBulkRecord 实现进行读取即可。  
  
 通过使用 SQLServerBulkCopy 类，你可以执行：  
  
-   单次大容量复制操作  
  
-   多次大容量复制操作  
  
-   对事务进行的大容量复制操作  
  
> [!NOTE]  
>  使用 Microsoft JDBC Driver 4.1 for SQL Server 或更早版本（不支持 SQLServerBulkCopy 类）时，可以改为执行 SQL Server Transact-SQL BULK INSERT 语句。  
  
## <a name="bulk-copy-example-setup"></a>大容量复制示例设置  
 SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 本主题中所示的代码示例使用 SQL Server 示例数据库 AdventureWorks。 为避免改变现有表，代码示例将数据写入必须一开始就创建的表中。  
  
 BulkCopyDemoMatchingColumns 表和 BulkCopyDemoDifferentColumns 表均基于 AdventureWorks Production.Products 表。 在使用这些表的代码示例中，将数据从 Production.Products 表添加到其中一个示例表。 在该示例说明如何将列从源数据映射到目标表时，使用 BulkCopyDemoDifferentColumns 表；BulkCopyDemoMatchingColumns 适用于大多数其他示例。  
  
 多个代码示例演示如何使用一个 SQLServerBulkCopy 类写入多个表。 对于这些示例，BulkCopyDemoOrderHeader 和 BulkCopyDemoOrderDetail 表将用作目标表。 这些表基于 AdventureWorks 中的 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 表。  
  
> [!NOTE]  
>  提供的 SQLServerBulkCopy 代码示例演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
###  <a name="BKMK_TableSetup"></a>表设置  
 若要创建正确运行代码示例所需的表，必须在 SQL Server 数据库中运行以下 Transact-SQL 语句。  
  
```  
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
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
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
  
## <a name="single-bulk-copy-operations"></a>单次批量复制操作  
 执行 SQL Server 大容量复制操作的最简单方法是针对数据库执行单次操作。 默认情况下，大容量复制操作作为独立的操作执行：复制操作以非事务的方式执行，不可对其进行回滚。  
  
> [!NOTE]  
>  如果需要回滚批量复制的全部或部分发生错误时，可以使用 SQLServerBulkCopy 管理事务，或执行大容量复制操作在现有事务中。  
>   
>  有关详细信息，请参阅[事务和大容量复制操作](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TransactionBulk)  
  
 执行大容量复制操作的常规步骤如下：  
  
1.  连接到源服务器并获取要复制的数据。 如果可从 ResultSet 对象或 ISQLServerBulkRecord 实现检索数据，则数据还可以来自其他源。  
  
2.  连接到目标服务器 (除非你想**SQLServerBulkCopy**来为你建立的连接)。  
  
3.  创建 SQLServerBulkCopy 对象，设置任何必要的属性通过**setBulkCopyOptions**。  
  
4.  调用**setDestinationTableName**方法，以指示目标表大容量插入操作。  
  
5.  调用之一**writeToServer**方法。  
  
6.  （可选） 更新属性通过**setBulkCopyOptions**并调用**writeToServer**根据需要再次。  
  
7.  调用**关闭**，或换行大容量复制操作，请尝试使用资源语句中的。  
  
> [!CAUTION]  
>  我们建议使源列与目标列数据类型相匹配。 如果数据类型不匹配，则 SQLServerBulkCopy 会尝试将每个源值转换为目标数据类型。 转换可能会影响性能，也可能会导致意外错误。 例如，在多数情况下，Double 数据类型可转换为 Decimal 数据类型，但并非总是如此。  
  
### <a name="example"></a>示例  
 下面的应用程序演示了如何使用 SQLServerBulkCopy 类加载数据。 在此示例中，ResultSet 用于将数据从 SQL Server AdventureWorks 数据库中的 Production.Product 表复制到同一数据库中的一个类似表。  
  
> [!IMPORTANT]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
                        // Open the destination connection. In the real world you would    
                        // not use SQLServerBulkCopy to move data from one table to the other    
                        // in the same database. This is for demonstration purposes only.   
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            // Set up the bulk copy object.    
                            // Note that the column positions in the source   
                            // table match the column positions in    
                            // the destination table so there is no need to   
                            // map columns.   
                            try (SQLServerBulkCopy bulkCopy =  
                                       new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                try  
                                {  
                                    // Write from the source to the destination.  
                                    bulkCopy.writeToServer(rsSourceData);  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                }  
                            }  
  
                            // Perform a final count on the destination    
                            // table to see how many rows were added.  
                            try (ResultSet rsRowCount = stmt.executeQuery(  
                                    "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                            {  
                                rsRowCount.next();  
                                long countEnd = rsRowCount.getInt(1);  
                                System.out.println("Ending row count = " + countEnd);  
                                System.out.println((countEnd - countStart) + " rows were added.");  
                            }  
                        }  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>使用 Transact-SQL 执行大容量复制操作  
 下面的示例说明了如何使用 executeUpdate 方法执行 BULK INSERT 语句。  
  
> [!NOTE]  
>  数据源的文件路径相对于服务器。 服务器进程必须有权访问该路径，才能成功执行大容量复制操作。  
  
```  
try (Connection con = DriverManager.getConnection(connectionString))  
{  
    try (Statement stmt = con.createStatement())  
    {  
        // Perform the BULK INSERT  
        stmt.executeUpdate(  
                "BULK INSERT Northwind.dbo.[Order Details] " +  
                        "FROM 'f:\\mydata\\data.tbl' " +  
                        "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");  
    }  
}  
```  
  
## <a name="multiple-bulk-copy-operations"></a>多次大容量复制操作  
 可以使用 SQLServerBulkCopy 类的单个实例执行多次大容量复制操作。 如果复制之间的操作参数已更改（例如，目标表的名称），必须首先更新它们，之后再对任何 writeToServer 方法进行任何后续调用，如以下示例所示。 除非已明确更改，否则将所有属性值保持为与给定实例的较早大容量复制上的属性值相同。  
  
> [!NOTE]  
>  与每个操作使用单独实例相比，使用 SQLServerBulkCopy 的同一实例执行多次大容量复制操作通常效率更高。  
  
 在使用同一 SQLServerBulkCopy 对象执行多次大容量复制操作时，对于每个操作中的源信息或目标信息相同与否没有限制。 但是，必须确保每次写入服务器时正确设置列关联信息。  
  
> [!IMPORTANT]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection1 = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection1.createStatement())  
                {  
  
                    // Empty the destination tables.   
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderHeader;");  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderDetail;");  
  
                    // Perform an initial count on the destination   
                    //  table with matching columns.  
                    long countStartHeader = 0;  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        countStartHeader = rsRowCountHeader.getInt(1);  
                        System.out.println("Starting row count for Header table = " + countStartHeader);  
                    }  
  
                    // Perform an initial count on the destination   
                    // table with different column positions.  
                    long countStartDetail = 0;  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        countStartDetail = rsRowCountDetail.getInt(1);  
                        System.out.println("Starting row count for Detail table = " + countStartDetail);  
                    }  
  
                    // Get data from the source table as a ResultSet.   
                    // The Sales.SalesOrderHeader and Sales.SalesOrderDetail   
                    // tables are quite large and could easily cause a timeout   
                    // if all data from the tables is added to the destination.    
                    // To keep the example simple and quick, a parameter is     
                    // used to select only orders for a particular account    
                    // as the source for the bulk insert.  
                    try (PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(  
                            "SELECT [SalesOrderID], [OrderDate], " +  
                            "[AccountNumber] FROM [Sales].[SalesOrderHeader] " +  
                            "WHERE [AccountNumber] = ?;"))  
                    {  
                        preparedStmt1.setString(1, "10-4020-000034");  
  
                        try (ResultSet rsHeader = preparedStmt1.executeQuery())  
                        {  
                            // Get the Detail data in a separate connection.   
                            try (Connection sourceConnection2 = DriverManager.getConnection(connectionString))  
                            {  
                                try (PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(  
                                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], " +  
                                                "[SalesOrderDetailID], [OrderQty], [ProductID], " +  
                                                "[UnitPrice] FROM [Sales].[SalesOrderDetail] " +  
                                                "INNER JOIN [Sales].[SalesOrderHeader] " +  
                                                "ON [Sales].[SalesOrderDetail].[SalesOrderID] " +  
                                                "= [Sales].[SalesOrderHeader].[SalesOrderID] " +  
                                                "WHERE [AccountNumber] = ?;"))  
                                {  
                                    preparedStmt2.setString(1, "10-4020-000034");  
  
                                    try (ResultSet rsDetail = preparedStmt2.executeQuery())  
                                    {  
                                        // Create the SQLServerBulkCopySQLServerBulkCopy object.    
                                        try (SQLServerBulkCopy bulkCopy =  
                                                   new SQLServerBulkCopy(connectionString))  
                                        {  
                                            bulkCopy.setBulkCopyOptions(copyOptions);  
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderHeader");  
  
                                            // Guarantee that columns are mapped correctly by   
                                            // defining the column mappings for the order.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping("OrderDate", "OrderDate");  
                                            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");  
  
                                            // Write rsHeader to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsHeader);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
  
                                            // Set up the order details destination.   
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderDetail");  
  
                                            // Clear the existing column mappings  
                                            bulkCopy.clearColumnMappings();  
  
                                            // Add order detail column mappings.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping(  
                                                    "SalesOrderDetailID",   
                                                    "SalesOrderDetailID");  
                                            bulkCopy.addColumnMapping("OrderQty", "OrderQty");  
                                            bulkCopy.addColumnMapping("ProductID", "ProductID");  
                                            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");  
  
                                            // Write rsDetail to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsDetail);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
                                        }  
                                    }  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination   
                    // tables to see how many rows were added.  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        long countEndHeader =  rsRowCountHeader.getInt(1);  
                        System.out.println(  
                                (countEndHeader - countStartHeader) +   
                                " rows were added to the Header table.");  
                    }  
  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        long countEndDetail = rsRowCountDetail.getInt(1);  
                        System.out.println(  
                                (countEndDetail - countStartDetail) +   
                                " rows were added to the Detail table.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
##  <a name="BKMK_TransactionBulk"></a>事务和批量复制操作  
 大容量复制操作可以作为独立操作或作为多步事务的一部分执行。 后面这个选项使你能够在同一事务中执行多个大容量复制操作，以及执行其他数据库操作（例如插入、更新和删除），同时仍能够提交或回滚整个事务。  
  
 默认情况下，大容量复制操作作为独立的操作执行。 大容量复制操作以非事务方式执行，不可以对其进行回滚。 如果在发生错误时需要回滚全部或部分大容量复制，可以使用 SQLServerBulkCopy 托管的事务，或者在现有事务内执行大容量复制操作。  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>执行非事务大容量复制操作  
 下面的应用程序演示了非事务大容量复制操作在操作中途遇到错误时将发生什么情况。  
  
 在示例中，源表和目标表中各包含一个名为的标识列**ProductID**。 代码首先通过删除所有行准备目标表，然后插入单个行其**ProductID**已知源表中存在。 默认情况下，在目标表中为添加的每个行生成一个标识列的新值。 在此示例中，在打开连接时设置某个选项，该选项用于强制执行大容量加载过程以改为使用源表中的标识值。  
  
 执行批量复制操作时使用**BatchSize**属性设置为 10。 当操作遇到无效行时，将引发异常。 在此第一个示例中，大容量复制操作是非事务的。 将提交在发生错误之前复制的所有批；将回滚包含重复项的批，并且在处理任何其他批之前中止大容量复制操作。  
  
> [!NOTE]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.  
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection String.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
              "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>在事务中执行专用的生成复制操作  
 默认情况下，大容量复制操作是其自己的事务。 当想要执行专用的大容量复制操作时，请使用连接字符串创建 SQLServerBulkCopy 的新实例。 在此方案中，将创建大容量复制操作，然后提交或回滚该事务。 你可以显式指定**UseInternalTransaction**选项**SQLServerBulkCopyOptions**以显式导致批量复制操作要在其自己的事务，使每批批量中执行复制操作将在单独的事务中执行。  
  
> [!NOTE]  
>  因为不同批在不同的事务中执行，因此如果在大容量复制操作期间出现错误，将回滚当前批中的所有行，但之前批中的行将保留在数据库中。  
  
 下面的应用程序与之前的示例类似，但有一个例外：在此示例中，大容量复制操作管理其自己的事务。 将提交在发生错误之前复制的所有批；将回滚包含重复项的批，并且在处理任何其他批之前中止大容量复制操作。  
  
> [!NOTE]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object.  
                        // Note that when specifying the UseInternalTransaction   
                        // option, you cannot also use an external transaction.   
                        // Therefore, you must use the SQLServerBulkCopy construct that   
                        // requires a string for the connection, rather than an   
                        // existing Connection object.   
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
                        copyOptions.setUseInternalTransaction(true);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="using-existing-transactions"></a>使用现有事务  
 可以将已启用事务的 Connection 对象作为参数传递在 SQLServerBulkCopy 构造函数中。 在这种情况下，大容量复制操作在现有事务中执行，并且不对事务状态进行任何更改（即，既不提交也不中止该事务）。 这允许应用程序将大容量复制操作包含在带有其他数据库操作的事务中。 如果由于出现错误需要回滚整个大容量复制操作，或者如果大容量复制应作为可以回滚的较大过程的一部分执行，你可以在大容量复制操作之后随时对 Connection 对象执行回滚。  
  
 下面的应用程序与第一个（非事务）示例类似，但有一个例外：在此示例中，大容量复制操作包含在较大的外部事务中。 发生主键冲突错误时，将回滚整个事务，并且不会向目标表添加任何行。  
  
> [!NOTE]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)。 提供的这一代码演示了仅供 SQLServerBulkCopy 使用的语法。 如果源表和目标表位于同一 SQL Server 实例中，则可以更轻松且更快速地使用 TRANSACT-SQL INSERT ... 用于复制数据的 SELECT 语句。  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object inside the transaction.  
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            destinationConnection.setAutoCommit(false);  
  
                            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                            copyOptions.setKeepIdentity(true);  
                            copyOptions.setBatchSize(10);  
  
                            try (SQLServerBulkCopy bulkCopy =   
                                    new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setBulkCopyOptions(copyOptions);  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                // Write from the source to the destination.   
                                // This should fail with a duplicate key error.   
                                try  
                                {  
                                    bulkCopy.writeToServer(rsSourceData);  
                                    destinationConnection.commit();  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                    destinationConnection.rollback();  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-from-a-csv-file"></a>从 CSV 文件进行大容量复制  
 下面的应用程序演示了如何使用 SQLServerBulkCopy 类加载数据。 在此示例中，CSV 文件用于将从 SQL Server AdventureWorks 数据库中的 Production.Product 表导出的数据复制到数据库中的一个类似表。  
  
> [!IMPORTANT]  
>  除非你已创建了工作表中所述，将不会运行此示例[表设置](../../ssms/download-sql-server-management-studio-ssms.md)即可使用它。  
  
1.  打开**SQL Server Management Studio**并连接到 SQL Server 使用 AdventureWorks 数据库。  
  
2.  展开数据库，右键单击的 AdventureWorks 数据库，选择**任务**和**导出数据**...  
  
3.  对于数据源中，选择**数据源**这样，你要连接到 SQL Server (例如 SQL Server Native Client 11.0)，请检查配置，然后**下一步**  
  
4.  目标位置，请选择**平面文件目标**并输入**文件名**以如 C:\Test\TestBulkCSVExample.csv 为目标。 检查**格式**分隔，**文本限定符**为 none，并启用**中第一个数据行的列名称**，然后选择**下一步**  
  
5.  选择**编写查询以指定要传输的数据**和**下一步**。  输入你**SQL 语句**选择 ProductID、 名称、 ProductNumber 从 Production.Product 和**下一步**  
  
6.  检查配置：可以将行分隔符保留为 {CR}{LF}，并将列分隔符保留为逗号 {,}。  选择**编辑映射**... 和检查数据**类型**为每个列 （例如其他的 ProductID 和 Unicode 字符串的整数） 正确无误。  
  
7.  跳到**完成**并运行导出。  
  
```  
  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        SQLServerBulkCSVFileRecord fileRecord = null;  
        try  
        {              
            // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.  
            // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.  
            fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);      
  
            // Set the metadata for each column to be copied.  
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);  
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);  
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);  
  
            // Open a destinationConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection destinationConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = destinationConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Set up the bulk copy object.    
                    // Note that the column positions in the source   
                    // data reader match the column positions in    
                    // the destination table so there is no need to   
                    // map columns.   
                    try (SQLServerBulkCopy bulkCopy =  
                               new SQLServerBulkCopy(destinationConnection))  
                    {  
                        bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                        try  
                        {  
                            // Write from the source to the destination.  
                            bulkCopy.writeToServer(fileRecord);  
                        }  
                        catch (Exception e)  
                        {  
                            // Handle any errors that may have occurred.  
                            e.printStackTrace();  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
        finally  
        {  
            if (fileRecord != null) try { fileRecord.close(); } catch(Exception e) {}  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-with-always-encrypted-columns"></a>使用始终加密列的大容量复制  
 从 SQL Server 的 Microsoft JDBC Driver 6.0，大容量复制支持始终加密列。  
  
 具体取决于大容量复制选项和加密的 JDBC 驱动程序可能以透明方式解密，然后加密的数据或它的源和目标表的类型可能会发送加密的数据按原样。 例如，当大容量将从加密列的数据复制到未加密的列，该驱动程序以透明方式解密数据发送到 SQL Server 之前。 同样当大容量复制到加密列数据从一个未加密的列 （或从 CSV 文件），该驱动程序以透明方式加密数据发送到 SQL Server 之前。 如果源域和目标进行加密，然后根据**allowEncryptedValueModifications**大容量复制选项，该驱动程序将发送数据，如或者将解密的数据，在发送到 SQL Server 之前再次对其进行加密。  
  
 有关详细信息，请参阅**allowEncryptedValueModifications**大容量复制选项下面，和[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  对于 SQL Server，大容量将数据从 CSV 文件复制到加密列时的 Microsoft JDBC Driver 6.0 限制：  
>   
>  仅 Transact SQL 默认字符串文本都支持此格式的日期和时间类型  
>   
>  不支持日期时间和 SMALLDATETIME 数据类型  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>用于 JDBC 驱动程序的大容量复制 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy  
 使你可以有效地大容量加载带有来自其他源的数据的 SQL Server 表。  
  
 Microsoft SQL Server 包含名为“bcp”的受欢迎的命令提示符实用工具，用于将数据从一个表移到另一个表（无论是在一台服务器上还是在服务器之间进行移动）。 SQLServerBulkCopy 类允许你采用 Java 编写可提供类似功能的代码解决方案。 还有其他方法可将数据加载到 SQL Server 表（例如，INSERT 语句）中，但 SQLServerBulkCopy 提供的性能优势明显超过它们。  
  
 SQLServerBulkCopy 类可用于只将数据写入 SQL Server 表。 但数据源并不局限于 SQL Server；可以使用任何数据源，只要数据可以使用 ResultSet 实例或 ISQLServerBulkRecord 实现进行读取即可。  
  
|构造函数|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopy(Connection)|初始化使用指定的公开实例的 SQLServerConnection SQLServerBulkCopy 类的新实例。 如果 Connection 已启用事务，将在该事务内执行复制操作。|  
|SQLServerBulkCopy (字符串 connectionURL)|初始化并打开 SQLServerConnection 基于提供 connectionURL 的新实例。 构造函数使用 SQLServerConnection 初始化 SQLServerBulkCopy 类的新实例。|  
  
|属性|Description|  
|--------------|-----------------|  
|字符串 DestinationTableName|服务器上的目标表的名称。<br /><br /> 如果在调用 writeToServer 时尚未设置 DestinationTableName，将引发 SQLServerException。<br /><br /> DestinationTableName 是一个由三部分名称 (\<数据库 >。\<owningschema >。\<名称 >)。 可以使用表名称的数据库和所属架构（如果选择）对表名称进行限定。 但是，如果表名称使用下划线（“_”）或任何其他特殊字符，则必须使用方括号将名称括起来以对其进行转义。 有关详细信息，请参阅 SQL Server 联机丛书中的“标识符”。|  
|ColumnMappings|列映射定义数据源中的列与目标中的列之间的关系。<br /><br /> 如果未定义映射，将基于序号位置隐式映射该列。 对于这种方式，源架构和目标架构必须匹配。 如果它们不匹配，将引发异常。<br /><br /> 如果映射不为空，则并非数据源中存在的每一列均需要指定。 将忽略那些未映射的列。<br /><br /> 可以按名称或序号引用源列和目标列。|  
  
|方法|Description|  
|------------|-----------------|  
|Void addColumnMapping （int sourceColumn (int destinationColumn）|使用序号指定源列和目标列来添加一个新的列映射。|  
|Void addColumnMapping （int sourceColumn (字符串 destinationColumn）|对源列使用序号，对目标列使用列名，来添加一个新的列映射。|  
|Void addColumnMapping （字符串 sourceColumn (int destinationColumn）|使用列名描述源列，同时使用序号指定目标列，来添加一个新的列映射。|  
|Void addColumnMapping （字符串 sourceColumn，字符串 destinationColumn）|使用列名指定源列和目标列，来添加一个新的列映射。|  
|Void clearColumnMappings()|清除列映射的内容。|  
|Void close （)|关闭 SQLServerBulkCopy 实例。|  
|SQLServerBulkCopyOptions getBulkCopyOptions()|检索当前的 SQLServerBulkCopyOptions 集。|  
|字符串 getDestinationTableName()|检索当前的目标表名称。|  
|Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)|根据提供的选项更新 SQLServerBulkCopy 实例的行为。|  
|Void setDestinationTableName(String tableName)|设置目标表的名称。|  
|Void writeToServer(ResultSet sourceData)|将在提供的结果集中的所有行都复制到由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定的目标表中。|  
|Void writeToServer(RowSet sourceData)|将提供的 RowSet 中的所有行都复制到由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定的目标表中。|  
|Void writeToServer(ISQLServerBulkRecord sourceData)|副本由 SQLServerBulkCopy 对象的 DestinationTableName 属性指定提供的 ISQLServerBulkRecord 实现到目标表中的所有行。|  
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  
 控制 writeToServer 方法在 SQLServerBulkCopy 实例中的行为方式的设置集合。  
  
|构造函数|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopyOptions()|初始化使用默认值有关的所有设置 SQLServerBulkCopyOptions 类的新实例。|  
  
 Getter 和 setter 存在以下选项：  
  
|选项|Description|默认|  
|------------|-----------------|-------------|  
|布尔 CheckConstraints|在插入数据的同时检查约束。|False - 不会检查约束|  
|布尔 FireTriggers|当指定后，导致服务器对于行插入数据库触发插入触发器。|False - 不会触发触发器|  
|布尔 KeepIdentity|保留源标识值。|False - 由目标分配标识值|  
|布尔 KeepNulls|无论默认值的设置为何，在目标表中都将保留 null 值。|False - null 值将替换为默认值（适用默认值的位置）。|  
|布尔 TableLock|获取大容量复制操作期间的大容量更新锁定。|False - 使用行锁定。|  
|布尔 UseInternalTransaction|当指定后，每批大容量复制操作将在事务中进行。 如果 SQLServerBulkCopy 使用现有连接（由构造函数指定），将引发 SQLServerException。  如果 SQLServerBulkCopy 已创建专用连接，将启用事务。|False - 没有事务|  
|Int BatchSize|每批中的行数。 在每批结束时，会将批中的行发送到服务器。<br /><br /> 当处理完 BatchSize 行或没有要发送到目标数据源的更多行时，即表示批已完成。  在已声明 SQLServerBulkCopy 实例而 UseInternalTransaction 选项不生效的情况下，会将行发送到服务器 BatchSize 行一次，但不执行任何与事务相关的操作。 如果 UseInternalTransaction 有效，每批行作为单独的事务插入。|0 - 指示每个 writeToServer 操作是单个批|  
|Int BulkCopyTimeout|超时之前要完成操作的秒数。值为 0 表示没有限制；大容量复制将无限期等待。|60 秒。|  
|布尔 allowEncryptedValueModifications|此选项才可用与 Microsoft JDBC Driver 6.0 （或更高版本） for SQL Server。<br /><br /> 如果指定， **allowEncryptedValueModifications**启用的表或数据库之间的加密数据而无需解密数据的大容量复制。 通常情况下，应用程序可以不解密 （应用程序将连接到数据库与列加密设置关键字设置为禁用） 的数据从一个表中的加密列选择数据，然后将使用此选项将大容量插入数据，这仍然为加密。 有关详细信息，请参阅[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。<br /><br /> 指定时要格外小心**allowEncryptedValueModifications**这可能会导致损坏数据库，因为该驱动程序不会检查是否确实已加密数据，或者如果正确加密使用相同的加密类型、 算法和密钥与目标列。||  
  
 Getter 和 setter:  
  
|方法|Description|  
|-------------|-----------------|  
|布尔 isCheckConstraints()|该值指示是否要检查正在插入数据的同时检查约束。|  
|Void setCheckConstraints(Boolean checkConstraints)|设置是否检查正在插入数据的同时检查约束。|  
|布尔 isFireTriggers()|指示是否服务器应激发插入触发器，从而插入到数据库的行。|  
|Void setFireTriggers(Boolean fireTriggers)|设置是否应设置服务器激发插入到数据库的行的触发器。|  
|布尔 isKeepIdentity()|指示保留任何源标识值。|  
|Void setKeepIdentity(Boolean keepIdentity)|设置保留标识值。|  
|布尔 isKeepNulls()|指示是否保留而不考虑默认值，设置目标表中的 null 值，或如果它们应替换为默认值 （如果适用）。|  
|Void setKeepNulls(Boolean keepNulls)|设置是否保留而不考虑默认值，设置目标表中的 null 值，或如果它们应替换为默认值 （如果适用）。|  
|布尔 isTableLock()|指示 SQLServerBulkCopy 是否应获取批量复制操作的持续时间内的大容量更新锁。|  
|Void setTableLock(Boolean tableLock)|设置是否 SQLServerBulkCopy 应获取批量复制操作的持续时间的大容量更新锁。|  
|布尔 isUseInternalTransaction()|指示是否每批批量复制操作将在事务内发生。|  
|Void setUseInternalTranscation(Boolean useInternalTransaction)|是否每个批大容量复制操作将在事务内发生，或不设置。|  
|Int getBatchSize()|获取每个批中的行数。 在每个批的结束时，批处理中的行发送到服务器|  
|Void setBatchSize(int batchSize)|设置每个批处理中的行数。 在每批结束时，会将批中的行发送到服务器。|  
|Int getBulkCopyTimeout()|获取操作的秒才能完成超时之前的数。|  
|Void setBulkCopyTimeout(int timeout)|设置操作完成之前超时秒的数。|  
|布尔 isAllowEncryptedValueModifications()|指示 allowEncryptedValueModifications 设置是启用还是禁用。|  
|void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)|配置用于包含始终加密列的大容量复制的 allowEncryptedValueModifications 设置。|  
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  
 ISQLServerBulkRecord 接口可用于创建读取来自任何源（如文件）的数据的类，并且允许 SQLServerBulkCopy 实例大容量加载带有该数据的 SQL Server 表。  
  
|接口方法|Description|  
|-----------------------|-----------------|  
|设置\<整数 > getColumnOrdinals()|获取此数据记录中所表示的每个列的序号。|  
|字符串 getColumnName(int column)|获取给定列的名称。|  
|Int getColumnType （int 列）|获取给定列的 JDBC 数据类型。|  
|Int getPrecision （int 列）|获取给定列的精度。|  
|对象 [] getRowData()|获取作为对象数组的当前行的数据。<br /><br /> 每个对象必须匹配 Java 语言类型，该类型用于代表针对给定列指示的 JDBC 数据类型。  有关详细信息，请参阅“‘了解 JDBC 驱动程序数据类型’以获取相应映射”。|  
|Int getScale （int 列）|获取给定列的小数位数。|  
|布尔 isAutoIncrement （int 列）|指示列是否表示一个标识列。|  
|布尔 next （)|前移到下一数据行。|  
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  
 简单实现可用于从分隔文件（其中每一行表示一行数据）中读取基本 Java 数据类型的 ISQLServerBulkRecord 接口。  
  
 实现说明和限制：  
  
1.  因为数据一次读取一行，可用内存将限制任何给定行中允许的最大数据量。  
  
2.  不支持流式处理大型数据类型（例如，varchar(max)、varbinary(max)、nvarchar(max)、sqlxml、ntext）。  
  
3.  为 CSV 文件指定的分隔符不应显示在数据中的任意位置，并且如果该分隔符是 Java 正则表达式中限制使用的字符，应对其正确转义。  
  
4.  在 CSV 文件实现中，将双引号视为数据的一部分。 例如，如果分隔符是逗号，会将行 hello,”world”,”hello,world” 视为带有以下值的四个列：hello、“world”、“hello 和 world”。  
  
5.  新的换行符用作行终止符，并且不允许出现在数据中的任意位置。  
  
|构造函数|Description|  
|-----------------|-----------------|  
|SQLServerBulkCSVFileRecord （字符串 fileToParse、 字符串编码、 字符串分隔符，布尔 firstLineIsColumnNamesSQLServerBulkCSVFileRecord （字符串、 字符串、 字符串、 布尔值）|初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用提供的分隔符和编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，则该文件中的第一行将分析为列名称。  如果编码为 NULL，将使用默认编码。|  
|SQLServerBulkCSVFileRecord (字符串 fileToParse，字符串编码，布尔 firstLineIsColumnNamesSQLServerBulkCSVFileRecord （String，String，布尔值）|初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用逗号分隔符和提供的编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，则该文件中的第一行将分析为列名称。  如果编码为 NULL，将使用默认编码。|  
|SQLServerBulkCSVFileRecord (字符串 fileToParse，布尔 firstLineIsColumnNamesSQLServerBulkCSVFileRecord （字符串、 布尔值）|初始化 SQLServerBulkCSVFileRecord 类的新实例，这将使用逗号分隔符和默认编码分析 fileToParse 中的每一行。 如果 firstLineIsColumnNames 设置为 True，将将文件中的第一行作为列名称来分析。|  
  
|方法|Description|  
|------------|-----------------|  
|Void addColumnMetadata （int positionInFile、 字符串 columnName、 int jdbcType、 int 精度、 int 缩放）|为文件中的给定列添加元数据。|  
|Void close （)|释放与文件读取器关联的任何资源。|  
|Void setTimestampWithTimezoneFormat (DateTim eFormatter dateTimeFormatter|将用于分析来自文件的时间戳数据格式设置为 java.sql.Types.TIMESTAMP_WITH_TIMEZONE。|  
|Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter)|将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。|  
|Void setTimeWithTimezoneFormat (DateTimeForm atter dateTimeFormatter)|将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。|  
|Void setTimeWithTimezoneFormat(String timeFormat)|将用于分析来自文件的时间数据格式设置为 java.sql.Types.TIME_WITH_TIMEZONE。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

