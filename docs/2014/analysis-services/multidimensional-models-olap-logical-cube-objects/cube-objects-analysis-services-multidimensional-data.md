---
title: 多维数据集对象 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47befc9fb80f84318cd090bb673b6b6906da6508
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047603"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>多维数据集对象（Analysis Services - 多维数据）
    
## <a name="introducing-cube-objects"></a>多维数据集对象介绍  
 简单 <xref:Microsoft.AnalysisServices.Cube> 对象由基本信息、维度和度量值组组成。 基本信息包括多维数据集的名称、多维数据集的默认度量值、数据源和存储模式等。  
  
 维度集合包含在数据库维度集合的多维数据集中使用的实际维度集。 所有维度都必须先在数据库的维度集合中定义，然后才能在多维数据集中引用。 专有维度中不可用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 度量值组是多维数据集中的度量值集。 度量值组是具有常见数据源视图和维度集的度量值的集合。 度量值组是度量值的处理单元；可先对度量值组进行单独处理，然后再浏览。  
  
## <a name="in-this-section"></a>本节内容  
  
|||  
|-|-|  
|主题||  
|[操作&#40;Analysis Services-多维数据&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[聚合和聚合设计](aggregations-and-aggregation-designs.md)||  
|[计算](calculations.md)||  
|[多维数据集单元&#40;Analysis Services-多维数据&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[多维数据集属性](cube-properties-multidimensional-model-programming.md)||  
|[多维数据集存储&#40;Analysis Services-多维数据&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[多维数据集翻译](cube-translations.md)||  
|[维度关系](dimension-relationships.md)||  
|[关键绩效指标&#40;Kpi&#41;多维模型中](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[度量值和度量值组](../multidimensional-models/measures-and-measure-groups.md)||  
|[分区&#40;Analysis Services-多维数据&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[透视](perspectives.md)||  
  
  
