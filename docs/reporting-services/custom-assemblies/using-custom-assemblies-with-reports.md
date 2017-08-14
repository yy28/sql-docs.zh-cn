---
title: "与报表中使用自定义程序集 |Microsoft 文档"
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
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0931134ffb0a1511a02a1919d0e68acc55d5f34b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="using-custom-assemblies-with-reports"></a>将自定义程序集用于报表
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，您可以为报表项值、样式和格式设置编写自定义代码。 例如，您可以使用自定义代码基于区域性设置货币的格式，使用特殊格式设置标记某些值，或者为您的公司应用其他实行中的业务规则。 在您的报表中包含此代码的一种方法是创建自定义代码程序集使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ，你可以从引用在报表定义文件中。 报表运行时，服务器将调用自定义程序集中的函数。 自定义程序集可用于检索您计划在报表中使用的指定函数。  
  
## <a name="in-this-section"></a>本節內容  
 [RDL 文件中的引用程序集](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 介绍如何引用报表定义语言文件中的自定义程序集。  
  
 [部署自定义程序集](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 介绍如何将自定义程序集部署到报表设计器和报表服务器。  
  
 [使用具有强名称的自定义程序集](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 介绍如何使用具有强名称的程序集。  
  
 [断言中自定义程序集的权限](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 介绍如何部署具有有限权限和特定权限的自定义程序集，以及如何在代码中断言这些权限。  
  
 [通过表达式访问自定义程序集](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 介绍如何在您的报表定义中将自定义程序集方法作为报表表达式调用。  
  
 [初始化自定义程序集对象](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 介绍如何初始化从报表调用的自定义程序集对象的值。  
  
 [如何： 调试自定义程序集](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 介绍如何调试您的自定义程序集代码。  
  
## <a name="see-also"></a>另请参阅  
 [报表定义语言 &#40;SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
