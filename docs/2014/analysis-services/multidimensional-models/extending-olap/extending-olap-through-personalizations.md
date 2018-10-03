---
title: 通过个性化设置扩展 OLAP |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Analysis Services, extensibility
ms.assetid: 348e49fc-4390-43c1-9b6c-61b386ff4373
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67e1af257dcdb9700fcdfa6643a50000f9dc845f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092187"
---
# <a name="extending-olap-through-personalizations"></a>通过个性化设置扩展 OLAP
  Microsoft  [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 提供了诸多可用于多维表达式 (MDX) 和数据挖掘扩展插件 (DMX) 语言的内部函数。 这些函数经过专门设计，可用于完成从标准统计计算到遍历层次结构中的成员的所有任务。 但是，任何复杂且可靠的产品都需要不断地扩展其功能，本产品也不例外。  
  
 因此，Analysis Services 为您提供了向服务实例添加程序集和个性化扩展插件的功能，其目的是在标准功能不能胜任时满足您的业务需要。  
  
## <a name="assemblies"></a>程序集  
 程序集，可以扩展 MDX 和 DMX 的业务功能。 您在诸如动态链接库 (DLL) 这样的库中构建所需的功能，然后将库作为程序集添加到 Analysis Services 的实例或 Analysis Services 数据库。 然后，库中的公共方法对 MDX 和 DMX 表达式、过程、计算、操作和客户端应用程序显示为用户定义函数。  
  
## <a name="personalized-extensions"></a>个性化扩展插件  
 SQL Server Analysis Services 个性化扩展插件是实现插件体系结构想法的基础。 Analysis Services 个性化扩展插件是对现有托管程序集体系结构的简单而有效的修改，并在整个 Analysis Services <xref:Microsoft.AnalysisServices.AdomdServer> 对象模型、多维表达式 (MDX) 语法和架构行集中公开。  
  
## <a name="see-also"></a>请参阅  
 [多维模型程序集管理](../multidimensional-model-assemblies-management.md)   
 [Analysis Services 个性化设置扩展](analysis-services-personalization-extensions.md)  
  
  
