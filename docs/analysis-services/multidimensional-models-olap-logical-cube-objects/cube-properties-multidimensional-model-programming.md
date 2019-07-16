---
title: 多维数据集属性-多维模型编程 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85453133ab9facd9f3ed56ad98fa2761ac527e40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209374"
---
# <a name="cube-properties---multidimensional-model-programming"></a>多维数据集属性 - 多维模型编程
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以在多维数据集中设置很多属性以影响整个多维数据集的行为。 下表总结了这些属性。  
  
> [!NOTE]  
>  某些属性是在创建多维数据集时自动设置的，不能更改。  
  
 有关如何设置多维数据集属性的详细信息，请参阅[多维数据集设计器&#40;Analysis Services-多维数据&#41;](http://msdn.microsoft.com/library/a6692467-da88-4312-8b03-d812f2ae5a96)。  
  
|属性|描述|  
|--------------|-----------------|  
|**AggregationPrefix**|指定用于聚合名称的通用前缀。|  
|**排序规则**|指定以下划线分隔的区域设置标识符 (LCID) 和比较标志，例如 Latin1_General_C1_AS。|  
|**DefaultMeasure**|包含定义多维数据集的默认度量值的多维表达式 (MDX)。|  
|**说明**|提供多维数据集的说明，可以在客户端应用程序中显示。|  
|**ErrorConfiguration**|包含可配置的错误处理设置，用于处理重复键、未知键、错误限制以及检测到错误时执行的操作、错误日志文件和空键处理。|  
|**EstimatedRows**|指定多维数据集中的估计行数。|  
|**ID**|包含多维数据集的唯一标识符 (ID)。|  
|**语言**|指定多维数据集的默认语言标识符。|  
|**名称**|指定多维数据集的用户友好名称。|  
|**ProactiveCaching**|定义多维数据集的主动缓存设置。|  
|**ProcessingMode**|指示在处理期间或之后是否进行索引和聚合。 选项包括**常规**或**延迟**。|  
|**ProcessingPriority**|确定在后台操作（例如，惰性聚合和索引）期间多维数据集的处理优先级。 默认值为 **0**。|  
|**ScriptCacheProcessingMode**|指示在处理期间或之后是否生成脚本缓存。 选项包括**常规**并**延迟**。|  
|**ScriptErrorHandlingMode**|确定错误处理。 选项包括**IgnoreNone**或**IgnoreAll**|  
|**数据源**|显示用于多维数据集的数据源视图|  
|**StorageLocation**|指定多维数据集的文件系统存储位置。 如果未指定任何位置，则从包含多维数据集对象的数据库中继承位置。|  
|**StorageMode**|指定多维数据集的存储模式。 值为**MOLAP**， **ROLAP**，或**HOLAP**。|  
|**Visible**|确定多维数据集的可见性。|  
  
> [!NOTE]  
>  有关处理 null 值和其他数据完整性问题时设置 ErrorConfiguration 属性的值的详细信息，请参阅[在 Analysis Services 2005 中处理数据完整性问题](http://go.microsoft.com/fwlink/?LinkId=81891)。  
  
## <a name="see-also"></a>请参阅  
 [主动缓存&#40;分区&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)  
  
  
