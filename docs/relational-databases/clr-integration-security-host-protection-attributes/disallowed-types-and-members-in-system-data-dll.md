---
title: "不允许类型和成员 System.Data.dll |Microsoft 文档"
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
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9a560a3dc5db0d6c13b5b77e0b0f4c707a4e43a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll 中不允许的类型和成员
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]常见语言集成 (CLR) 编程不允许使用类型或成员有**HostProtectionAttribute** ，它指定**System.Security.Permissions.HostProtectionResource**枚举，其中的值**ExternalProcessMgmt**， **ExternalThreading**， **MayLeakOnAbort**， **SecurityInfrastructure**， **SelfAffectingProcessMgmnt**， **SelfAffectingThreading**， **SharedState**， **同步**，或**UI**。 下表列出了宿主保护属性 (HPA) 值被禁用的 System.Data.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持.NET Framework 库](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|类型或成员|HPA 值|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>另请参阅  
 [宿主保护特性和 CLR 集成编程](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll 中不允许的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [不允许的类型和 mscorlib.dll 中的成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [不允许的类型和成员 System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
