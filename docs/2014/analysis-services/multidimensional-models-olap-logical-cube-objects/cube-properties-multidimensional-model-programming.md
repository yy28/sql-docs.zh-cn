---
title: 多维数据集属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
author: minewiskan
ms.author: owend
ms.openlocfilehash: 27d4202774107795eaddf76c27e21010d534d977
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545249"
---
# <a name="cube-properties"></a>多维数据集属性
  可以在多维数据集中设置很多属性以影响整个多维数据集的行为。 下表总结了这些属性。  
  
> [!NOTE]  
>  某些属性是在创建多维数据集时自动设置的，不能更改。  
  
 有关如何设置多维数据集属性的详细信息，请参阅[多维数据集设计器 &#40;Analysis Services 多维数据&#41;](../cube-designer-analysis-services-multidimensional-data.md)。  
  
|属性|说明|  
|--------------|-----------------|  
|`AggregationPrefix`|指定用于聚合名称的通用前缀。|  
|`Collation`|指定以下划线分隔的区域设置标识符 (LCID) 和比较标志，例如 Latin1_General_C1_AS。|  
|`DefaultMeasure`|包含定义多维数据集的默认度量值的多维表达式 (MDX)。|  
|`Description`|提供多维数据集的说明，可以在客户端应用程序中显示。|  
|`ErrorConfiguration`|包含可配置的错误处理设置，用于处理重复键、未知键、错误限制以及检测到错误时执行的操作、错误日志文件和空键处理。|  
|`EstimatedRows`|指定多维数据集中的估计行数。|  
|`ID`|包含多维数据集的唯一标识符 (ID)。|  
|`Language`|指定多维数据集的默认语言标识符。|  
|`Name`|指定多维数据集的用户友好名称。|  
|`ProactiveCaching`|定义多维数据集的主动缓存设置。|  
|`ProcessingMode`|指示在处理期间或之后是否进行索引和聚合。 选项为**常规**或 `lazy` 。|  
|`ProcessingPriority`|确定在后台操作（例如，惰性聚合和索引）期间多维数据集的处理优先级。 默认值为**0**。|  
|`ScriptCacheProcessingMode`|指示在处理期间或之后是否生成脚本缓存。 选项为 "**常规**" 和 `lazy` 。|  
|`ScriptErrorHandlingMode`|确定错误处理。 选项是 `IgnoreNone` 或 `IgnoreAll`|  
|`Source`|显示用于多维数据集的数据源视图|  
|`StorageLocation`|指定多维数据集的文件系统存储位置。 如果未指定任何位置，则从包含多维数据集对象的数据库中继承位置。|  
|`StorageMode`|指定多维数据集的存储模式。 值为 `MOLAP` 、 `ROLAP` 或`HOLAP``.`|  
|`Visible`|确定多维数据集的可见性。|  
  
> [!NOTE]  
>  有关在处理 null 值和其他数据完整性问题时设置 ErrorConfiguration 属性的值的详细信息，请参阅[处理 Analysis Services 2005 中的数据完整性问题](https://go.microsoft.com/fwlink/?LinkId=81891)。  
  
## <a name="see-also"></a>另请参阅  
 [主动缓存 &#40;分区&#41;](partitions-proactive-caching.md)  
  
  
