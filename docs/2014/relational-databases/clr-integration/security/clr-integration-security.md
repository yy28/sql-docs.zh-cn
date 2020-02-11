---
title: CLR 集成安全性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 12ca3fcb00122313c1d1e4aae8b64733be9140c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62918992"
---
# <a name="clr-integration-security"></a>CLR 集成安全性
  [!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)]公共语言运行时（CLR）的安全模型管理并保护在[!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)]语句或在服务器中运行的其他 CLR 对象之间运行的不同类型 clr 和非 CLR 对象之间的访问。 对象之间的调用称为链接。 对这些对象执行的安全检查类型取决于相关的链接类型。  
  
 CLR 集成安全模式可实现以下目的：  
  
-   默认情况下，在上运行托管[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的用户代码。 如果执行有可能损害 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可靠性的操作，则应当受到适当的高级权限的保护。  
  
-   托管用户代码不应当获得对数据库中用户数据或其他用户代码的未经授权访问。 用户定义代码应当在调用该代码的用户会话的安全上下文中运行，且拥有该安全上下文的正确特权。  
  
-   应当有控制来限制用户代码不得访问服务器以外的任何资源，而只能用于本地数据访问和计算。  
  
-   用户定义代码不应能通过在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程中运行而获得对系统资源的未经授权访问。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CLR 的基于代码访问的安全模型。 本节将讨论此组合安全方法的某些优势。  
  
 下表列出了本节的主题。  
  
 [CLR 集成代码访问安全性](clr-integration-code-access-security.md)  
 讨论托管代码的代码访问安全性 (CAS) 模式。  
  
 [宿主保护属性和 CLR 集成编程](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 提供有关 SAFE 和 EXTERNAL_ACCESS 程序集中禁止的宿主保护属性 (HPA) 值的信息。  
  
 [CLR 集成安全性中的链接](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 介绍在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中用户代码段是如何能相互调用的。  
  
 [模拟和 CLR 集成安全性](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 讨论托管代码是如何使用模拟来访问外部资源的。  
  
 [允许部分可信任的调用方](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 讨论当托管方法调用其他程序集中所包含类的方法时所产生的问题。  
  
 [应用程序域和 CLR 集成安全性](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 描述如何将程序集加载到应用程序域。  
  
## <a name="see-also"></a>另请参阅  
 [管理 CLR 集成程序集](../assemblies/managing-clr-integration-assemblies.md)  
  
  
