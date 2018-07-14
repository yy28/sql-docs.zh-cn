---
title: 常规 （分区属性对话框) (SSMS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 54ef8ce15795f8744b8ab7d368c05892a2dc850a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170148"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>常规（“分区属性”对话框）(SSMS)
  对于 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的多维数据集，可以在 SQL Server Management Studio 中使用“分区属性”对话框的“常规”页，为其度量值组中的分区设置常规属性。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**聚合设计 ID**|显示分区所使用的聚合设计的标识符。|  
|**聚合前缀**|显示分区所包含的聚合实例的默认前缀。|  
|**创建时间戳**|显示分区的创建日期和时间。|  
|**当前存储模式**|显示分区的当前存储模式。<br /><br /> 注意：根据分区的主动缓存设置的不同，此模式可能有所不同。 有关主动缓存的详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**Description**|键入内容即可更改分区的说明。|  
|**估计行数**|键入在基础数据源中由该分区表示的估计行数。 在处理期间将使用此值来估计处理分区所需的时间和存储空间。|  
|**估计的大小**|显示分区的估计大小。|  
|**ID**|显示分区的标识符。|  
|**上次处理**|显示上次处理分区的日期和时间。|  
|**上次架构更新时间**|显示上次更新分区元数据的日期和时间。|  
|**名称**|显示分区的名称。|  
|**处理模式**|选择分区的处理模式。 有关处理模式的详细信息[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]对象，请参阅[多维模型对象处理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。|  
|**远程数据源 ID**|显示从中检索分区的源数据的远程数据源的标识符。<br /><br /> 注意：只有对于远程分区，此属性才会包含值。|  
|**切片**|显示用于标识分区所表示的数据切片的表达式。|  
|**数据源**|显示为分区提供源数据的表或查询。|  
|**State**|显示分区的当前处理状态。|  
|**存储位置**|显示用于存储分区的数据的文件夹。<br /><br /> 注意：只有在为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例指定了默认存储位置以外的存储位置时，此属性才会包含值。|  
|**类型**|显示分区的类型。|  
  
## <a name="see-also"></a>请参阅  
 [分区&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [远程分区](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [分区属性对话框&#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [选择&#40;分区属性对话框&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [主动缓存&#40;分区属性对话框&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [多维数据集、 分区和维度处理的错误配置&#40;SSAS-多维&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
