---
title: CLR 表值函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 97ad8e64260d337135a1b0d5cda739d8c81b1799
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62707145"
---
# <a name="clr-table-valued-functions"></a>CLR 表值函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  表值函数是返回表的用户定义函数。  
  
 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过允许您在任何托管语言中定义表值函数以扩展表值函数的功能。 从通过表值函数返回数据**IEnumerable**或**IEnumerator**对象。  
  
> [!NOTE]  
>  对于表值函数返回表类型的列不能包含时间戳列或非 Unicode 字符串数据类型列 (如**char**， **varchar**，和**文本**). 不支持 NOT NULL 约束。  
  
 有关 CLR 表值函数的详细信息，请参阅 MSSQLTips'[简介 SQL Server CLR 表值的函数 ！](https://www.mssqltips.com/sqlservertip/2582/introduction-to-sql-server-clr-table-valued-functions/)  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Transact-SQL 与 CLR 表值函数之间的差异  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表值函数将调用此函数的结果具体化到某个中间表中。 由于它们使用中间表，因此它们可以对于结果支持约束和唯一索引。 当返回大型结果时，这些功能极其有用。  
  
 相比较而言，CLR 表值函数表示一种流替代方法。 此时，不要求在单个表中具体化整个结果集。 **IEnumerable**由调用表值函数时，该查询的执行计划直接调用托管函数返回的对象，并且结果将以递增方式使用。 这种流模型可确保在第一行可用之后立即使用结果，而不是等待填充整个表。 如果返回的行非常多，则这还是一个更好的替代方法，因为它们不必在内存中作为一个整体进行具体化。 例如，可以使用托管表值函数分析文本文件并将其中的每行作为一行返回。  
  
## <a name="implementing-table-valued-functions"></a>实现表值函数  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集中将表值函数作为类的方法实现。 表值函数代码必须实现**IEnumerable**接口。 **IEnumerable**接口在.NET Framework 中定义。 表示数组和.NET Framework 中的集合已实现的类型**IEnumerable**接口。 这样，就可以轻松地编写将集合或数组转换为结果集的表值函数。  
  
## <a name="table-valued-parameters"></a>表值参数  
 表值参数即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 表值参数提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 表值参数还有助于减少到服务器的往返次数。 可以将数据作为表值参数发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 有关表值参数的详细信息，请参阅[使用表值参数（数据引擎）](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="output-parameters-and-table-valued-functions"></a>输出参数和表值函数  
 通过使用输出参数，可以从表值函数返回信息。 在实现代码表值函数中的相应参数应将按引用传递参数用作参数。 请注意，Visual Basic 不支持采用与 Visual C# 的相同方法输出参数。 你必须按引用指定参数并应用\<out （) > 属性以表示输出参数，如以下所示：  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>在 Transact-SQL 中定义表值函数  
 定义 CLR 表值函数的语法是类似于[!INCLUDE[tsql](../../includes/tsql-md.md)]表值函数，通过添加**外部名称**子句。 例如：  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 表值函数用于以相关格式表示数据，以便在查询中进一步处理，例如：  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 在以下情况下，表值函数可以返回表：  
  
-   当从标量输入参数中创建表值函数时。 例如，使用以逗号分隔的数字字符串并将它们透视到某个表中的表值函数。  
  
-   当从外部数据生成表值函数时。 例如，读取事件日志并将其显示为表的表值函数。  
  
 **请注意**的表值函数只能执行数据访问通过[!INCLUDE[tsql](../../includes/tsql-md.md)]查询中的**InitMethod**方法，而不是在**FillRow**方法。 **InitMethod**应该用标记**SqlFunction.DataAccess.Read**特性属性，如果[!INCLUDE[tsql](../../includes/tsql-md.md)]执行查询。  
  
## <a name="a-sample-table-valued-function"></a>示例表值函数  
 下面的表值函数返回系统事件日志中的信息。 此函数采用单个字符串参数，其中包含要读取的事件日志的名称。  
  
###### <a name="sample-code"></a>示例代码  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>声明和使用示例表值函数  
 在编译了示例表值函数后，就可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中声明它，如下所示：  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中不再支持执行使用 /clr:pure 编译的 Visual C++ 数据库对象。 例如，此类数据库对象包含表值函数。  
  
 若要测试此示例，请尝试以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码：  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>示例：返回 SQL Server 查询的结果  
 以下示例演示查询 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表值函数。 本示例使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中的 AdventureWorks 轻型数据库。 请参阅[ https://www.codeplex.com/sqlserversamples ](https://go.microsoft.com/fwlink/?LinkId=87843)有关下载 AdventureWorks 的详细信息。  
  
 将源代码文件命名为 FindInvalidEmails.cs 或 FindInvalidEmails.vb。  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 将源代码编译为 DLL 并将此 DLL 复制到 C 驱动器的根目录下。  然后，执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询。  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
  
