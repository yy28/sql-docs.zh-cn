---
title: SqlPipe 对象 |微软文档
description: 对于在 SQL Server 中运行的 CLR 数据库对象，可以使用 SqlPipe 对象的"发送"方法将结果发送到连接的管道。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 7b95788d37fa8f8c2e57c2b20aa222938c65dc6c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487504"
---
# <a name="sqlpipe-object"></a>SqlPipe 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本中，编写向调用客户端发送结果或输出参数的存储过程（或扩展存储过程）非常常见。  
  
 在[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程中，返回零行或更多行的任何**SELECT**语句都会将结果发送到连接的调用方的"管道"。  
  
 对于在 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行的常见语言运行时 （CLR） 数据库对象，可以使用**SqlPipe**对象的**Send**方法将结果发送到连接的管道。 访问**SqlContext**对象的**Pipe**属性以获取**SqlPipe**对象。 **SqlPipe**类在概念上类似于ASP.NET中的**响应**类。 有关详细信息，请参阅 .NET Framework 软件开发包中的 SqlPipe 类参考文档。  
  
## <a name="returning-tabular-results-and-messages"></a>返回表格结果和消息  
 **SqlPipe**具有一个**Send**方法，该方法有三个重载。 它们分别是：  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **Send**方法将数据直接发送到客户端或调用方。 它通常是使用**SqlPipe**输出的客户端，但在嵌套 CLR 存储过程中，输出使用者也可以是一个存储过程。 例如，Procedure1 使用命令文本“EXEC Procedure2”调用 SqlCommand.ExecuteReader()。 Procedure2 也是托管存储过程。 如果现在 Procedure2 调用 SqlPipe.Send(SqlDataRecord)，则该行被发送到 Procedure1 的读取器，而不是客户端。  
  
 **Send**方法发送一个字符串消息，该字符串消息作为信息消息显示在客户端上，等效于[!INCLUDE[tsql](../../includes/tsql-md.md)]中的 PRINT。 它还可以使用**SqlDataRecord**发送单行结果集，也可以使用**SqlDataReader**发送多行结果集。  
  
 **SqlPipe**对象还具有**Execute 和Send**方法。 此方法可用于执行命令（作为**SqlCommand**对象传递）并将结果直接发送回调用方。 如果已提交的命令中有错误，则将异常发送到管道，但同时将一个副本发送到调用托管代码。 如果调用代码没有捕获异常，它会将堆栈传播到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码并两次出现在输出中。 如果调用代码捕获了异常，则管道使用者仍将看到错误，但不会有重复错误。  
  
 它只能采用与上下文连接关联的 SqlCommand;它只能使用与上下文连接关联的**SqlCommand;** 它不能采用与非上下文连接关联的命令。  
  
## <a name="returning-custom-result-sets"></a>返回自定义结果集  
 托管存储过程可以发送并非来自**SqlDataReader**的结果集。 **SendResultStart**方法以及**SendResultRow**和**SendResultEnd**允许存储过程将自定义结果集发送到客户端。  
  
 **发送结果开始**将**SqlDataRecord**作为输入。 该方法标记结果集的开始，并使用记录元数据构造描述结果集的元数据。 它不发送具有**Send 结果开始**的记录值。 使用**Send结果行**发送的所有后续行必须与该元数据定义匹配。  
  
> [!NOTE]  
>  调用 **"发送结果开始"** 方法后，只能调用 **"发送结果行**"和 **"发送结果结束"。** 调用**SqlPipe**同一实例中的任何其他方法会导致**无效操作异常**。 **Send结果End**将**SqlPipe**设置回可以调用其他方法的初始状态。  
  
### <a name="example"></a>示例  
 **uspGetProductLine**存储过程返回指定产品线中所有产品的名称、产品编号、颜色和标价。 此存储过程接受*prodLine*的精确匹配。  
  
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
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]语句执行**uspGetProduct**过程，该过程返回旅游自行车产品的列表。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>另请参阅  
 [SqlDataRecord 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR 存储过程](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [SQL Server 进程内专用的 ADO.NET 扩展](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
