---
title: SqlContext 对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62920045"
---
# <a name="sqlcontext-object"></a>SqlContext 对象
  当您调用过程或函数，或对公共语言运行时 (CLR) 用户定义类型调用方法，或者当您所执行的操作激发任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 语言中定义的触发器时，您就会调用服务器中的托管代码。 由于在用户连接过程中需要执行此代码，因此需要从服务器上运行的代码访问调用方的上下文。 此外，某些数据访问操作只有在调用方的上下文中运行时才有效。 例如，访问触发器操作中使用的插入和删除的伪表只在调用方的上下文中有效。  
  
 调用方的上下文是在 `SqlContext` 对象中提取的。 有关 `SqlTriggerContext` 方法和属性的详细信息，请参阅 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 中的 `Microsoft.SqlServer.Server.SqlTriggerContext` 类参考文档。  
  
 `SqlContext` 提供了对以下组件的访问：  
  
-   `SqlPipe`：`SqlPipe` 对象表示结果流向客户端时所使用的“管道”。 有关`SqlPipe`对象的详细信息，请参阅[SqlPipe 对象](sqlpipe-object.md)。  
  
-   `SqlTriggerContext`：`SqlTriggerContext` 对象只能从 CLR 触发器内部检索。 它提供有关导致触发器被激发的操作的信息，以及所更新的列的映射。 有关`SqlTriggerContext`对象的详细信息，请参阅[SqlTriggerContext 对象](sqltriggercontext-object.md)。  
  
-   `IsAvailable`：`IsAvailable` 属性用于确定上下文的可用性。  
  
-   `WindowsIdentity`：`WindowsIdentity` 属性用于检索调用方的 Windows 标识。  
  
## <a name="determining-context-availability"></a>确定上下文可用性  
 查询 `SqlContext` 类可查看当前执行的代码是否在进程中运行。 若要执行此项检查，请查看 `IsAvailable` 对象的 `SqlContext` 属性。 `IsAvailable` 属性是只读的，如果调用代码正在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内运行，并且其他 `True` 成员可访问，该属性将返回 `SqlContext`。 如果 `IsAvailable` 属性返回 `False`，所有其他 `SqlContext` 成员都将在使用时引发 `InvalidOperationException`。 如果 `IsAvailable` 返回 `False`，打开连接字符串中具有“context connection=true”的连接对象的任何尝试都会失败。  
  
## <a name="retrieving-windows-identity"></a>检索 Windows 标识  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内执行的 CLR 代码始终在进程帐户的上下文中调用。 如果代码应使用执行调用的用户的标识而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程标识来执行某些操作，则应通过 `WindowsIdentity` 对象的 `SqlContext` 属性获取模拟标记。 `WindowsIdentity` 属性返回表示调用方的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 标识的 `WindowsIdentity` 实例；如果客户端是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行身份验证的，则返回 Null。 只有用 `EXTERNAL_ACCESS` 或 `UNSAFE` 权限标记的程序集才能访问此属性。  
  
 获取 `WindowsIdentity` 对象之后，调用方可以模拟客户端帐户并代表调用方执行操作。  
  
 如果启动存储过程或函数执行的客户端是使用 Windows 身份验证连接到服务器的，则调用方的标识只能通过 `SqlContext.WindowsIdentity` 使用。 如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则该属性将为 Null，并且该代码无法模拟调用方。  
  
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
 [SqlPipe 对象](sqlpipe-object.md)   
 [SqlTriggerContext 对象](sqltriggercontext-object.md)   
 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)   
 [SQL Server 进程内专用的 ADO.NET 扩展](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
