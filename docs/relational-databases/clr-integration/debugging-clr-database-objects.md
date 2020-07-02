---
title: 调试 CLR 数据库对象 |Microsoft Docs
description: SQL Server 提供对在将 SQL Server 调试器与 Microsoft Visual Studio 调试器集成的数据库中调试 Transact-sql 和 CLR 对象的支持。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 7af58a109a658a4af60ca49ad6eea401284782ac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756311"
---
# <a name="debugging-clr-database-objects"></a>调试 CLR 数据库对象
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为调试 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和数据库中的公共语言运行时 (CLR) 对象提供支持。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行调试的主要特点一个是易于设置和使用，另一个是 SQL Server 调试器与 Microsoft Visual Studio 调试器集成。 此外，还可以跨语言进行调试。 用户可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中无缝地单步执行 CLR 对象，反之亦然。 SQL Server Management Studio 中的 Transact-SQL 调试器无法用于调试托管数据库对象，但您可以通过使用 Visual Studio 中的调试器来调试这些对象。 Visual Studio 中的托管数据库对象调试支持所有常见的调试功能，例如，在服务器上执行的例程中的“单步执行”语句和“逐过程”语句。 调试器可以在调试过程中设置断点、检查调用堆栈、检查变量以及修改变量值。 请注意，Visual Studio .NET 2003 无法用于 CLR 集成编程或调试。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含预先安装的 .NET Framework，而 Visual Studio .NET 2003 无法使用 .NET Framework 2.0 程序集。  
  
 有关使用 Visual Studio 调试托管代码的详细信息，请参阅 Visual Studio 文档中的 "[调试托管代码](https://go.microsoft.com/fwlink/?LinkId=120377)" 主题。  
  
## <a name="debugging-permissions-and-restrictions"></a>调试权限和限制  
 调试是一项高度特权的操作，因此只有**sysadmin**固定服务器角色的成员才可以在中执行此操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 调试时存在下列限制：  
  
-   调试 CLR 例程时仅限一次运行一个调试器实例。 存在此限制的原因是，所有 CLR 代码执行在命中断点时都会冻结，并且执行在调试器从断点继续运行之前不会继续。 但是，您可以在其他连接中继续调试 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 尽管 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试不会冻结服务器上的其他执行，但它会因持有锁而导致其他连接等待。  
  
-   无法调试现有连接，只能调试新连接，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在建立连接之前需要客户端和调试器环境的相关信息。  
  
 由于存在上述限制，建议在测试服务器上而不是在生产服务器上调试 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 代码。  
  
## <a name="overview-of-debugging-managed-database-objects"></a>关于调试托管数据库对象的概述  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行的调试遵循单连接模式。 一个调试器只能检测和调试其附加到的客户端连接的活动。 由于调试器的功能不受连接类型的限制，因此表格格式数据流 (TDS) 和 HTTP 连接都可以进行调试。 不过，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许调试现有连接。 调试支持在服务器上执行的例程中使用所有常见的调试功能。 调试器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之间的交互通过分布式组件对象模型 (COM) 进行。  
  
 有关调试托管存储过程、函数、触发器、用户定义类型和聚合的详细信息和方案，请参阅 Visual Studio 文档中的 "[SQL SERVER CLR 集成数据库调试](https://go.microsoft.com/fwlink/?LinkId=120378)" 主题。  
  
 必须对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用 TCP/IP 网络协议，才能使用 Visual Studio 进行远程开发、调试和开发。 有关在服务器上启用 TCP/IP 协议的详细信息，请参阅[配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)。  
  
#### <a name="to-debug-a-managed-database-object"></a>调试托管数据库对象  
  
1.  打开 Microsoft Visual Studio，创建一个新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 项目，并与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的数据库建立连接。  
  
2.  创建一种新类型。 在**解决方案资源管理器**中，右键单击项目，选择 "**添加**" 和 "**新建项 ...** "从 "**添加新项**" 窗口中，选择**存储过程**、**用户定义函数**、**用户定义类型**、**触发器**、**聚合**或**类**。 指定新类型的源文件的名称，然后单击 "**添加**"。  
  
3.  将此新类型的代码添加到文本编辑器中。 有关示例存储过程的示例代码，请参阅本主题后面的部分。  
  
4.  添加测试该类型的脚本。 在**解决方案资源管理器**中，展开**TestScripts**目录双击 "test.txt **" 以打开默认的测试脚本**源文件。 将调用要调试的代码的测试脚本添加到文本编辑器中。 示例脚本见下文。  
  
5.  将一个或多个断点放在源代码中。 在文本编辑器中，右键单击要调试的函数或例程内的代码行，然后选择 "**断点**" 和 "**插入断点**"。 即会添加断点，并以红色突出显示该行代码。  
  
6.  在 "**调试**" 菜单中，选择 "**启动调试**" 以编译、部署和测试项目。 将运行 Test.sql 中的测试脚本，并将调用托管数据库对象。  
  
7.  如果在断点代码执行暂停时出现表示指令指针的黄色箭头，则您可以开始调试托管数据库对象。 可以从 "**调试**" 菜单**单步执行**，将指令指针前进到下一行代码。 "**局部变量**" 窗口用于观察当前由指令指针突出显示的对象的状态。 可以将变量添加到 "**监视**" 窗口。 受监视变量的状态在整个调试会话过程中都可以进行观察，而不是仅当变量位于当前由指令指针突出显示的代码行中时才可以进行观察。 从“调试”菜单中选择“继续”以使指令指针前进到下一个断点或完成例程的执行（如果不再有其他断点）。  
  
### <a name="example"></a>示例  
 下面的示例将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本返回给调用方。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
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
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 下面是调用上面定义的 GetVersion 存储过程的测试脚本。  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 (CLR) 集成编程概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
