---
title: CLR 事务示例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b09161af-6ac1-406c-9d62-e40be3b4cf8d
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 581510c786e31ab83399bb1ca0d21dd8391ff547
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154978"
---
# <a name="clr-transactions-sample"></a>CLR 事务示例
  此示例说明如何使用 `System.Transactions` 命名空间中的托管 API 来控制事务。 特别需要指出的是，`System.Transactions.TransactionScope` 类用于建立事务边界，以确保只有在库存足以满足需求的情况下才调整库存数据，而且如果存在足够的库存，库存将以原子方式从一个位置传输到另一个位置。 通过将库存中的更改记录到存储在独立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的审核数据库来说明如何在分步式事务中进行自动注册。  
  
## <a name="prerequisites"></a>必要條件  
 若要创建和运行此项目，必须安装下列软件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文档和示例[网站](http://go.microsoft.com/fwlink/?LinkId=31046)免费获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]开发人员[网站](http://go.microsoft.com/fwlink/?linkid=62796)提供的 AdventureWorks 数据库  
  
-   .NET Framework SDK 2.0 或更高版本，或 Microsoft Visual Studio 2005 或更高版本。 您可以免费获取 .NET Framework SDK。  
  
-   此外，还必须满足以下条件：  
  
-   使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须已启用 CLR 集成。  
  
-   若要启用 CLR 集成，请执行以下步骤：  
  
    #### <a name="enabling-clr-integration"></a>启用 CLR 集成  
  
    -   执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  若要启用 CLR，必须具有`ALTER SETTINGS`服务器级权限，其中的成员隐式拥有`sysadmin`和`serveradmin`固定服务器角色的成员。  
  
-   必须在您使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装 AdventureWorks 数据库。  
  
-   如果你不是管理员[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在使用的实例，必须让管理员授予您**CreateAssembly**权限，才能完成安装。  
  
## <a name="building-the-sample"></a>生成示例  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>按照以下说明创建和运行该示例：  
  
1.  打开 Visual Studio 或 .NET Framework 命令提示符。  
  
2.  如有必要，为您的示例创建目录。 对于此示例，我们将使用 C:\MySample。  
  
3.  由于此示例需要签名的程序集，请通过键入以下命令创建一个非对称密钥：  
  
     `sn -k SampleKey.snk`  
  
4.  从命令行提示符执行以下代码之一（具体取决于所选的语言)，对示例代码进行编译。  
  
    -   `Vbc /reference:"C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\v3.5\System.Core.dll","C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\v3.5\System.Data.DataSetExtensions.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Transactions.dll","C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll" /keyfile:Key.snk /target:Library /out:Transaction.dll InventoryMover.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Transactions.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /keyfile:key.snk /out:Transaction.dll /target:library InventoryMover.cs`  
  
5.  将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安装代码复制到一个文件中，并在示例目录中将其另存为 `install.sql`。  
  
6.  通过执行以下命令部署程序集和存储过程：  
  
    -   `sqlcmd -E -I -i install.sql -v root = "C:\MySample\"`  
  
7.  复制[!INCLUDE[tsql](../../includes/tsql-md.md)]到一个文件数据库安装代码并将其保存为`installDB.sql`示例目录中。  
  
8.  通过执行以下命令安装审核数据库：  
  
    -   `Sqlcmd –S server_name [ \instance_name ] -E -I -i installDB.sql`  
  
     （需为实例和服务器提供适当的值。）  
  
9. 复制[!INCLUDE[tsql](../../includes/tsql-md.md)]到一个文件测试命令脚本并将其保存为`test.sql`示例目录中。  
  
10. 使用以下命令执行测试脚本：  
  
    -   `sqlcmd -E -I -i test.sql`  
  
11. 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据库清除脚本复制到一个文件中，并在示例目录中将其另存为 `cleanupDB.sql`。  
  
12. 使用以下命令执行该脚本  
  
    -   `Sqlcmd –S server_name [ \instance_name ] -E -I -i cleanup.sql`  
  
         （需为实例和服务器提供适当的值。）  
  
13. 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除脚本复制到一个文件中，并在示例目录中将其另存为 `cleanup.sql`。  
  
14. 使用以下命令执行该脚本  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>示例代码  
 下面是此示例的代码列表。  
  
 C#  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using System.Transactions;  
using Microsoft.SqlServer.Server;  
using System.Security.Principal;  
  
    public static class InventoryMover  
    {  
        const string contextConnectionString = "context connection=true";  
  
        // **********  
        // Important: Change this connection string to refer to a server other than the one  
        // you have installed the AdventureWorks database.  This sample demonstrates   
        // two-phase commit across multiple servers, and loopback to the same server is not  
        // permitted from CLR integrated based stored procedures.  
        // **********  
        const string auditConnectionString = "server=<YourServer>; database=InventoryAudit; user=<YourUser>; password=<YourPassword>";  
  
        [SqlMethod(DataAccess = DataAccessKind.Read, IsMutator = true)]  
        public static void ExecuteTransfer(int productID, short fromLocationID,  
            short toLocationID, short quantityToTransfer)  
        {  
                       // Establish bounds of the transaction  
            using (TransactionScope transScope = new TransactionScope())  
            {  
                using (SqlConnection adventureworksConnection = new  
                   SqlConnection(contextConnectionString))  
                {  
                    // Opening adventureworksConnection automatically enlists it in the   
                    // TransactionScope as part of the transaction.  
                    adventureworksConnection.Open();  
  
                    SqlCommand checkCommand = adventureworksConnection.CreateCommand();  
                    checkCommand.CommandText = "SELECT TOP 1 Quantity"  
                        + " FROM Production.ProductInventory WITH (REPEATABLEREAD)"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    checkCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    checkCommand.Parameters[0].Value = productID;  
                    checkCommand.Parameters.Add("@LocationID", SqlDbType.Int);  
                    checkCommand.Parameters[1].Value = fromLocationID;  
  
                    object result = checkCommand.ExecuteScalar();  
                    short availableQuantity = (short)result;  
  
                    if (availableQuantity < quantityToTransfer)  
                        //It would be better to throw a custom error, and in some cases to actually  
                        //RAISERROR.  Also, it would be better to map product IDs and location IDs to   
                        //names for the error message.  
                        throw new ArgumentOutOfRangeException("quantityToTransfer",  
                            string.Format("Attempt to transfer {0} of product {1} from"  
                                + " location {2} but only {3} is available.",  
                                quantityToTransfer, productID, fromLocationID,  
                                availableQuantity));  
  
                    //Remove inventory count from source  
                    SqlCommand reduceCommand = adventureworksConnection.CreateCommand();  
                    reduceCommand.CommandText = "UPDATE Production.ProductInventory"  
                        + " SET Quantity = Quantity - @QuantityToTransfer"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    reduceCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    reduceCommand.Parameters[0].Value = productID;  
                    reduceCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt);  
                    reduceCommand.Parameters[1].Value = fromLocationID;  
                    reduceCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt);  
                    reduceCommand.Parameters[2].Value = quantityToTransfer;  
  
                    reduceCommand.ExecuteNonQuery();  
  
                    //Increate inventory count at destination  
                    SqlCommand increaseCommand = adventureworksConnection.CreateCommand();  
                    increaseCommand.CommandText = "UPDATE Production.ProductInventory"  
                        + " SET Quantity = Quantity + @QuantityToTransfer"  
                        + " WHERE ProductID = @ProductID AND LocationID = @LocationID;";  
                    increaseCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                    increaseCommand.Parameters[0].Value = productID;  
                    increaseCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt);  
                    increaseCommand.Parameters[1].Value = toLocationID;  
                    increaseCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt);  
                    increaseCommand.Parameters[2].Value = quantityToTransfer;  
  
                    increaseCommand.ExecuteNonQuery();  
  
                    // Create an audit trail of the inventory transfer.  We must impersonate the  
                    // client credentials in order for this to work.  Otherwise we'd have to  
                    // set up security for the machine account.  
//                    SqlConnection auditConnection = adventureworksConnection;  
                    using (SqlConnection auditConnection = new SqlConnection(auditConnectionString))  
                    {  
                        SqlCommand auditCommand = auditConnection.CreateCommand();  
                        auditCommand.CommandText = "INSERT InventoryChange "  
                            + " (ProductID, FromLocationID, ToLocationID, Quantity) "  
                            + " VALUES (@ProductID, @FromLocationID, @ToLocationID, @Quantity);";  
                        auditCommand.Parameters.Add("@ProductID", SqlDbType.Int);  
                        auditCommand.Parameters[0].Value = productID;  
                        auditCommand.Parameters.Add("@FromLocationID", SqlDbType.SmallInt);  
                        auditCommand.Parameters[1].Value = fromLocationID;  
                        auditCommand.Parameters.Add("@ToLocationID", SqlDbType.SmallInt);  
                        auditCommand.Parameters[2].Value = toLocationID;  
                        auditCommand.Parameters.Add("@Quantity", SqlDbType.SmallInt);  
                        auditCommand.Parameters[3].Value = quantityToTransfer;  
  
                        // Opening auditConnection automatically enlists it in the   
                        // TransactionScope as part of the transaction.  
                        auditConnection.Open();  
                        auditCommand.ExecuteNonQuery();  
                    }  
  
                }  
                //  The Complete method commits the transaction.  
                transScope.Complete();  
            }  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.Data  
Imports System.Data.SqlTypes  
Imports System.Data.SqlClient  
Imports System.Transactions  
Imports Microsoft.SqlServer.Server  
Imports System.Security.Principal  
Imports System.Globalization  
  
Public NotInheritable Class InventoryMover  
    Private Const contextConnectionString As String = "context connection=true"  
  
    Private Sub New()  
  
    End Sub  
  
    ' **********  
    ' Important: Change this connection string to refer to a server other than the one  
    ' you have installed the AdventureWorks database.  This sample demonstrates   
    ' two-phase commit across multiple servers, and loopback to the same server is not  
    ' permitted from CLR integrated based stored procedures.  
    ' **********  
    Private Const auditConnectionString As String = "server=<YourServer>; database=InventoryAudit; user=<YourUser>; password=<YourPassword>"  
    <SqlMethod(DataAccess:=DataAccessKind.Read, IsMutator:=True)> _  
    Public Shared Sub ExecuteTransfer(ByVal productID As Integer, ByVal fromLocationID As Short, _  
        ByVal toLocationID As Short, ByVal quantityToTransfer As Short)  
        ' Establish bounds of the transaction  
        Using transScope As New TransactionScope()  
            Using adventureworksConnection As New SqlConnection(contextConnectionString)  
                ' Opening adventureworksConnection automatically enlists it in the   
                ' TransactionScope as part of the transaction.  
                adventureworksConnection.Open()  
  
                Dim checkCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                checkCommand.CommandText = "SELECT TOP 1 Quantity" _  
                        & " FROM Production.ProductInventory WITH (REPEATABLEREAD)" _  
                        & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                checkCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                checkCommand.Parameters(0).Value = productID  
                checkCommand.Parameters.Add("@LocationID", SqlDbType.Int)  
                checkCommand.Parameters(1).Value = fromLocationID  
  
                Dim result As Object = checkCommand.ExecuteScalar()  
                Dim availableQuantity As Short = CType(result, Short)  
  
                If (availableQuantity < quantityToTransfer) Then  
                    'It would be better to throw a custom error, and in some cases to actually  
                    'RAISERROR.  Also, it would be better to map product IDs and location IDs to   
                    'names for the error message.  
                    Throw New ArgumentOutOfRangeException("quantityToTransfer", _  
                        String.Format(CultureInfo.InvariantCulture, "Attempt to transfer {0} of product {1} from" _  
                        & " location {2} but only {3} is available.", _  
                        quantityToTransfer, productID, fromLocationID, _  
                        availableQuantity))  
                End If  
  
                'Remove inventory count from source  
                Dim reduceCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                reduceCommand.CommandText = "UPDATE Production.ProductInventory" _  
                    & " SET Quantity = Quantity - @QuantityToTransfer" _  
                    & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                reduceCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                reduceCommand.Parameters(0).Value = productID  
                reduceCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt)  
                reduceCommand.Parameters(1).Value = fromLocationID  
                reduceCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt)  
                reduceCommand.Parameters(2).Value = quantityToTransfer  
  
                reduceCommand.ExecuteNonQuery()  
  
                'Increate inventory count at destination  
                Dim increaseCommand As SqlCommand = adventureworksConnection.CreateCommand()  
                increaseCommand.CommandText = "UPDATE Production.ProductInventory" _  
                    & " SET Quantity = Quantity + @QuantityToTransfer" _  
                    & " WHERE ProductID = @ProductID AND LocationID = @LocationID;"  
                increaseCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                increaseCommand.Parameters(0).Value = productID  
                increaseCommand.Parameters.Add("@LocationID", SqlDbType.SmallInt)  
                increaseCommand.Parameters(1).Value = toLocationID  
                increaseCommand.Parameters.Add("@QuantityToTransfer", SqlDbType.SmallInt)  
                increaseCommand.Parameters(2).Value = quantityToTransfer  
  
                increaseCommand.ExecuteNonQuery()  
  
                ' Create an audit trail of the inventory transfer.  We must impersonate the  
                ' client credentials in order for this to work.  Otherwise we'd have to  
                ' set up security for the machine account.  
                'SqlConnection auditConnection = adventureworksConnection  
                Using auditConnection As New SqlConnection(auditConnectionString)  
                    Dim auditCommand As SqlCommand = auditConnection.CreateCommand()  
                    auditCommand.CommandText = "INSERT InventoryChange " _  
                        & " (ProductID, FromLocationID, ToLocationID, Quantity) " _  
                        & " VALUES (@ProductID, @FromLocationID, @ToLocationID, @Quantity);"  
                    auditCommand.Parameters.Add("@ProductID", SqlDbType.Int)  
                    auditCommand.Parameters(0).Value = productID  
                    auditCommand.Parameters.Add("@FromLocationID", SqlDbType.SmallInt)  
                    auditCommand.Parameters(1).Value = fromLocationID  
                    auditCommand.Parameters.Add("@ToLocationID", SqlDbType.SmallInt)  
                    auditCommand.Parameters(2).Value = toLocationID  
                    auditCommand.Parameters.Add("@Quantity", SqlDbType.SmallInt)  
                    auditCommand.Parameters(3).Value = quantityToTransfer  
  
                    ' Opening auditConnection automatically enlists it in the   
                    ' TransactionScope as part of the transaction.  
                    auditConnection.Open()  
                    auditCommand.ExecuteNonQuery()  
  
                End Using  
            End Using  
  
            '  The Complete method commits the transaction.  
            transScope.Complete()  
        End Using  
    End Sub  
End Class  
  
```  
  
 这是[!INCLUDE[tsql](../../includes/tsql-md.md)]安装脚本 (`Install.sql`)，它将程序集部署并在数据库中创建存储的过程。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
  
EXEC('CREATE ASYMMETRIC KEY ExternalSample_Key FROM EXECUTABLE FILE = ''' + @SamplesPath + 'Transaction.dll'';');  
CREATE LOGIN ExternalSample_Login FROM ASYMMETRIC KEY ExternalSample_Key  
GRANT EXTERNAL ACCESS ASSEMBLY TO ExternalSample_Login  
GO  
  
USE AdventureWorks  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = 'C:\MySample\'  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY [Transaction]   
FROM @SamplesPath + 'Transaction.dll'  
WITH permission_set = External_Access;  
GO  
  
CREATE PROCEDURE usp_ExecuteTransfer  
(  
@ProductID int,  
@FromLocationID smallint,  
@ToLocationID smallint,  
@QuantityToTransfer smallint  
)  
AS EXTERNAL NAME [Transaction].[InventoryMover].ExecuteTransfer;  
GO  
```  
  
 这是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安装脚本 (`InstallDB.sql`)，该脚本在第二个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中创建审核数据库。  
  
```  
SET NOCOUNT OFF;  
GO  
  
PRINT CONVERT(varchar(1000), @@VERSION);  
GO  
  
PRINT '';  
PRINT 'Started - ' + CONVERT(varchar, GETDATE(), 121);  
GO  
  
USE [master];  
GO  
  
-- ****************************************  
-- Drop Database  
-- ****************************************  
PRINT '';  
PRINT '*** Dropping Database';  
GO  
  
IF EXISTS (SELECT [name] FROM [master].[sys].[databases] WHERE [name] = N'InventoryAudit')  
    DROP DATABASE [InventoryAudit];  
  
-- If the database has any other open connections close the network connection.  
IF @@ERROR = 3702   
    RAISERROR('[InventoryAudit] database cannot be dropped because there are still other open connections', 127, 127) WITH NOWAIT, LOG;  
GO  
  
-- ****************************************  
-- Create Database  
-- ****************************************  
PRINT '';  
PRINT '*** Creating Database';  
GO  
  
DECLARE   
    @sql_path nvarchar(256),   
    @sql_cmd nvarchar(256);  
  
SELECT @sql_path = SUBSTRING([physical_name], 1, CHARINDEX(N'master.mdf', LOWER([physical_name])) - 1)  
FROM [master].[sys].[master_files]   
WHERE [database_id] = 1   
    AND [file_id] = 1;  
  
-- COLLATE Latin1_General_CS_AS  
EXECUTE (N'CREATE DATABASE [InventoryAudit]   
    ON (NAME = ''InventoryAudit_Data'', FILENAME = N''' + @sql_path + N'InventoryAudit_Data.mdf'', SIZE = 120, FILEGROWTH = 8)   
    LOG ON (NAME = ''InventoryAudit_Log'', FILENAME = N''' + @sql_path + N'InventoryAudit_Log.ldf'' , SIZE = 2, FILEGROWTH = 96);');  
GO  
  
ALTER DATABASE [InventoryAudit]   
SET RECOVERY SIMPLE,   
    ANSI_NULLS ON,   
    ANSI_PADDING ON,   
    ANSI_WARNINGS ON,   
    ARITHABORT ON,   
    CONCAT_NULL_YIELDS_NULL ON,   
    QUOTED_IDENTIFIER ON,   
    NUMERIC_ROUNDABORT OFF,   
    PAGE_VERIFY CHECKSUM,   
    ALLOW_SNAPSHOT_ISOLATION OFF;  
GO  
  
USE [InventoryAudit];  
GO  
  
PRINT '';  
PRINT '*** Creating Table';  
GO  
  
CREATE TABLE [InventoryChange] (  
[InventoryChangeID] int IDENTITY (1, 1) NOT NULL,  
[ProductID] int NOT NULL,  
[FromLocationID] smallint,  
[ToLocationID] smallint,  
[Quantity] smallint NOT NULL  
);  
GO  
  
```  
  
 这是 `test.sql`，该脚本通过执行函数测试该示例。  
  
```  
USE AdventureWorks  
GO  
SELECT 'Before first transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'Before first transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
--Move 12 adjustable race parts (product id 1) from the Tool Crib (location id 1)   
--to Miscellaneous Storage (location id 6).  
EXEC usp_ExecuteTransfer 1, 1, 6, 12  
  
SELECT 'After first transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'After first transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
--Move them back  
EXEC usp_ExecuteTransfer 1, 6, 1, 12  
  
SELECT 'After second transfer quantity of adjustable races at Tool Crib = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 1  
  
SELECT 'After second transfer quantity of adjustable races at Miscellaneous Storage = ', Quantity FROM Production.ProductInventory  
WHERE ProductID = 1 AND LocationID = 6  
  
The following tsql removes the assembly and stored procedure from the database (Cleanup.sql).  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
USE AdventureWorks  
GO  
```  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 从第二个实例中删除审核数据库。  
  
```  
SET NOCOUNT OFF;  
GO  
  
PRINT CONVERT(varchar(1000), @@VERSION);  
GO  
  
PRINT '';  
PRINT 'Started - ' + CONVERT(varchar, GETDATE(), 121);  
GO  
  
USE [master];  
GO  
  
-- ****************************************  
-- Drop Database  
-- ****************************************  
PRINT '';  
PRINT '*** Dropping Database';  
GO  
  
IF EXISTS (SELECT [name] FROM [master].[sys].[databases] WHERE [name] = N'InventoryAudit')  
    DROP DATABASE [InventoryAudit];  
  
-- If the database has any other open connections close the network connection.  
IF @@ERROR = 3702   
    RAISERROR('[InventoryAudit] database cannot be dropped because there are still other open connections', 127, 127) WITH NOWAIT, LOG;  
GO  
```  
  
 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 从数据库中删除程序集和函数。  
  
```  
SE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_ExecuteTransfer')  
DROP PROCEDURE usp_ExecuteTransfer;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'Transaction')  
DROP ASSEMBLY [Transaction];  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
USE AdventureWorks  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时 (CLR) 集成的使用方案和示例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
