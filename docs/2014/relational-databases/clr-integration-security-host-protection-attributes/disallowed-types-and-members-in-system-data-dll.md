---
title: 不允许类型和成员 System.Data.dll |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7c222c10fe13a422e5195970057fbb623cc960a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024841"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>System.Data.dll 中不允许的类型和成员
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公共语言集成 (CLR) 编程不允许使用类型或成员有`HostProtectionAttribute`，它指定`System.Security.Permissions.HostProtectionResource`枚举，其中的值`ExternalProcessMgmt`， `ExternalThreading`， `MayLeakOnAbort`， `SecurityInfrastructure`， `SelfAffectingProcessMgmnt`，`SelfAffectingThreading`， **SharedState**， `Synchronization`，或`UI`。 下表列出了宿主保护属性 (HPA) 值被禁用的 System.Data.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持.NET Framework 库](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [宿主保护特性和 CLR 集成编程](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll 中不允许的类型和成员](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [不允许的类型和 mscorlib.dll 中的成员](disallowed-types-and-members-in-mscorlib-dll.md)   
 [不允许的类型和成员 System.dll](disallowed-types-and-members-in-system-dll.md)   
 [System.Core.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-core-dll.md)  
  
  