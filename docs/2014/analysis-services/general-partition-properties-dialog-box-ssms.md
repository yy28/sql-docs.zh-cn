---
title: 常规 （分区属性对话框) (SSMS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05d840d4e43d9856dedeb3fd446c8158f23275b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081064"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>常规（“分区属性”对话框）(SSMS)
  对于 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的多维数据集，可以在 SQL Server Management Studio 中使用“分区属性”  对话框的“常规”  页，为其度量值组中的分区设置常规属性。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**聚合设计 ID**|显示分区所使用的聚合设计的标识符。|  
|**聚合前缀**|显示分区所包含的聚合实例的默认前缀。|  
|**创建时间戳**|显示分区的创建日期和时间。|  
|**当前存储模式**|显示分区的当前存储模式。<br /><br /> 注意：此模式可能会有所不同，具体取决于分区的主动缓存设置。 有关主动缓存的详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**说明**|键入内容即可更改分区的说明。|  
|**估计行数**|键入在基础数据源中由该分区表示的估计行数。 在处理期间将使用此值来估计处理分区所需的时间和存储空间。|  
|**估计的大小**|显示分区的估计大小。|  
|**ID**|显示分区的标识符。|  
|**上次处理**|显示上次处理分区的日期和时间。|  
|**上次架构更新时间**|显示上次更新分区元数据的日期和时间。|  
|**名称**|显示分区的名称。|  
|**处理模式**|选择分区的处理模式。 有关处理模式的详细信息[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]对象，请参阅[多维模型对象处理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。|  
|**远程数据源 ID**|显示从中检索分区的源数据的远程数据源的标识符。<br /><br /> 注意：此属性包含远程分区的值。|  
|**Slice**|显示用于标识分区所表示的数据切片的表达式。|  
|**数据源**|显示为分区提供源数据的表或查询。|  
|**状态**|显示分区的当前处理状态。|  
|**存储位置**|显示用于存储分区的数据的文件夹。<br /><br /> 注意：此属性包含一个值，仅当以外的默认存储位置的存储位置[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]指定实例。|  
|**类型**|显示分区的类型。|  
  
## <a name="see-also"></a>请参阅  
 [分区（Analysis Services - 多维数据）](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [远程分区](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [分区属性对话框&#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [选择&#40;分区属性对话框&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [主动缓存&#40;分区属性对话框&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [多维数据集、 分区和维度处理的错误配置&#40;SSAS-多维&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
