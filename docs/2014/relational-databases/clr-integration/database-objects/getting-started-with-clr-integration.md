---
title: 入门与 CLR 集成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
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
manager: craigg
ms.openlocfilehash: db3a72facf1676360e7c338663facac66840a113
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874123"
---
# <a name="getting-started-with-clr-integration"></a>CLR 集成入门
  本主题概述了使用与 .NET Framework 公共语言运行时（CLR）的[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]集成编译数据库对象所需的命名空间和库。 本主题还说明如何编写、编译和运行用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 编写的简单 CLR 存储过程。  
  
## <a name="required-namespaces"></a>所需命名空间  
 从开始[!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)]。 CLR 集成功能在称作 system.data.dll 的程序集中公开，该程序集是 .NET Framework 的一部分。 该程序集还在全局程序集缓存 (GAC) 以及 .NET Framework 目录中提供。 对此程序集的引用通常由命令行工具和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 自动添加，因此无需手动添加它。  
  
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
    <Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
 这一简单的程序包含针对公共类的单个静态方法。 此方法使用两个新类 `SqlContext` 和 `SqlPipe`，用于创建托管数据库对象以输出简单的文本消息。 此方法还将字符串“Hello world!”指派 为某一输出参数的值。 此方法可以声明为存储过程中[!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)]的存储过程。  
  
 我们现在将此程序编译为一个库，将其加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，然后将其作为存储过程运行。  
  
## <a name="compiling-the-hello-world-stored-procedure"></a>编译“Hello World”存储过程  
 [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)]默认情况下，.NET Framework 再分发文件。 这些文件包括 csc.exe 和 vbc.exe，它们是用于 Visual C# 和 Visual Basic 程序的命令行编译器。 为了编译我们的示例，您必须修改路径变量以指向包含 csc.exe 或 vbc.exe 的目录。 下面是 .NET Framework 的默认安装路径。  
  
```  
C:\Windows\Microsoft.NET\Framework\(version)  
```  
  
 Version 包含已安装 .NET Framework 可再发行组件的版本号。 例如：  
  
```  
C:\Windows\Microsoft.NET\Framework\v2.0.31113  
```  
  
 一旦将 .NET Framework 目录添加到路径后，您可以使用以下命令将该存储过程示例编译到某一程序集中。 
  `/target` 选项可用于将其编译到某一程序集中。  
  
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
 成功编译该示例过程后，可以在中[!INCLUDE[ssNoVersion](../../../includes/ssmanstudiofull-md.md)]对其进行测试，并创建新的查询，连接到合适的测试数据库（例如，AdventureWorks 示例数据库）。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，能否执行公共语言运行时 (CLR) 代码默认设置为 OFF。 可以通过使用**sp_configure**系统存储过程来启用 CLR 代码。 有关详细信息，请参阅 [Enabling CLR Integration](../clr-integration-enabling.md)。  
  
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
  
 一旦创建该存储过程后，就可以像用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 编写的普通存储过程一样运行该存储过程。 运行以下命令：  
  
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
  
## <a name="see-also"></a>另请参阅  
 [CLR 存储过程](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [SQL Server ADO.NET 中特定于进程的扩展](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)   
 [调试 CLR 数据库对象](../debugging-clr-database-objects.md)   
 [CLR 集成安全性](../security/clr-integration-security.md)  
  
  
