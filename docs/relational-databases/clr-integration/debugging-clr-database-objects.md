---
title: " (CLR) 数据库对象调试公共语言运行时"
description: SQL Server 提供对在将 SQL Server 调试器与 Microsoft Visual Studio 调试器集成的数据库中调试 Transact-sql 和 CLR 对象的支持。
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 1be293f98a3b78280b16f80ab7dcfcb656f7e0ec
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196888"
---
# <a name="how-to-debug-clr-database-objects"></a>如何调试 CLR 数据库对象

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为调试 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和数据库中的公共语言运行时 (CLR) 对象提供支持。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行调试的主要特点一个是易于设置和使用，另一个是 SQL Server 调试器与 Microsoft Visual Studio 调试器集成。 此外，还可以跨语言进行调试。 用户可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中无缝地单步执行 CLR 对象，反之亦然。 SQL Server Management Studio 中的 Transact-SQL 调试器无法用于调试托管数据库对象，但您可以通过使用 Visual Studio 中的调试器来调试这些对象。 Visual Studio 中的托管数据库对象调试支持所有常见的调试功能，例如，在服务器上执行的例程中的“单步执行”语句和“逐过程”语句。 调试器可以在调试过程中设置断点、检查调用堆栈、检查变量以及修改变量值。 

> [!NOTE]
> Visual Studio .NET 2003 不能用于 CLR 集成编程或调试。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含预先安装的 .NET Framework，而 Visual Studio .NET 2003 无法使用 .NET Framework 2.0 程序集。  
  
## <a name="debugging-permissions-and-restrictions"></a>调试权限和限制

调试是一项高度特权的操作，因此只有 **sysadmin** 固定服务器角色的成员才可以在中执行此操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
调试时存在下列限制：  
  
- 调试 CLR 例程时仅限一次运行一个调试器实例。 存在此限制的原因是，所有 CLR 代码执行在命中断点时都会冻结，并且执行在调试器从断点继续运行之前不会继续。 但是，您可以在其他连接中继续调试 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 尽管 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试不会冻结服务器上的其他执行，但它会因持有锁而导致其他连接等待。  
  
- 无法调试现有连接，只能调试新连接，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在建立连接之前需要客户端和调试器环境的相关信息。  
  
由于存在上述限制，建议在测试服务器上而不是在生产服务器上调试 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 代码。  
  
## <a name="overview"></a>概述

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行的调试遵循单连接模式。 一个调试器只能检测和调试其附加到的客户端连接的活动。 由于调试器的功能不受连接类型的限制，因此表格格式数据流 (TDS) 和 HTTP 连接都可以进行调试。 不过，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许调试现有连接。 调试支持在服务器上执行的例程中使用所有常见的调试功能。 调试器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之间的交互通过分布式组件对象模型 (COM) 进行。  
  
有关调试托管存储过程、函数、触发器、用户定义类型和聚合的详细信息和方案，请参阅 Visual Studio 文档中的 [SQL SERVER CLR 集成数据库调试](/previous-versions/ms165050(v=vs.100)) 。  
  
必须对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用 TCP/IP 网络协议，才能使用 Visual Studio 进行远程开发、调试和开发。 有关在服务器上启用 TCP/IP 协议的详细信息，请参阅 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)。  
  
## <a name="debugging-steps"></a>调试步骤

使用以下步骤在 Microsoft Visual Studio 中调试 CLR 数据库对象：

1. 打开 Microsoft Visual Studio，然后创建新的 SQL Server 项目。 可以使用随 Visual Studio 一起提供的 SQL LocalDB 实例。

2.  (c # ) 创建新的 SQL CLR 类型：

   1. 在 **解决方案资源管理器**中，右键单击项目，然后选择 " **添加**"、" **新建项 ...**"。 
   1. 从 " **添加新项** " 窗口中，选择 " **Sql Clr c # 存储过程**"、" **Sql clr c # User-Defined 函数**、 **sql CLR c # User-Defined 类型**、 **Sql Clr c # 触发器**、 **sql clr c # 聚合**或 **类**"。
   1. 指定新类型的源文件的名称，然后选择 " **添加**"。

3. 将此新类型的代码添加到文本编辑器中。 有关示例存储过程的示例代码，请参阅本文中的以下示例部分。

4. 添加用于测试类型的脚本： 

   1. 在 **解决方案资源管理器**中，右键单击项目节点，然后选择 " **添加**"、" **脚本 ...**"。 
   1. 在 " **添加新项** " 窗口中，选择 " **脚本 (不在生成) 中 **"，然后指定一个名称，例如 `Test.sql` 。 选择“添加”按钮。
   1. 在 **解决方案资源管理器**中，双击该 `Test.sql` 节点以打开默认测试脚本源文件。
   1. 将 (调用要调试的代码的测试脚本添加) 到文本编辑器。 有关示例脚本，请参阅下一部分中的示例。

5. 将一个或多个断点放在源代码中。 右键单击要调试的函数或例程的文本编辑器中的代码行。 选择 " **断点**"、" **插入断点**"。 即会添加断点，并以红色突出显示该行代码。

6. 在 " **调试** " 菜单中，选择 " **启动调试** " 以编译、部署和测试项目。 中的测试脚本 `Test.sql` 将运行，并调用托管数据库对象。

7. 当黄色箭头 (指定指令指针) 出现在断点处时，代码执行会暂停。 然后，可以调试托管数据库对象：

   1. 使用 "**调试**" 菜单中的 "**逐过程**" 将指令指针前进到下一行代码。
   1. 使用 " **局部变量** " 窗口可查看当前由指令指针突出显示的对象的状态。
   1. 将变量添加到 " **监视** " 窗口。 即使变量不是指令指针当前突出显示的代码行，您也可以观察整个调试会话中受监视的变量的状态。 
   1. 从 "**调试**" 菜单中选择 "**继续**"，以使指令指针前进到下一个断点，或在没有断点时完成例程的执行。
  
## <a name="example-code"></a>示例代码

下面的示例将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本返回给调用方。  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>示例测试脚本

下面的测试脚本显示了如何调用 `GetVersion` 上一个示例中定义的存储过程。  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>后续步骤
  
有关使用 Visual Studio 调试托管代码的详细信息，请参阅 Visual Studio 文档中的 [调试托管代码](/visualstudio/debugger/debugging-managed-code) 。  

有关详细信息，请参阅 [公共语言运行时集成编程概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
