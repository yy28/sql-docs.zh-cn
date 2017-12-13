---
title: "定义多维数据集层次结构属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
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
ms.openlocfilehash: 858e5f95c4c382b46d85a9f0abcae728bae102c1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="define-cube-hierarchy-properties"></a>定义多维数据集层次结构属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]多维数据集层次结构属性，可以指定基于相同的数据库维度的多维数据集维度中的用户定义的层次结构的唯一设置。 下表介绍了多维数据集层次结构的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**已启用**|确定是否针对多维数据集维度启用层次结构。|  
|**HierarchyID**|包含层次结构的唯一标识符 (ID)。|  
|**OptimizedState**|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> **FullyOptimized**：<br />                    实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> **NotOptimized**：<br />                    实例未生成其他索引。|  
|**Visible**|确定多维数据集层次结构的可见性。 默认值是 **True**秒。|  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
