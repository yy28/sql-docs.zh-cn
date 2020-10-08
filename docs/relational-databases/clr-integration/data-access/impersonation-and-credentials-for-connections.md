---
title: 连接的模拟和凭据 |Microsoft Docs
description: 在 SQL Server CLR 集成中，你可能想要使用 SqlContext WindowsIdentity 属性在 Windows 身份验证中模拟调用方。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: a6487b61d9c21ee86acad28413fb8a0439731b33
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810823"
---
# <a name="impersonation-and-credentials-for-connections"></a>模拟和连接凭据
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成中，使用 Windows 身份验证虽然比较复杂，但是比使用 SQL Server 身份验证更为安全。 使用 Windows 身份验证时，请谨记下列注意事项：  
  
 默认情况下，连出至 Windows 的 SQL Server 进程会获得 SQL Server Windows 服务帐户的安全上下文。 但可以将 CLR 函数映射到代理标识上，以便其出站连接具有的安全上下文不同于 Windows 服务帐户的安全上下文。  
  
 在某些情况下，你可能想要使用 **SqlContext WindowsIdentity** 属性模拟调用方，而不是作为服务帐户运行。 **WindowsIdentity**实例表示调用调用代码的客户端的标识，仅当客户端使用 Windows 身份验证时才可用。 获取 **WindowsIdentity** 实例后，可以调用 **模拟** 来更改该线程的安全令牌，然后代表客户端打开 ADO.NET 连接。  
  
 调用 SQLContext 后，无法访问本地数据并且无法访问系统数据。 若要再次访问数据，必须调用 WindowsImpersonationContext。  
  
 下面的示例演示如何使用 **SqlContext. WindowsIdentity** 属性模拟调用方。  
  
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
>  有关模拟中行为更改的信息，请参阅 [SQL Server 2016 中数据库引擎功能的重大更改](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 另外，如果获得了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 标识实例，则默认情况下不能将该实例传播到其他计算机；默认情况下 Windows 安全基础结构会限制这种传播。 然而，存在一种称为“委托”的机制，通过该机制可在多个可信任的计算机之间启用 Windows 标识传播。 你可以在 TechNet 文章 "[Kerberos 协议转换和约束委派](/previous-versions/windows/it-pro/windows-server-2003/cc739587(v=ws.10))" 中了解有关委派的详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [SqlContext 对象](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
