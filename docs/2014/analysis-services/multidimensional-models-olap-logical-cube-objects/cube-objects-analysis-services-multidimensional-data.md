---
title: 多维数据集对象 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 783caa7a2ea334da09ab038694c09795fa3af229
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024928"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>多维数据集对象（Analysis Services - 多维数据）
    
## <a name="introducing-cube-objects"></a>多维数据集对象介绍  
 简单 <xref:Microsoft.AnalysisServices.Cube> 对象由基本信息、维度和度量值组组成。 基本信息包括多维数据集的名称、多维数据集的默认度量值、数据源和存储模式等。  
  
 维度集合包含在数据库维度集合的多维数据集中使用的实际维度集。 所有维度都必须先在数据库的维度集合中定义，然后才能在多维数据集中引用。 专用维度中均不提供[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 度量值组是多维数据集中的度量值集。 度量值组是具有常见数据源视图和维度集的度量值的集合。 度量值组是度量值的处理单元；可先对度量值组进行单独处理，然后再浏览。  
  
## <a name="in-this-section"></a>本节内容  
  
|||  
|-|-|  
|主题||  
|[操作&#40;Analysis Services-多维数据&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[聚合和聚合设计](aggregations-and-aggregation-designs.md)||  
|[计算](calculations.md)||  
|[多维数据集单元格&#40;Analysis Services-多维数据&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[多维数据集属性](cube-properties-multidimensional-model-programming.md)||  
|[多维数据集存储&#40;Analysis Services-多维数据&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[多维数据集翻译](cube-translations.md)||  
|[维度关系](dimension-relationships.md)||  
|[关键绩效指标&#40;Kpi&#41;多维模型中](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[度量值和度量值组](../multidimensional-models/measures-and-measure-groups.md)||  
|[分区&#40;Analysis Services-多维数据&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[透视](perspectives.md)||  
  
  