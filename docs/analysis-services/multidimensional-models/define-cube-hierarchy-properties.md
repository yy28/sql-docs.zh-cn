---
title: "定义多维数据集层次结构属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dad968995a91d8a163a8ba067925e4dcb07848cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="define-cube-hierarchy-properties"></a>定义多维数据集层次结构属性
  可以使用多维数据集层次结构属性，为基于同一数据库维度的多维数据集维度中的用户定义层次结构指定唯一的设置。 下表介绍了多维数据集层次结构的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**已启用**|确定是否针对多维数据集维度启用层次结构。|  
|**HierarchyID**|包含层次结构的唯一标识符 (ID)。|  
|**OptimizedState**|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> **FullyOptimized**：<br />                    实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> **NotOptimized**：<br />                    实例未生成其他索引。|  
|**Visible**|确定多维数据集层次结构的可见性。 默认值是 **True**秒。|  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
