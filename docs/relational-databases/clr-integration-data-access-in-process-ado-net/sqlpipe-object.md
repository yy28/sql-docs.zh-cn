---
title: SqlPipe 对象 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeeb65173b29ab5e0e441789d1c0033a2a59b369
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpipe-object"></a>SqlPipe 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，编写向调用客户端发送结果或输出参数的存储过程（或扩展存储过程）非常常见。  
  
 在[!INCLUDE[tsql](../../includes/tsql-md.md)]任何存储过程，**选择**返回零个或多行语句将结果发送到的连接调用方的"命名管道。"  
  
 有关公共语言运行时 (CLR) 数据库中运行的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以将结果发送给连接的管道使用**发送**方法**SqlPipe**对象。 访问**管道**属性**SqlContext**对象以获取**SqlPipe**对象。 **SqlPipe**类是从概念上讲类似于**响应**类在 ASP.NET 中找到。 有关详细信息，请参阅 .NET Framework 软件开发包中的 SqlPipe 类参考文档。  
  
## <a name="returning-tabular-results-and-messages"></a>返回表格结果和消息  
 **SqlPipe**具有**发送**方法，有三个重载。 它们分别是：  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **发送**方法数据将直接发送到客户端或调用方。 它通常是客户端使用的输出**SqlPipe**，但在嵌套的 CLR 存储过程的情况下，输出使用者也可以是存储的过程。 例如，Procedure1 使用命令文本“EXEC Procedure2”调用 SqlCommand.ExecuteReader()。 Procedure2 也是托管存储过程。 如果现在 Procedure2 调用 SqlPipe.Send(SqlDataRecord)，则该行被发送到 Procedure1 的读取器，而不是客户端。  
  
 **发送**方法发送客户端显示的信息性消息，等效于在打印为一个字符串消息[!INCLUDE[tsql](../../includes/tsql-md.md)]。 它还可以发送单行结果集使用**SqlDataRecord**，或多行结果集使用**SqlDataReader**。  
  
 **SqlPipe**对象还具有**ExecuteAndSend**方法。 此方法可以用于执行命令 (作为传递**SqlCommand**对象) 并将结果直接发送回调用方。 如果已提交的命令中有错误，则将异常发送到管道，但同时将一个副本发送到调用托管代码。 如果调用代码没有捕获异常，它会将堆栈传播到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码并两次出现在输出中。 如果调用代码捕获了异常，则管道使用者仍将看到错误，但不会有重复错误。  
  
 它只能接受**SqlCommand**上下文连接与该键相关联; 它无法接受非上下文连接与关联的命令。  
  
## <a name="returning-custom-result-sets"></a>返回自定义结果集  
 托管的存储的过程可以发送不是来自的结果集**SqlDataReader**。 **SendResultsStart**方法，以及**SendResultsRow**和**SendResultsEnd**，允许要发送到客户端的自定义结果集的存储的过程。  
  
 **SendResultsStart**采用**SqlDataRecord**作为输入。 该方法标记结果集的开始，并使用记录元数据构造描述结果集的元数据。 它不会发送与记录的值**SendResultsStart**。 所有后续的行，使用发送**SendResultsRow**，必须与该元数据定义匹配。  
  
> [!NOTE]  
>  在调用**SendResultsStart**方法仅**SendResultsRow**和**SendResultsEnd**可以调用。 调用的同一个实例中的任何其他方法**SqlPipe**导致**InvalidOperationException**。 **SendResultsEnd**设置**SqlPipe**回可以在其中调用其他方法的初始状态。  
  
### <a name="example"></a>示例  
 **UspGetProductLine**存储的过程返回名称、 产品编号、 颜色和指定的产品行中的所有产品的列表价格。 此存储的过程接受的完全匹配项*prodLine*。  
  
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
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句执行**uspGetProduct**过程，返回的 touring bike 产品列表。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>另请参阅  
 [SqlDataRecord 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR 存储过程](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [SQL Server 进程内专用的 ADO.NET 扩展](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
