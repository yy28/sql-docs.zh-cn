---
title: "模拟和连接的凭据 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- authentication [CLR integration]
- user impersonation [CLR integration]
- credentials [CLR integration]
- database objects [CLR integration], security
ms.assetid: 293dce7d-1db2-4657-992f-8c583d6e9ebb
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd87459202b3e18af6c16ef16becaccf172eb62e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="impersonation-and-credentials-for-connections"></a>模拟和连接凭据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成中，使用 Windows 身份验证虽然比较复杂，但是比使用 SQL Server 身份验证更为安全。 使用 Windows 身份验证时，请谨记下列注意事项：  
  
 默认情况下，连出至 Windows 的 SQL Server 进程会获得 SQL Server Windows 服务帐户的安全上下文。 但可以将 CLR 函数映射到代理标识上，以便其出站连接具有的安全上下文不同于 Windows 服务帐户的安全上下文。  
  
 在某些情况下，你可能想要通过使用模拟调用方**SqlContext.WindowsIdentity**属性而不是作为服务帐户运行。 **WindowsIdentity**实例表示的调用的调用的代码和客户端使用 Windows 身份验证时才可用的客户端的标识。 您已获得了后**WindowsIdentity**实例，你可以调用**Impersonate**更改线程的安全令牌，然后打开代表客户端的 ADO.NET 连接。  
  
 调用 SQLContext.WindowsIdentity.Impersonate 之后，你无法访问本地数据，并不能访问系统数据。 若要访问数据同样，你必须调用 WindowsImpersonationContext.Undo。  
  
 下面的示例演示如何通过使用模拟调用方**SqlContext.WindowsIdentity**属性。  
  
 Visual C#  
  
```  
WindowsIdentity clientId = null;  
WindowsImpersonationContext impersonatedUser = null;  
  
clientId = SqlContext.WindowsIdentity;  
  
// This outer try block is used to protect from   
// exception filter attacks which would prevent  
// the inner finally block from executing and   
// resetting the impersonation.  
try  
{  
   try  
   {  
      impersonatedUser = clientId.Impersonate();  
      if (impersonatedUser != null)  
         return GetFileDetails(directoryPath);  
         else return null;  
   }  
   finally  
   {  
      if (impersonatedUser != null)  
         impersonatedUser.Undo();  
   }  
}  
catch  
{  
   throw;  
}  
```  
  
> [!NOTE]  
>  有关中模拟的行为更改的信息，请参阅[中 SQL Server 2016 数据库引擎功能的重大更改](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 另外，如果获得了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 标识实例，则默认情况下不能将该实例传播到其他计算机；默认情况下 Windows 安全基础结构会限制这种传播。 然而，存在一种称为“委托”的机制，通过该机制可在多个可信任的计算机之间启用 Windows 标识传播。 你可以了解有关 TechNet 文章中的委派"[Kerberos 协议转换和约束委派](http://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>另请参阅  
 [SqlContext 对象](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
