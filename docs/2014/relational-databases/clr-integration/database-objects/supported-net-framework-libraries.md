---
title: 支持的 .NET Framework 库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 0db38e8bf21d56a0fcd35208920b9ee24b583062
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953467"
---
# <a name="supported-net-framework-libraries"></a>支持的 .NET Framework 库
  借助驻留在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的公共语言运行时 (CLR)，您可以采用托管代码创作存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合。 利用 .NET Framework 类库中的功能，您可以访问提供字符串操作、高级数学运算、文件访问和密码系统等功能的预建类。 可通过任何托管存储过程、用户定义类型、触发器、用户定义函数或用户定义聚合访问这些类。  
  
> [!NOTE]  
>  如果你在全局程序集缓存（GAC）中服务或升级不受支持的程序集，你的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果程序集在 CLR 集成中同时存在，则为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果在 GAC 中提供服务或升级的任何程序集（包括不支持的 .NET Framework 程序集）同时已在数据库中注册，请确保使用 `ALTER ASSEMBLY` 语句对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中的程序集副本同时提供相应服务或升级。 有关详细信息，请参阅[知识库文章 949080](https://support.microsoft.com/kb/949080)。  
  
## <a name="supported-libraries"></a>支持的库  
 从开始 [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] ，提供了受支持的 .NET Framework 库列表，已经过测试，可确保它们满足与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 从全局程序集缓存（GAC）直接加载它们的可靠性和安全性标准。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，CLR 集成支持的库/命名空间包括：  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   系统  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>不支持的库  
 通过托管存储过程、触发器、用户定义函数、用户定义类型和用户定义聚合仍可以调用不支持的库。 必须首先使用 `CREATE ASSEMBLY` 语句在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中注册不支持的库，然后才能在代码中使用它们。 对于在服务器上注册和运行的任何不支持的库，应检查和测试其安全性和可靠性。  
  
 例如，不支持 `System.DirectoryServices` 命名空间。 您必须使用 `UNSAFE` 权限注册 System.DirectoryServices.dll 程序集，然后才能从代码中调用它。 `UNSAFE` 权限是必需的，这是因为 `System.DirectoryServices` 命名空间中的类不满足 `SAFE` 或 `EXTERNAL_ACCESS` 要求。 有关详细信息，请参阅[Clr 集成编程模型限制](clr-integration-programming-model-restrictions.md)和[Clr 集成代码访问安全性](../security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建程序集](../assemblies/creating-an-assembly.md)   
 [CLR 集成代码访问安全性](../security/clr-integration-code-access-security.md)   
 [CLR 集成编程模型限制](clr-integration-programming-model-restrictions.md)  
  
  
