---
title: System.exception 中不允许的类型和成员 |Microsoft Docs
descriptions: SQL Server CLR programming disallows a type or member with some values for the HostProtectionResource enum. This article lists System.Data.dll disallowed values.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: a8f875476d5509c538b2fb47575b94369a5e1186
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81486854"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll 中禁用的类型和成员
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言集成（CLR）编程不允许使用具有指定**HostProtectionAttribute**的类型或成员，其值为**ExternalProcessMgmt**、 **ExternalThreading**、 **MayLeakOnAbort**、 **SecurityInfrastructure**、 **SelfAffectingProcessMgmnt**、 **SelfAffectingThreading**、 **SharedState**、**同步**或**UI** **。** 下表列出了宿主保护属性 (HPA) 值被禁用的 System.Data.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持的 .NET Framework 库](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
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
 [宿主保护属性和 CLR 集成编程](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [不允许的类型和成员在](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Mscorlib.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [系统中不允许的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll 中禁用的类型和成员](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
