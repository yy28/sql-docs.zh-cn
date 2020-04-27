---
title: CLR 触发器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87d822e97a75bbd08375980fe6a6f0341d8f9c60
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62755255"
---
# <a name="clr-triggers"></a>CLR 触发器
  由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时 (CLR) 集成，因此，您可以使用任何 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 语言来创建 CLR 触发器。 本部分包含通过 CLR 集成实现的触发器的特定信息。 有关触发器的完整讨论，请参阅[DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)。  
  
## <a name="what-are-triggers"></a>什么是触发器？  
 触发器是特殊类型的存储过程，可在执行某个语言事件时自动运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括两种常规类型的触发器：数据操作语言 (DML) 触发器和数据定义语言 (DDL) 触发器。 当 `INSERT`、`UPDATE` 或 `DELETE` 语句修改指定表或视图中的数据时，可以使用 DML 触发器。 DDL 触发器激发存储过程以响应各种 DDL 语句，这些语句主要以 `CREATE`、`ALTER` 和 `DROP` 开头。 DDL 触发器可用于管理任务，例如审核和控制数据库操作。  
  
## <a name="unique-capabilities-of-clr-triggers"></a>CLR 触发器的特有功能  
 采用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编写的触发器具有如下功能：确定已使用 `UPDATE(column)` 和 `COLUMNS_UPDATED()` 函数更新激发视图或表中的哪些列。  
  
 以 CLR 语言编写的触发器在若干重大方面均不同于其他 CLR 集成对象。 CLR 触发器可以执行下列操作：  
  
-   引用 `INSERTED` 和 `DELETED` 表中的数据  
  
-   确定因 `UPDATE` 操作而修改了哪些列  
  
-   访问有关执行 DDL 语句所影响的数据库对象的信息。  
  
 这些功能采用查询语言在内部提供，或者由 `SqlTriggerContext` 类提供。 有关 CLR 集成的优点以及如何在托管代码和[!INCLUDE[tsql](../../includes/tsql-md.md)]之间进行选择的信息，请参阅[clr 集成概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="using-the-sqltriggercontext-class"></a>使用 SqlTriggerContext 类  
 `SqlTriggerContext` 类不能公开构造，只能通过访问 CLR 触发器主体中的 `SqlContext.TriggerContext` 属性获取。 通过调用 `SqlTriggerContext` 属性可以从活动的 `SqlContext` 中获取 `SqlContext.TriggerContext` 类：  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 `SqlTriggerContext` 类提供有关触发器的上下文信息。 该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是 DDL 触发器，则还包括描述触发操作的 XML `EventData` 结构。 有关详细信息，请参阅[EVENTDATA &#40;transact-sql&#41;](/sql/t-sql/functions/eventdata-transact-sql)。  
  
### <a name="determining-the-trigger-action"></a>确定触发器操作  
 获取 `SqlTriggerContext` 之后，可以使用它来确定导致触发器被激发的操作类型。 该信息可通过 `TriggerAction` 类的 `SqlTriggerContext` 属性获得。  
  
 对于 DML 触发器，`TriggerAction` 属性可以是下列值之一：  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete(0x3)  
  
-   对于 DDL 触发器，可能的 TriggerAction 值的列表要长得多。 有关详细信息，请参阅 .NET Framework SDK 中的“TriggerAction 枚举”。  
  
### <a name="using-the-inserted-and-deleted-tables"></a>使用插入的和删除的表  
 DML 触发器语句使用两种特殊的表：**插入**的表和**已删除**的表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动创建和管理这两种表。 您可以使用这两种临时表来测试特定数据修改的影响以及设置 DML 触发器操作条件；但是，不能直接更改表中的数据。  
  
 CLR 触发器可以通过 CLR 进程内提供程序访问**插入**的和**删除**的表。 这是通过从 SqlContext 对象获取 `SqlCommand` 对象来完成的。 例如：  
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>确定更新的列  
 可以使用 `ColumnCount` 对象的 `SqlTriggerContext` 属性确定 UPDATE 操作已修改的列数。 此外，还可以使用 `IsUpdatedColumn` 方法，该方法采用列序号作为输入参数，以便确定是否已更新列。 `True` 值指示已更新此列。  
  
 例如，以下代码段（摘自本主题后面的 EmailAudit 触发器）列出所有已更新的列：  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>访问 DDL 触发器的 EventData  
 像常规触发器一样，DDL 触发器将激发存储过程以响应事件。 但与 DML 触发器不同的是，它们不会为响应针对表或视图的 UPDATE、INSERT 或 DELETE 语句而激发， 而是为响应各种 DDL 语句而激发，这些语句主要以 CREATE、ALTER 和 DROP 开头。 DDL 触发器可用于管理任务，例如审核和监视数据库操作和架构更改。  
  
 `EventData` 类的 `SqlTriggerContext` 属性提供了有关激发 DDL 触发器的事件的信息。 该属性包含一个 `xml` 值。 xml 架构包括下列相关信息：  
  
-   事件时间。  
  
-   在执行触发器期间，连接的系统进程 ID (SPID)。  
  
-   激发触发器的事件类型。  
  
 然后，根据事件类型，该架构还包括其他信息，例如事件发生所在的数据库、发生事件的相关对象以及事件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。  
  
 在下面的示例中，以下 DDL 触发器返回原始 `EventData` 属性。  
  
> [!NOTE]  
>  此处显示了如何使用 `SqlPipe` 对象发送结果和消息，此示例仅用于说明用途，通常，建议您不要将此示例用作对 CLR 触发器进行编程的生产代码。 可能返回其他意外数据，并导致应用程序错误。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
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
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 下面的示例输出是 `EventData` 事件激发 DDL 触发器之后的 `CREATE TABLE` 属性值：  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 除通过 `SqlTriggerContext` 类访问的信息以外，查询仍可以引用在进程内执行的命令的文本中的`COLUMNS_UPDATED` 和插入的/删除的内容。  
  
## <a name="sample-clr-trigger"></a>示例 CLR 触发器  
 在本示例中，请考虑这样一种情况：允许用户选择他们需要的任何 ID，但是您希望知道哪些用户专门输入了电子邮件地址作为 ID。 以下触发器将检测该信息并将其记录到审核表。  
  
> [!NOTE]  
>  此处显示了如何使用 `SqlPipe` 对象发送结果和消息，此示例仅用于说明用途，通常，建议您不要将此示例用作生产代码。 返回的额外数据可能并非预期并可能导致应用程序错误。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
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
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 假定存在具有以下定义的两个表：  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 在[!INCLUDE[tsql](../../includes/tsql-md.md)]中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建触发器的语句如下所示，并且假定已在**SQLCLRTest**当前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中注册程序集 SQLCLRTest。  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>验证和取消无效事务  
 使用触发器验证和取消无效 INSERT、UPDATE 或 DELETE 事务或防止对数据库架构进行更改，这一用法很常见。 如果操作不满足验证条件，将验证逻辑并入触发器并回滚当前事务可以实现上述目的。  
  
 当在触发器内部调用 `Transaction.Rollback` 方法或带有“TRANSACTION ROLLBACK”命令文本的 SqlCommand 时，将引发异常并显示不明确的错误消息，必须在 try/catch 块中包装此方法或命令。 您会看到如下错误消息：  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 应出现该异常，而且需要 try/catch 块才能继续执行代码。 当完成执行触发器代码时，将引发另一个异常。  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 此异常也是预期行为，并且执行激发触发器操作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句前后的 try/catch 块是必需的，以便继续执行。 尽管引发了两个异常，仍可以回滚事务，并且更改不会提交到表中。 CLR 触发器和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 触发器之间的主要区别在于：[!INCLUDE[tsql](../../includes/tsql-md.md)] 触发器可以在回滚事务之后继续执行更多工作。  
  
### <a name="example"></a>示例  
 下面的触发器对表执行简单的 INSERT 语句验证。 如果插入的整数值等于 1，则回滚事务，并且该值不会插入到表中。 所有其他整数值将插入到表中。 请注意，`Transaction.Rollback` 方法前后存在 try/catch 块。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本创建测试表、程序集和托管存储过程。 请注意，两个 INSERT 语句包装在 try/catch 块中，这样可以捕获在完成执行触发器时所引发的异常。  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DML 触发器](../../relational-databases/triggers/dml-triggers.md)   
 [DDL 触发器](../../relational-databases/triggers/ddl-triggers.md)   
 [尝试 .。。CATCH &#40;Transact-sql&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [通过公共语言运行时 &#40;CLR&#41; 集成生成数据库对象](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
