---
title: 使用具有强名称的自定义程序集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: custom-assemblies
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 965c75a16e02d6561da2cf326a74f585e5e8be3a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014804"
---
# <a name="using-strong-named-custom-assemblies"></a>使用具有强名称的自定义程序集
  强名称标识程序集，它包括程序集的文本名称、由四个部分组成的版本号、区域性信息（如果提供）、公钥以及存储在程序集的清单中的数字签名。 强名称针对公共语言运行时 (CLR) 唯一标识程序集并确保二进制完整性。  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>使用 AllowPartiallyTrustedCallersAttribute  
 要将具有强名称的程序集用于报表，必须允许部分受信任的代码使用程序集的 AllowPartiallyTrustedCallers 属性调用具有强名称的程序集。 可以使用 AllowPartiallyTrustedCallersAttribute 以允许报表设计器或报表服务器在报表表达式中调用具有强名称的程序集。 若要允许部分受信任的代码调用具有强名称的程序集，请将以下程序集级别属性添加到程序集属性文件。  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 AllowPartiallyTrustedCallersAttribute 仅当被具有强名称的程序集在程序集级别应用时才生效。 有关在程序集级别应用属性的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文档中的“应用属性”。  
  
> [!CAUTION]  
>  当存在 AllowPartiallyTrustedCallersAttribute 时，将阻止默认的 FullTrustLinkDemand 安全检查，同时可以从任何其他部分受信任的程序集调用该程序集。 所有安全检查（包括类级别或方法级别的声明性安全属性）都必须显式声明。  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
