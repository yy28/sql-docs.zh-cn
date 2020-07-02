---
title: SqlContext 对象 |Microsoft Docs
description: 当你在用户连接中的 SQL Server 中调用托管代码时，将在 SqlContext 对象中抽象访问调用方的上下文。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
ms.openlocfilehash: cc3dc5787693345c531e7afb3384bf093dc17aa6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765440"
---
# <a name="sqlcontext-object"></a>SqlContext 对象
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  当您调用过程或函数，或对公共语言运行时 (CLR) 用户定义类型调用方法，或者当您所执行的操作激发任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 语言中定义的触发器时，您就会调用服务器中的托管代码。 由于在用户连接过程中需要执行此代码，因此需要从服务器上运行的代码访问调用方的上下文。 此外，某些数据访问操作只有在调用方的上下文中运行时才有效。 例如，访问触发器操作中使用的插入和删除的伪表只在调用方的上下文中有效。  
  
 调用方的上下文是在**SqlContext**对象中提取的。 有关**SqlTriggerContext**方法和属性的详细信息，请参阅 SDK 中的**SqlTriggerContext**类参考文档。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  
  
 **SqlContext**提供以下组件的访问权限：  
  
-   **SqlPipe**： **SqlPipe**对象表示结果流到客户端的 "管道"。 有关**SqlPipe**对象的详细信息，请参阅[SqlPipe 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerContext**：只能从 CLR 触发器中检索**SqlTriggerContext**对象。 它提供有关导致触发器被激发的操作的信息，以及所更新的列的映射。 有关**SqlTriggerContext**对象的详细信息，请参阅[SqlTriggerContext 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**： **IsAvailable**属性用于确定上下文可用性。  
  
-   **WindowsIdentity**： **WindowsIdentity**属性用于检索调用方的 Windows 标识。  
  
## <a name="determining-context-availability"></a>确定上下文可用性  
 查询**SqlContext**类，以查看当前正在执行的代码是否在进程中运行。 为此，请检查**SqlContext**对象的**IsAvailable**属性。 **IsAvailable**属性是只读的，如果调用代码在内运行， **True** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且可以访问其他**SqlContext**成员，则返回 True。 如果**IsAvailable**属性返回**False**，则所有其他**SqlContext**成员将引发**InvalidOperationException**（如果使用）。 如果**IsAvailable**返回**False**，则任何打开连接字符串中包含 "context connection = true" 的连接对象的尝试都将失败。  
  
## <a name="retrieving-windows-identity"></a>检索 Windows 标识  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内执行的 CLR 代码始终在进程帐户的上下文中调用。 如果代码应使用调用用户的标识（而不是进程标识）执行某些操作， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则应通过**SqlContext**对象的**WindowsIdentity**属性获取模拟标记。 **WindowsIdentity**属性返回表示调用方的 Windows 标识的**WindowsIdentity**实例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ，如果使用身份验证对客户端进行身份验证，则返回 null [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 只有标记有**EXTERNAL_ACCESS**或**UNSAFE**权限的程序集才能访问此属性。  
  
 获取**WindowsIdentity**对象后，调用方可以模拟客户端帐户并代表其执行操作。  
  
 如果启动了使用 Windows 身份验证连接到服务器的存储过程或函数执行的客户端，则调用方的标识只能通过**SqlContext 获取。** 如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则该属性将为 Null，并且该代码无法模拟调用方。  
  
### <a name="example"></a>示例  
 下面的示例说明如何获取调用客户端的 Windows 标识并模拟该客户端。  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>另请参阅  
 [SqlPipe 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 触发器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [SQL Server 进程内专用的 ADO.NET 扩展](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
