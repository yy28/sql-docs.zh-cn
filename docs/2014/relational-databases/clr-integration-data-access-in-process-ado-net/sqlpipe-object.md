---
title: SqlPipe 对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcf462f82d7455f83bb0bee8a3b0af991ec2e7db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62920056"
---
# <a name="sqlpipe-object"></a>SqlPipe 对象
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，编写向调用客户端发送结果或输出参数的存储过程（或扩展存储过程）非常常见。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程中，返回零个或多个行的所有 `SELECT` 语句将结果发送到连接调用方的“管道”中。  
  
 对于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中运行的公共语言运行时 (CLR) 数据库对象，您可以使用 `Send` 对象的 `SqlPipe` 方法将结果发送到连接的管道中。 访问 `Pipe` 对象的 `SqlContext` 属性可以获取 `SqlPipe` 对象。 从概念上来说，`SqlPipe` 类与 ASP.NET 中的 `Response` 类相似。 有关详细信息，请参阅 .NET Framework 软件开发包中的 SqlPipe 类参考文档。  
  
## <a name="returning-tabular-results-and-messages"></a>返回表格结果和消息  
 `SqlPipe` 包含 `Send` 方法，该方法具有三次重载。 它们分别是：  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 `Send` 方法将数据直接发送到客户端或调用方。 通常是客户端使用来自 `SqlPipe` 的输出，但在嵌套 CLR 存储过程的情况下，输出使用者也可以是存储过程。 例如，Procedure1 使用命令文本“EXEC Procedure2”调用 SqlCommand.ExecuteReader()。 Procedure2 也是托管存储过程。 如果现在 Procedure2 调用 SqlPipe.Send(SqlDataRecord)，则该行被发送到 Procedure1 的读取器，而不是客户端。  
  
 `Send` 方法发送的字符串消息在客户端上显示为信息性消息，该方法等效于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 PRINT。 该方法还可以使用 `SqlDataRecord` 发送单行结果集，或者使用 `SqlDataReader` 发送多行结果集。  
  
 `SqlPipe` 对象还具有 `ExecuteAndSend` 方法。 可以使用此方法执行作为 `SqlCommand` 对象传递的命令，并将结果直接回发给调用方。 如果已提交的命令中有错误，则将异常发送到管道，但同时将一个副本发送到调用托管代码。 如果调用代码没有捕获异常，它会将堆栈传播到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码并两次出现在输出中。 如果调用代码捕获了异常，则管道使用者仍将看到错误，但不会有重复错误。  
  
 该方法仅采用与上下文连接关联的 `SqlCommand`；但不能采用与非上下文连接关联的命令。  
  
## <a name="returning-custom-result-sets"></a>返回自定义结果集  
 托管存储过程可以发送并非来自于 `SqlDataReader` 的结果集。 `SendResultsStart` 方法以及 `SendResultsRow` 和 `SendResultsEnd` 允许存储过程将自定义结果集发送到客户端。  
  
 `SendResultsStart` 采用 `SqlDataRecord` 作为输入。 该方法标记结果集的开始，并使用记录元数据构造描述结果集的元数据。 它不会使用 `SendResultsStart` 发送记录的值。 使用 `SendResultsRow` 发送的所有后续行都必须与该元数据定义相匹配。  
  
> [!NOTE]  
>  在调用 `SendResultsStart` 方法之后，只能调用 `SendResultsRow` 和 `SendResultsEnd`。 在同一 `SqlPipe` 实例中调用任何其他方法将导致 `InvalidOperationException`。 `SendResultsEnd` 将 `SqlPipe` 设置回初始状态，您可以在该状态下调用其他方法。  
  
### <a name="example"></a>示例  
 `uspGetProductLine` 存储过程返回指定产品系列中所有产品的名称、产品编号、颜色和标价。 此存储过程接受与*prodLine*完全匹配的项。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句执行 `uspGetProduct` 过程，这将返回旅行登山车产品的列表。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>另请参阅  
 [SqlDataRecord 对象](sqldatarecord-object.md)   
 [CLR 存储过程](../../database-engine/dev-guide/clr-stored-procedures.md)   
 [SQL Server 进程内专用的 ADO.NET 扩展](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
