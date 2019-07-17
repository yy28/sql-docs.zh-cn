---
title: CLR 集成入门 |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: quickstart
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration]
- namespaces [CLR integration]
- database objects [CLR integration], about CLR integration
- stored procedures [CLR integration]
- common language runtime [SQL Server], about CLR integration
- building database objects [CLR integration], about CLR integration
- common language runtime [SQL Server], stored procedures
- common language runtime [SQL Server], namespaces
- Hello World example [CLR integration]
- library [CLR integration]
ms.assetid: c73e628a-f54a-411a-bfe3-6dae519316cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 15e4a750e2568598fc5db2bab175643b50310db2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138610"
---
# <a name="getting-started-with-clr-integration"></a>CLR 集成入门
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题提供的命名空间和编译使用的数据库对象所需的库概述[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]与.NET Framework 公共语言运行时 (CLR) 集成。 本主题还说明如何编写、编译和运行用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 编写的简单 CLR 存储过程。  
  
## <a name="required-namespaces"></a>所需命名空间  
 与安装开发基本 CLR 数据库对象所需的组件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 CLR 集成功能在称作 system.data.dll 的程序集中公开，该程序集是 .NET Framework 的一部分。 该程序集还在全局程序集缓存 (GAC) 以及 .NET Framework 目录中提供。 对此程序集的引用通常由命令行工具和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 自动添加，因此无需手动添加它。  
  
 system.data.dll 程序集包含以下命名空间，这些命名空间是编译 CLR 数据库对象所必需的：  
  
 `System.Data`  
  
 `System.Data.Sql`  
  
 `Microsoft.SqlServer.Server`  
  
 `System.Data.SqlTypes`  
  
## <a name="writing-a-simple-hello-world-stored-procedure"></a>撰写一个简单的“Hello World”存储过程  
 将以下 Visual C# 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 代码复制并粘贴到某一文本编辑器中，并且将其保存在名为“helloworld.cs”或“helloworld.vb”的文件中。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
  
public class HelloWorldProc  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld(out string text)  
    {  
        SqlContext.Pipe.Send("Hello world!" + Environment.NewLine);  
        text = "Hello world!";  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.Runtime.InteropServices  
  
Public Class HelloWorldProc  
    \<Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(\<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
 这一简单的程序包含针对公共类的单个静态方法。 此方法使用两个新类 **[SqlContext](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.aspx)** 并 **[SqlPipe](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)** ，用于创建托管数据库对象以输出简单的文本消息。 此方法还将字符串“Hello world!”指派 为某一输出参数的值。 此方法可以声明为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的存储过程，然后采用与 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 存储过程相同的方式运行。  
  
 此程序编译为一个库，将其加载到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，并将其作为存储过程运行。  
  
## <a name="compile-the-hello-world-stored-procedure"></a>编译"Hello World"存储过程  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认情况下将安装 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 再分发文件。 这些文件包括 csc.exe 和 vbc.exe，它们是用于 Visual C# 和 Visual Basic 程序的命令行编译器。 为了编译我们的示例，您必须修改路径变量以指向包含 csc.exe 或 vbc.exe 的目录。 下面是 .NET Framework 的默认安装路径。  
  
```  
C:\Windows\Microsoft.NET\Framework\(version)  
```  
  
 Version 包含已安装 .NET Framework 可再发行组件的版本号。 例如：  
  
```  
C:\Windows\Microsoft.NET\Framework\v4.6.1  
```  
  
 一旦将 .NET Framework 目录添加到路径后，您可以使用以下命令将该存储过程示例编译到某一程序集中。 **/Target**选项，可以将其编译到程序集。  
  
 对于 Visual C# 源文件：  
  
```  
csc /target:library helloworld.cs   
```  
  
 对于 Visual Basic 源文件：  
  
```  
vbc /target:library helloworld.vb  
```  
  
 以上命令使用 /target 选项启动 Visual C# 或 Visual Basic 编译器，以指定生成库 DLL。  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>在 SQL Server 中加载并运行“Hello World”存储过程  
 一旦该存储过程示例成功编译后，就可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中测试它。 为此，打开 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 并创建一个新查询，将其连接到适合的测试数据库（例如，AdventureWorks 示例数据库）。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，能否执行公共语言运行时 (CLR) 代码默认设置为 OFF。 可以使用启用 CLR 代码**sp_configure**系统存储过程。 有关详细信息，请参阅 [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md)。  
  
 我们将需要创建该程序集，以便可以访问该存储过程。 对于此示例，我们将假定您已在 C:\ 目录中创建了 helloworld.dll 程序集。 将以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句添加到您的查询中。  
  
```  
CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE  
```  
  
 一旦创建了该程序集后，我们现在就可以通过使用 create procedure 语句访问 HelloWorld 方法。 我们将存储过程称为“hello”：  
  
```  
  
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
 一旦创建该存储过程后，就可以像用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 编写的普通存储过程一样运行该存储过程。 请执行以下命令：  
  
```  
DECLARE @J nchar(25)  
EXEC hello @J out  
PRINT @J  
```  
  
 这将在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 消息窗口中导致以下输出。  
  
```  
Hello world!  
Hello world!  
```  
  
## <a name="removing-the-hello-world-stored-procedure-sample"></a>删除“Hello World”存储过程示例  
 在您完成该存储过程示例的运行后，可以从测试数据库中删除该过程和程序集。  
  
 首先，使用 drop procedure 命令删除该存储过程。  
  
```  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
 一旦该存储过程删除后，就可以删除包含示例代码的程序集。  
  
```  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="see-also"></a>请参阅  
 [CLR 存储过程](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [SQL Server 进程内特定扩展 ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)   
 [调试 CLR 数据库对象](../../../relational-databases/clr-integration/debugging-clr-database-objects.md)   
 [CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
