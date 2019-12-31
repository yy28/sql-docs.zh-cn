---
title: 公共语言运行时（CLR）主机保护特性
description: 公共语言运行时（CLR）提供了一种机制，用于注释作为 .NET Framework 包含某些属性的托管应用程序编程接口（Api）。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: 733e4adc69570dd98e6e0ad5448820607ade6329
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258755"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>宿主保护属性和 CLR 集成编程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  公共语言运行时 (CLR) 提供一种机制，用于使用 CLR 宿主（例如从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 开始的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]）可能需要的特定属性对属于 .NET Framework 的托管应用程序编程接口 (API) 进行批注。 这种宿主保护属性 (HPA) 的示例包括：  
  
-   **SharedState**，它指示 API 是否公开创建或管理共享状态（例如，静态类字段）的功能。  
  
-   **同步**，指示 API 是否公开在线程之间执行同步的功能。  
  
-   **ExternalProcessMgmt**，它指示 API 是否公开控制主机进程的方法。  
  
 在给定这些属性的基础上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可通过代码访问安全性 (CAS) 指定在宿主环境下不允许的 HPA 的列表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ca 要求由以下三个权限集之一指定： **SAFE**、 **EXTERNAL_ACCESS**或**UNSAFE**。 当使用**CREATE assembly**语句在服务器上注册程序集时，将指定这三个安全级别之一。 在**SAFE**或**EXTERNAL_ACCESS**权限集内执行的代码必须避免应用**HostProtectionAttribute**特性的某些类型或成员。 有关详细信息，请参阅[创建程序集](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)和[CLR 集成编程模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
 **HostProtectionAttribute**既不是安全权限，也不是一种提高可靠性的方式，因为它标识宿主可能会禁止的特定代码构造（类型或方法）。 使用**HostProtectionAttribute**会强制实施编程模型，以帮助保护主机的稳定性。  
  
## <a name="host-protection-attributes"></a>宿主保护属性  
 HPA 可标识不适合宿主编程模型的类型或成员，并表示可靠性威胁的以下递增级别：  
  
-   在其他方面为良性。  
  
-   可能会导致反序列化服务器托管的用户代码。  
  
-   可能会导致反序列化服务器进程本身。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不允许使用具有**HostProtectionAttribute**的类型或成员，该类型或成员指定了值为**ExternalProcessMgmt**、 **ExternalThreading**、 **MayLeakOnAbort**、 **SecurityInfrastructure**、 **SelfAffectingProcessMgmnt**、 **SelfAffectingThreading**、 **SharedState**、**同步**或**UI**的**HostProtectionResource**枚举。 这会阻止程序集调用启用共享状态、执行同步、可能导致终止时资源泄漏或影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的完整性的成员。  
  
### <a name="disallowed-types-and-members"></a>不允许的类型和成员  
 以下主题标识了不允许其**HostProtectionResource**值的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]类型和成员。  
  
> [!NOTE]  
>  这些主题中的列表是通过受支持的程序集生成的。  有关详细信息，请参阅[支持的 .NET Framework 库](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [Microsoft.VisualBasic.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 列出了 Microsoft.VisualBasic.dll 中其 HPA 值被禁用的类型和成员。  
  
 [mscorlib.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 列出了 mscorlib.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 列出了 System.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.Data.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 列出了 System.Data.dll 中其 HPA 值被禁用的类型和成员。  
  
 [System.Core.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 列出了 System.Core.dll 中其 HPA 值被禁用的类型和成员。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成代码访问安全性](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 集成编程模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [创建程序集](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
