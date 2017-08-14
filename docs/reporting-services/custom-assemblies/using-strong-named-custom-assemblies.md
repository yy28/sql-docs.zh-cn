---
title: "使用具有强名称的自定义程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cf8ee5462bd75ab82ea4296a5b71136cb2eb9ee9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="using-strong-named-custom-assemblies"></a>使用具有强名称的自定义程序集
  强名称标识程序集，它包括程序集的文本名称、由四个部分组成的版本号、区域性信息（如果提供）、公钥以及存储在程序集的清单中的数字签名。 强名称针对公共语言运行时 (CLR) 唯一标识程序集并确保二进制完整性。  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>使用 AllowPartiallyTrustedCallersAttribute  
 若要使用强名称的程序集的报表，必须允许你具有强名称程序集由使用的程序集的部分受信任代码调用**AllowPartiallyTrustedCallers**属性。 你可以使用**AllowPartiallyTrustedCallersAttribute**可允许具有强名称程序集由报表设计器或报表服务器在报表表达式中的调用。 若要允许部分受信任的代码调用具有强名称的程序集，请将以下程序集级别属性添加到程序集属性文件。  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute**仅当应用程序集级别的具有强名称程序集时才有效。 有关应用程序集级别的属性的详细信息，请参阅"将应用属性"中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档。  
  
> [!CAUTION]  
>  当**AllowPartiallyTrustedCallersAttribute**存在，则默认值**FullTrustLinkDemand**安全检查，则可以避免、 使程序集可从任何其他调用部分受信任的程序集。 所有安全检查（包括类级别或方法级别的声明性安全属性）都必须显式声明。  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
