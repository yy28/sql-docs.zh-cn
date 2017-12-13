---
title: "通过个性化设置扩展 OLAP |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e41858ee929aa38bc043939378f45d35eac755dd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="extending-olap-through-personalizations"></a>通过个性化设置扩展 OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Analysis Services 提供用于与多维表达式 (MDX) 和数据挖掘扩展插件 (DMX) 语言的很多内部函数。 这些函数经过专门设计，可用于完成从标准统计计算到遍历层次结构中的成员的所有任务。 但是，任何复杂且可靠的产品都需要不断地扩展其功能，本产品也不例外。  
  
 因此，Analysis Services 为您提供了向服务实例添加程序集和个性化扩展插件的功能，其目的是在标准功能不能胜任时满足您的业务需要。  
  
## <a name="assemblies"></a>程序集  
 程序集，可以扩展 MDX 和 DMX 的业务功能。 您在诸如动态链接库 (DLL) 这样的库中构建所需的功能，然后将库作为程序集添加到 Analysis Services 的实例或 Analysis Services 数据库。 然后，库中的公共方法对 MDX 和 DMX 表达式、过程、计算、操作和客户端应用程序显示为用户定义函数。  
  
## <a name="personalized-extensions"></a>个性化的扩展  
 SQL Server Analysis Services 个性化扩展插件是实现插件体系结构想法的基础。 Analysis Services 个性化扩展插件是对现有托管程序集体系结构的简单而有效的修改，并在整个 Analysis Services <xref:Microsoft.AnalysisServices.AdomdServer> 对象模型、多维表达式 (MDX) 语法和架构行集中公开。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Analysis Services 个性化设置扩展](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  
