---
title: 配置度量值组属性 |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f7cf2328a6f93ed1c7fe17034af1b42b53baaa39
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="configure-measure-group-properties"></a>配置度量值组属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]度量值组具有使您能够定义度量值组的工作的属性。  
  
## <a name="measure-group-properties"></a>度量值组属性  
 度量值组属性确定整个度量值组的行为，并设置度量值组内度量值的某些属性的默认行为。  
  
|“属性”|定义|  
|--------------|----------------|  
|**AggregationPrefix**|适用于 ROLAP 存储。 将公共前缀分配给 SQL Server 中的索引视图，用于为与此度量值组关联的分区存储聚合。|  
|**DataAggregation**|此属性是保留供将来使用，当前不起任何作用。 因此，建议你不要修改此设置。|  
|**Description**|你可以使用此属性来记录度量值组。|  
|**ErrorConfiguration**|可配置的错误处理设置，用于处理重复键、未知键、空键、错误限制、检测到错误时的操作以及错误日志文件。 请参阅[多维数据集、分区和维度处理的错误配置（SSAS - 多维）](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)。|  
|**EstimatedRows**|指定事实数据表中的估计行数。|  
|**EstimatedSize**|指定度量值组的估计大小(字节)。|  
|**ID**|指定对象的标识符。|  
|**IgnoreUnrelatedDimensions**|确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。 默认设置为 **True**。|  
|**名称**|度量值的名称。 该属性为只读。|  
|**ProactiveCaching**|可配置的错误处理设置，用于处理重复键、未知键、空键、错误限制、检测到错误时的操作以及错误日志文件。|  
|**ProcessingMode**|指示在处理期间或之后是否进行索引和聚合。 选项是 Regular 和 LazyAggregations。 LazyAggregations 可作为后台任务运行聚合。|  
|**ProcessingPriority**|确定在后台操作（例如，惰性聚合和索引）期间多维数据集的处理优先级。 默认值为 **0**。|  
|**StorageLocation**|度量值组的文件系统存储位置。 如果未指定，则从包含度量值组的多维数据集中继承该位置。|  
|**StorageMode**|度量值组的存储模式。 可用值是 MOLAP、ROLAP 或 HOLAP。|  
|**类型**|指定度量值组的类型。|  
  
  
