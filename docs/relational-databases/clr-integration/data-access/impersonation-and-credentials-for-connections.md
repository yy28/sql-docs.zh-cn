---
title: 模拟和连接的凭据 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
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
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 828357e883ddcf1b1aa1792878d1aedc52105f99
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358889"
---
# <a name="impersonation-and-credentials-for-connections"></a>模拟和连接凭据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成中，使用 Windows 身份验证虽然比较复杂，但是比使用 SQL Server 身份验证更为安全。 使用 Windows 身份验证时，请谨记下列注意事项：  
  
 默认情况下，连出至 Windows 的 SQL Server 进程会获得 SQL Server Windows 服务帐户的安全上下文。 但可以将 CLR 函数映射到代理标识上，以便其出站连接具有的安全上下文不同于 Windows 服务帐户的安全上下文。  
  
 在某些情况下，你可能想要使用模拟调用方**SqlContext.WindowsIdentity**属性而不是作为服务帐户运行。 **WindowsIdentity**实例表示调用调用代码和客户端使用 Windows 身份验证时才可用的客户端的标识。 获取后**WindowsIdentity**实例，可以调用**Impersonate**更改线程的安全令牌，然后打开 ADO.NET 连接代表客户端。  
  
 调用 SQLContext.WindowsIdentity.Impersonate 后，不能访问本地数据并不能访问系统数据。 若要访问的数据同样，您必须调用 WindowsImpersonationContext.Undo。  
  
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
>  有关模拟中行为更改的信息，请参阅[SQL Server 2016 中数据库引擎功能的重大更改](../../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 另外，如果获得了 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 标识实例，则默认情况下不能将该实例传播到其他计算机；默认情况下 Windows 安全基础结构会限制这种传播。 然而，存在一种称为“委托”的机制，通过该机制可在多个可信任的计算机之间启用 Windows 标识传播。 您可以了解有关 TechNet 文章中的委派的详细信息"[Kerberos 协议转换和约束委派](http://go.microsoft.com/fwlink/?LinkId=50419)"。  
  
## <a name="see-also"></a>请参阅  
 [SqlContext 对象](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
  
  
