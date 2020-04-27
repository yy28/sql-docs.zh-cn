---
title: 模拟和 CLR 集成安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c32691a065c2bfc43868d6b4105fbf1395a63ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62781125"
---
# <a name="impersonation-and-clr-integration-security"></a>模拟和 CLR 集成安全性
  托管代码访问外部资源时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会自动模拟执行例程所处的当前执行上下文。 `EXTERNAL_ACCESS` 和 `UNSAFE` 程序集中的代码可以显式模拟当前执行上下文。  
  
> [!NOTE]  
>  有关模拟中的行为更改的信息，请参阅[SQL Server 2014 中数据库引擎功能的重大更改](../breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
 进程内数据访问提供程序提供了一个应用程序编程接口 `SqlContext.WindowsIdentity`，该接口可用于检索与当前安全上下文有关的令牌。 `EXTERNAL_ACCESS` 和 `UNSAFE` 程序集中的托管代码可使用此方法检索上下文并使用 .NET Framework `WindowsIdentity.Impersonate` 方法模拟该上下文。 当用户代码显式模拟时，适用下列限制：  
  
-   托管代码处于模拟状态时，不允许进程内数据访问。 代码可以撤消模拟，然后调用进程内数据访问。 请注意，这需要存储原始 `WindowsImpersonationContext` 方法的返回值（`Impersonate` 对象）并对该 `Undo` 调用 `WindowsImpersonationContext` 方法。  
  
     该限制意味着当出现进程内数据访问时，实际它将始终位于该会话当前安全上下文的上下文中。 在托管代码内无法通过显式模拟对此进行修改。  
  
-   为异步执行托管代码（例如通过 `UNSAFE` 程序集创建线程并异步运行代码），从不允许进程内数据访问。 无论是否存在模拟，结果都将为 True。  
  
 当代码在与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的上下文不同的模拟上下文中运行时，无法执行进程内数据访问调用，该代码在进行进程内数据访问调用之前应撤消此模拟上下文。 当从托管代码中进行进程内数据访问时，指向托管代码中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 项的原始执行上下文始终用于授权。  
  
 `EXTERNAL_ACCESS` 程序集和 `UNSAFE` 程序集都使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户访问操作系统资源，除非它们如上所述自动模拟当前的安全上下文。 因此，`EXTERNAL_ACCESS` 程序集的作者需要具有比 `SAFE` 程序集的作者更高的信任级别，该级别由 `EXTERNAL ACCESS` 登录级别权限指定。 只有被信任可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户下运行代码的登录名才应被授予 `EXTERNAL ACCESS` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [模拟和连接凭据](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
