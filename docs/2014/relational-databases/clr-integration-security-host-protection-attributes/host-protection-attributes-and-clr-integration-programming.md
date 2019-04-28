---
title: 宿主保护属性和 CLR 集成编程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 68f1f114002ab0ef38c7565a523723a06958048d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874345"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>宿主保护属性和 CLR 集成编程
  公共语言运行时 (CLR) 提供一种机制，用于使用 CLR 宿主（例如从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 开始的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]）可能需要的特定属性对属于 .NET Framework 的托管应用程序编程接口 (API) 进行批注。 这种宿主保护属性 (HPA) 的示例包括：  
  
-   `SharedState`，指示 API 是否公开创建或管理共享状态（例如，静态类字段）的功能。  
  
-   `Synchronization`，指示 API 是否公开在线程之间执行同步的功能。  
  
-   `ExternalProcessMgmt`，指示 API 是否公开控制宿主进程的方法。  
  
 在给定这些属性的基础上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可通过代码访问安全性 (CAS) 指定在宿主环境下不允许的 HPA 的列表。 CAS 要求由以下三个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 权限集之一指定：`SAFE`、`EXTERNAL_ACCESS` 或 `UNSAFE`。 在服务器上使用 `CREATE ASSEMBLY` 语句注册程序集时，将指定这三个安全级别之一。 在 `SAFE` 或 `EXTERNAL_ACCESS` 权限集内执行的代码必须避免应用了 `System.Security.Permissions.HostProtectionAttribute` 属性的特定类型或成员。 有关详细信息，请参阅[创建程序集](../clr-integration/assemblies/creating-an-assembly.md)并[CLR 集成编程模型限制](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
 `HostProtectionAttribute` 与其说是一项安全权限，不如说是一种用于提高可靠性的方法，原因在于它标识宿主可能不允许的特定代码构造（类型或方法）。 使用 `HostProtectionAttribute` 会强制执行可帮助保护宿主稳定性的编程模型。  
  
## <a name="host-protection-attributes"></a>宿主保护属性  
 HPA 可标识不适合宿主编程模型的类型或成员，并表示可靠性威胁的以下递增级别：  
  
-   在其他方面为良性。  
  
-   可能会导致反序列化服务器托管的用户代码。  
  
-   可能会导致反序列化服务器进程本身。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许使用的类型或成员，具有`HostProtectionAttribute`，它指定`System.Security.Permissions.HostProtectionResource`枚举，其中的值`ExternalProcessMgmt`， `ExternalThreading`， `MayLeakOnAbort`， `SecurityInfrastructure`， `SelfAffectingProcessMgmnt`， `SelfAffectingThreading`， `SharedState`， `Synchronization`，或`UI`。 这会阻止程序集调用启用共享状态、执行同步、可能导致终止时资源泄漏或影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的完整性的成员。  
  
### <a name="disallowed-types-and-members"></a>不允许的类型和成员  
 下面的主题标识了其 `HostProtectionResource` 值被 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 禁用的类型和成员。  
  
> [!NOTE]  
>  这些主题中的列表是通过受支持的程序集生成的。  有关详细信息，请参阅[支持的.NET Framework 库](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [Microsoft.VisualBasic.dll 中禁用的类型和成员](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 列出了 Microsoft.VisualBasic.dll 中其 HPA 值被禁用的类型和成员。  
  
 [mscorlib.dll 中禁用的类型和成员](disallowed-types-and-members-in-mscorlib-dll.md)  
 列出了 mscorlib.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-dll.md)  
 列出了 System.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.Data.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-data-dll.md)  
 列出了 System.Data.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.Core.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-core-dll.md)  
 列出了 System.Core.dll 中其 HPA 值被禁用的类型和成员。  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成代码访问安全性](../clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 集成编程模型限制](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [创建程序集](../clr-integration/assemblies/creating-an-assembly.md)  
  
  
