---
title: "数据库对象 (Analysis Services-多维数据) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], about objects
- SQL Server Analysis Services, objects
- Analysis Services objects, about Analysis Services objects
- SSAS, objects
- Analysis Services objects
- objects [Analysis Services]
ms.assetid: f76d869b-fc1d-4807-9f28-da09c7be382d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32024dc0799fcc7324fd30349a65e741773db66b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="database-objects-analysis-services---multidimensional-data"></a>数据库对象（Analysis Services - 多维数据）
  A [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例都包含数据库对象和程序集用于联机分析处理 (OLAP) 和数据挖掘。  
  
-   数据库包含 OLAP 和数据挖掘对象，例如数据源、数据源视图、多维数据集、度量值、度量值组、维度、属性、层次结构、挖掘结构、挖掘模型和角色。  
  
-   程序集中包含用户定义的函数，这些函数对多维表达式 (MDX) 和数据挖掘扩展插件 (DMX) 语言所提供的内部函数的功能进行了扩展。  
  
 <xref:Microsoft.AnalysisServices.Database> 对象是商业智能项目（如 OLAP 多维数据集、维度和数据挖掘结构）需要的所有数据对象及其支持对象（如 <xref:Microsoft.AnalysisServices.DataSource>、<xref:Microsoft.AnalysisServices.Account> 和 <xref:Microsoft.AnalysisServices.Role>）的容器。  
  
 <xref:Microsoft.AnalysisServices.Database> 对象可提供对包含以下项的对象和属性的访问：  
  
-   可访问的所有多维数据集，以一个集合表示。  
  
-   可访问的所有维度，以一个集合表示。  
  
-   可访问的所有挖掘结构，以一个集合表示。  
  
-   所有数据源和数据源视图，以两个集合表示。  
  
-   所有角色和数据库权限，以两个集合表示。  
  
-   数据库的排序规则值。  
  
-   数据库的估计大小。  
  
-   数据库的语言值。  
  
-   数据库的可见设置。  
  
## <a name="in-this-section"></a>本节内容  
 以下主题介绍 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中 OLAP 和数据挖掘功能共享的对象。  
  
|主题|Description|  
|-----------|-----------------|  
|[多维模型中的数据源](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)|介绍 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的数据源。|  
|[多维模型中的数据源视图](../../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)|介绍 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中基于一个或多个数据源的逻辑数据模型。|  
|[多维模型中的多维数据集](../../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)|介绍多维数据集和多维数据集对象，包括度量值、度量值组、维度用法关系、计算、关键绩效指标 (KPI)、操作、翻译、分区和透视。|  
|[维度 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|介绍维度和维度对象，包括属性、属性关系、层次结构、级别和成员。|  
|[挖掘结构 &#40;Analysis Services-数据挖掘 &#41;](../../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)|介绍挖掘结构和挖掘对象，包括挖掘模型。|  
|[安全角色 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)|介绍一个角色，它是在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中用于对对象的访问进行控制的安全机制。|  
|[多维模型程序集管理](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)|介绍一个程序集，它是在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中用于扩展 MDX 和 DMX 语言的用户定义函数的集合。|  
  
## <a name="see-also"></a>另请参阅  
 [支持的数据源 &#40;SSAS-多维 &#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [多维模型解决方案 &#40;SSAS &#41;](../../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [数据挖掘解决方案](../../../analysis-services/data-mining/data-mining-solutions.md)  
  
  

