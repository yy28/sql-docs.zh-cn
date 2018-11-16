---
title: SqlContext 对象 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3293cbed44cc6eeae12c3c48247de8748ddad894
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664865"
---
# <a name="sqlcontext-object"></a>SqlContext 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当您调用过程或函数，或对公共语言运行时 (CLR) 用户定义类型调用方法，或者当您所执行的操作激发任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 语言中定义的触发器时，您就会调用服务器中的托管代码。 由于在用户连接过程中需要执行此代码，因此需要从服务器上运行的代码访问调用方的上下文。 此外，某些数据访问操作只有在调用方的上下文中运行时才有效。 例如，访问触发器操作中使用的插入和删除的伪表只在调用方的上下文中有效。  
  
 调用方的上下文中抽象**SqlContext**对象。 有关详细信息**SqlTriggerContext**方法和属性，请参阅**Microsoft.SqlServer.Server.SqlTriggerContext**类中的参考文档[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SDK。  
  
 **SqlContext**连接可以访问以下组件：  
  
-   **SqlPipe**: **SqlPipe**对象表示通过结果发送到客户端的"管道"。 有关详细信息**SqlPipe**对象，请参阅[SqlPipe 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerContext**: **SqlTriggerContext**对象只能从 CLR 触发器中检索。 它提供有关导致触发器被激发的操作的信息，以及所更新的列的映射。 有关详细信息**SqlTriggerContext**对象，请参阅[SqlTriggerContext 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**: **IsAvailable**属性用于确定上下文可用性。  
  
-   **WindowsIdentity**: **WindowsIdentity**属性用于检索调用方的 Windows 标识。  
  
## <a name="determining-context-availability"></a>确定上下文可用性  
 查询**SqlContext**类，以查看当前执行的代码是否正在运行的进程。 若要执行此操作，请检查**IsAvailable**的属性**SqlContext**对象。 **IsAvailable**属性是只读的并返回**True**如果调用代码运行内部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和其他**SqlContext**成员可访问。 如果**IsAvailable**属性将返回**False**，所有其他**SqlContext**成员引发**InvalidOperationException**，如果使用. 如果**IsAvailable**返回**False**，任何尝试打开的连接对象的具有"上下文连接 = true"的连接字符串中将失败。  
  
## <a name="retrieving-windows-identity"></a>检索 Windows 标识  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内执行的 CLR 代码始终在进程帐户的上下文中调用。 如果代码应执行特定的操作，而不使用调用用户的标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进程标识，则应通过获取模拟标记**WindowsIdentity** 的属性**SqlContext**对象。 **WindowsIdentity**属性将返回**WindowsIdentity**实例表示[!INCLUDE[msCoName](../../includes/msconame-md.md)]调用方，则为 null，如果客户端进行身份验证使用的 Windows 标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 只有程序集标记有**EXTERNAL_ACCESS**或**UNSAFE**权限可以访问此属性。  
  
 获取后**WindowsIdentity**对象，调用方可以模拟客户端帐户并代表他们执行操作。  
  
 调用方的标识才可通过**SqlContext.WindowsIdentity**如果启动执行存储过程或函数的客户端连接到使用 Windows 身份验证服务器。 如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则该属性将为 Null，并且该代码无法模拟调用方。  
  
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
  
## <a name="see-also"></a>请参阅  
 [SqlPipe 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext 对象](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 触发器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [SQL Server 进程内专用的 ADO.NET 扩展](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
