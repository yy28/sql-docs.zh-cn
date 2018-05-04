---
title: SqlContext 对象 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 77a390cb4e3ffc0681e5d9251bad41d7274c97ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcontext-object"></a>SqlContext 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当您调用过程或函数，或对公共语言运行时 (CLR) 用户定义类型调用方法，或者当您所执行的操作激发任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 语言中定义的触发器时，您就会调用服务器中的托管代码。 由于在用户连接过程中需要执行此代码，因此需要从服务器上运行的代码访问调用方的上下文。 此外，某些数据访问操作只有在调用方的上下文中运行时才有效。 例如，访问触发器操作中使用的插入和删除的伪表只在调用方的上下文中有效。  
  
 调用方的上下文中提取**SqlContext**对象。 有关详细信息**SqlTriggerContext**方法和属性，请参阅**Microsoft.SqlServer.Server.SqlTriggerContext**类参考文档中的[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SDK。  
  
 **SqlContext**提供对以下组件：  
  
-   **SqlPipe**: **SqlPipe**对象通过结果发送到客户端表示"管道"。 有关详细信息**SqlPipe**对象，请参阅[SqlPipe 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerContext**: **SqlTriggerContext**对象只能从 CLR 触发器中检索。 它提供有关导致触发器被激发的操作的信息，以及所更新的列的映射。 有关详细信息**SqlTriggerContext**对象，请参阅[SqlTriggerContext 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**: **IsAvailable**属性用于确定上下文可用性。  
  
-   **WindowsIdentity**: **WindowsIdentity**属性用于检索调用方的 Windows 标识。  
  
## <a name="determining-context-availability"></a>确定上下文可用性  
 查询**SqlContext**类，以查看当前执行的代码是否正在运行进程内。 若要执行此操作，请检查**IsAvailable**属性**SqlContext**对象。 **IsAvailable**属性是只读的且返回**True**如果调用的代码在内部运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和如果其他**SqlContext**可以访问成员。 如果**IsAvailable**属性返回**False**，所有其他**SqlContext**成员引发**InvalidOperationException**，如果使用. 如果**IsAvailable**返回**False**，任何尝试打开连接对象具有"上下文连接 = true"连接字符串中无法正常工作。  
  
## <a name="retrieving-windows-identity"></a>检索 Windows 标识  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内执行的 CLR 代码始终在进程帐户的上下文中调用。 如果代码应执行某些操作，而不使用的调用用户的标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进程标识，则应通过获得模拟令牌**WindowsIdentity** 属性**SqlContext**对象。 **WindowsIdentity**属性返回**WindowsIdentity**实例表示[!INCLUDE[msCoName](../../includes/msconame-md.md)]调用方，则为 null，如果客户端进行身份验证使用的 Windows 标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 只有程序集标记为**EXTERNAL_ACCESS**或**UNSAFE**权限可以访问此属性。  
  
 获取之后**WindowsIdentity**对象，调用方可以模拟客户端帐户并代表它们执行操作。  
  
 调用方的标识是仅可通过**SqlContext.WindowsIdentity**如果启动存储过程或函数的执行的客户端连接到使用 Windows 身份验证的服务器。 如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则该属性将为 Null，并且该代码无法模拟调用方。  
  
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
 [CLR 触发器](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [SQL Server 进程内专用的 ADO.NET 扩展](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
