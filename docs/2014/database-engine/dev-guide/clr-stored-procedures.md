---
title: CLR 存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0949b6fddf1755da48dd7922a4fbda50d4b2787
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111967"
---
# <a name="clr-stored-procedures"></a>CLR 存储过程
  存储过程是不能用于标量表达式的例程。 与标量函数不同，存储过程可以向客户端返回表格结果和消息、调用数据定义语言 (DDL) 和数据操作语言 (DML) 语句并返回输出参数。 有关优点的 CLR 集成和托管代码之间进行选择并[!INCLUDE[tsql](../../includes/tsql-md.md)]，请参阅[CLR 集成概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-stored-procedures"></a>CLR 存储过程的要求  
 在公共语言运行时 (CLR) 中，存储的过程作为实现中的类上的公共静态方法[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]程序集。 该静态方法可以声明为 void，或者返回整数值。 如果它返回某一整数值，则返回的整数将视作来自该存储过程的返回代码。 例如：  
  
 `EXECUTE @return_status = procedure_name`  
  
 @return_status变量将包含该方法返回的值。 如果该方法声明为 void，则返回代码是 0。  
  
 如果该方法具有参数，则 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 实现中的参数数目应与该存储过程的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 声明中使用的参数数目相同。  
  
 传递到 CLR 存储过程的参数可以是在托管代码中具有等效值的任何本机 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型。 对于用于创建该过程的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法，应该使用最合适的等效本机 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型指定这些类型。 有关类型转换的详细信息，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 有关 Tvp 的详细信息，请参阅[使用表值参数&#40;数据库引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="returning-results-from-clr-stored-procedures"></a>从 CLR 存储过程中返回结果  
 信息可通过若干方式从 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 存储过程返回。 这包括输出参数、表格结果和消息。  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>OUTPUT 参数和 CLR 存储过程  
 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程一样，信息可通过使用 OUTPUT 参数从 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 存储过程返回。 用于创建 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] DML 语法与用于创建使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 撰写的存储过程相同。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类中实现代码的相应参数应将传址调用参数用作参数。 请注意，Visual Basic 不支持采用与 Visual C# 的相同方法输出参数。 你必须按引用指定参数并应用\<out （) > 属性以表示输出参数，如以下所示：  
  
```  
Imports System.Runtime.InteropServices  
…  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 以下示例显示通过 OUTPUT 参数返回信息的存储过程。  
  
 C#  
  
```  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 一旦包含以上 CLR 的程序集存储已生成并创建在服务器上，以下过程[!INCLUDE[tsql](../../includes/tsql-md.md)]用于在数据库中，创建过程，并指定*总和*作为输出参数。  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 请注意，*总和*声明为`int`SQL Server 数据类型，并且*值*CLR 存储过程中定义的参数被指定为`SqlInt32`CLR 数据类型。 当调用程序执行 CLR 存储过程时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会自动将转换`SqlInt32`CLR 数据类型设置为`int`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  有关哪些 CLR 数据类型可以和不能转换的详细信息，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
### <a name="returning-tabular-results-and-messages"></a>返回表格结果和消息  
 将表格结果和消息返回到客户端通过 `SqlPipe` 对象执行，该对象通过使用 `Pipe` 类的 `SqlContext` 属性获取。 `SqlPipe` 对象具有 `Send` 方法。 通过调用 `Send` 方法，您可以通过管道将数据传输到调用应用程序。  
  
 下面是 `SqlPipe.Send` 方法的若干重载，包括发送 `SqlDataReader` 的一个方法以及只发送文本字符串的另一个方法。  
  
###### <a name="returning-messages"></a>返回消息  
 使用 `SqlPipe.Send(string)` 可以将消息发送到客户端应用程序。 消息文本限制在 8000 个字符以内。 如果消息超出 8000 个字符，该消息将被截断。  
  
###### <a name="returning-tabular-results"></a>返回表格结果  
 若要将查询的结果直接发送到客户端，请对 `Execute` 对象使用 `SqlPipe` 方法的重载之一。 这是将结果返回到客户端的最高效方法，因为数据不必复制到托管内存即传输到网络缓冲区。 例如：  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 若要通过进程内提供程序发送以前已执行的查询结果（或者使用 `SqlDataReader` 的自定义实现对数据进行预处理），则使用采用 `Send` 的 `SqlDataReader` 方法的重载。 此方法在速度上稍慢于前面所述的直接方法，但它提供更高的灵活性，以便在将数据发送到客户端之前操作数据。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 若要创建动态结果集，请填充该结果集并将其发送到客户端，您可以通过当前连接创建记录并且使用 `SqlPipe.Send` 发送它们。  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 下面是通过 `SqlPipe` 发送表格结果和消息的示例。  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 第一个 `Send` 将消息发送到客户端，第二个则使用 `SqlDataReader` 发送表格结果。  
  
 请注意，这些示例只用于说明用途。 对于执行大量计算的应用程序，CLR 函数比简单的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句更合适。 与前一示例几乎等效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程是：  
  
```  
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  消息和结果集在客户端应用程序中以不同的方式检索。 例如，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]结果集出现在**结果**视图中，而消息出现在**消息**窗格。  
  
 如果以上 Visual C# 代码保存在 MyFirstUdp.cs 文件中并且使用以下语句编译：  
  
```  
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 或者，如果以上 Visual Basic 代码保存在 MyFirstUdp.vb 文件中并且使用以下语句编译：  
  
```  
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，不再支持执行使用 `/clr:pure` 编译的 Visual C++ 数据库对象（例如存储过程）。  
  
 可以使用以下 DDL 注册最终生成的程序集，以及调用的入口点：  
  
```  
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>请参阅  
 [CLR 用户定义函数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 触发器](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
