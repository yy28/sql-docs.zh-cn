---
title: 支持的 .NET Framework 库 |Microsoft Docs
description: 通过 SQL Server 中托管的 CLR，你可以使用支持的 .NET Framework 类库和你向数据库注册的不受支持的库进行创作。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 610dcca5103e4a819b0e6c59629ddd4d510f5469
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756358"
---
# <a name="supported-net-framework-libraries"></a>支持的 .NET Framework 库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  借助驻留在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的公共语言运行时 (CLR)，您可以采用托管代码创作存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合。 利用 .NET Framework 类库中的功能，您可以访问提供字符串操作、高级数学运算、文件访问和密码系统等功能的预建类。 可通过任何托管存储过程、用户定义类型、触发器、用户定义函数或用户定义聚合访问这些类。  
  
> [!NOTE]  
>  如果在全局程序集缓存 (GAC) 中对不支持的程序集提供服务或升级，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 应用程序可能会停止运行。 其原因在于在 GAC 中对库提供服务或升级并不会更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的相应程序集。 如果某一程序集存在于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库和 GAC 中，该程序集的两个副本必须完全匹配。 如果不一致，当 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 集成功能使用该程序集时，将发生错误。 如果你服务或升级 GAC 中同时在数据库中注册的任何程序集（包括不受支持的 .NET Framework 程序集），请确保同时 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通过**ALTER assembly**语句来服务或升级数据库中的程序集副本。 有关详细信息，请参阅[知识库文章 949080](https://support.microsoft.com/kb/949080)。  
  
## <a name="supported-libraries"></a>支持的库  
 从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含一系列支持的 .NET Framework 库，已对这些库进行测试，确保它们满足与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成的可靠性和安全性标准。 在代码中使用支持的库之前，您不需要在服务器上显式注册这些库；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 从全局程序集缓存 (GAC) 中直接加载这些库。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，CLR 集成支持的库/命名空间包括：  
  
-   CustomMarshalers  
-   Microsoft.VisualBasic  
-   Microsoft.VisualC  
-   mscorlib  
-   系统  
-   System.Configuration  
-   System.Core  
-   System.Data  
-   System.Data.OracleClient  
-   System.Data.SqlXml  
-   System.Deployment  
-   System.Security  
-   System.Transactions  
-   System.Web.Services  
-   System.Xml  
-   System.Xml.Linq  

<!--
Any modifications to the list above should be duplicated on the following page:
https://docs.microsoft.com/sql/relational-databases/clr-integration/assemblies-designing#supported-net-framework-assemblies
-->

## <a name="unsupported-libraries"></a>不支持的库  
 通过托管存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合仍可以调用不支持的库。 不受支持的库必须先 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用**CREATE ASSEMBLY**语句在数据库中注册，然后才能在代码中使用。 对于在服务器上注册和运行的任何不支持的库，应检查和测试其安全性和可靠性。  
  
 例如， **microsoft.directoryservices**命名空间不受支持。 您必须向**不安全**的权限注册 System.DirectoryServices.dll 程序集，然后才能从代码中调用它。 不**安全**的权限是必需的，因为**microsoft.directoryservices**命名空间中的类不满足**SAFE**或**EXTERNAL_ACCESS**的要求。 有关详细信息，请参阅[Clr 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)和[Clr 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
