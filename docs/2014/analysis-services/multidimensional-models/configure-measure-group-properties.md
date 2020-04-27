---
title: 配置度量值组属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7571457847d8ffb0388608b7d634cc19261a609
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076673"
---
# <a name="configure-measure-group-properties"></a>配置度量值组属性
  通过使用度量值组属性，您可以定义度量值组的工作方式。  
  
## <a name="measure-group-properties"></a>度量值组属性  
 度量值组属性确定整个度量值组的行为，并设置度量值组内度量值的某些属性的默认行为。  
  
|属性|定义|  
|--------------|----------------|  
|`AggregationPrefix`|适用于 ROLAP 存储。 将公共前缀分配给 SQL Server 中的索引视图，用于为与此度量值组关联的分区存储聚合。|  
|`DataAggregation`|此属性是保留供将来使用，当前不起任何作用。 因此，建议你不要修改此设置。|  
|`Description`|你可以使用此属性来记录度量值组。|  
|`ErrorConfiguration`|可配置的错误处理设置，用于处理重复键、未知键、空键、错误限制、检测到错误时的操作以及错误日志文件。 请参阅[多维数据集、分区和维度处理的错误配置（SSAS - 多维）](error-configuration-for-cube-partition-and-dimension-processing.md)。|  
|`EstimatedRows`|指定事实数据表中的估计行数。|  
|`EstimatedSize`|指定度量值组的估计大小(字节)。|  
|`ID`|指定对象的标识符。|  
|`IgnoreUnrelatedDimensions`|确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。 默认设置为`True`。|  
|`Name`|度量值的名称。 此属性为只读。|  
|`ProactiveCaching`|可配置的错误处理设置，用于处理重复键、未知键、空键、错误限制、检测到错误时的操作以及错误日志文件。|  
|`ProcessingMode`|指示在处理期间或之后是否进行索引和聚合。 选项是 Regular 和 LazyAggregations。 LazyAggregations 可作为后台任务运行聚合。|  
|`ProcessingPriority`|确定在后台操作（例如，惰性聚合和索引）期间多维数据集的处理优先级。 默认值为 **0**。|  
|`StorageLocation`|度量值组的文件系统存储位置。 如果未指定，则从包含度量值组的多维数据集中继承该位置。|  
|`StorageMode`|度量值组的存储模式。 可用值是 MOLAP、ROLAP 或 HOLAP。|  
|`Type`|指定度量值组的类型。|  
  
  
