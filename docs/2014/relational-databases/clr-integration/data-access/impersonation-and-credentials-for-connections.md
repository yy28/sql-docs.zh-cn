---
title: 连接的模拟和凭据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3311984e1a1a4148ddb2752e4b2356d235dc8b53
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970627"
---
# <a name="impersonation-and-credentials-for-connections"></a>模拟和连接凭据
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成中，使用 Windows 身份验证虽然比较复杂，但是比使用 SQL Server 身份验证更为安全。 使用 Windows 身份验证时，请谨记下列注意事项：  
  
 默认情况下，连出至 Windows 的 SQL Server 进程会获得 SQL Server Windows 服务帐户的安全上下文。 但可以将 CLR 函数映射到代理标识上，以便其出站连接具有的安全上下文不同于 Windows 服务帐户的安全上下文。  
  
 在某些情况下，最好使用 `SqlContext.WindowsIdentity` 属性来模拟调用方，而非作为服务帐户运行。 `WindowsIdentity` 实例表示调用调用代码的客户端的标识，并且仅在客户端使用 Windows 身份验证时才可用。 在已获得 `WindowsIdentity` 实例后，可以调用 `Impersonate` 来更改线程的安全令牌，然后代表客户端打开 ADO.NET 连接。  
  
 调用 SQLContext 后，无法访问本地数据并且无法访问系统数据。 若要再次访问数据，必须调用 WindowsImpersonationContext。  
  
 下面的示例将说明如何使用 `SqlContext.WindowsIdentity` 属性来模拟调用方。  
  
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
>  有关模拟中行为更改的信息，请参阅[SQL Server 2014 中数据库引擎功能的重大更改](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 另外，如果获得了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 标识实例，则默认情况下不能将该实例传播到其他计算机；默认情况下 Windows 安全基础结构会限制这种传播。 然而，存在一种称为“委托”的机制，通过该机制可在多个可信任的计算机之间启用 Windows 标识传播。 你可以在 TechNet 文章 "[Kerberos 协议转换和约束委派](https://go.microsoft.com/fwlink/?LinkId=50419)" 中了解有关委派的详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [SqlContext 对象](../../clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
