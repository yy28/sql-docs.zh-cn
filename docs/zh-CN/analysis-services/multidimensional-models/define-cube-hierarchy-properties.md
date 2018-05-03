---
title: 定义多维数据集层次结构属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e91bbb6bdc5ef6e84653d69fc26e4caa18c9f37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="define-cube-hierarchy-properties"></a>定义多维数据集层次结构属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以使用多维数据集层次结构属性，为基于同一数据库维度的多维数据集维度中的用户定义层次结构指定唯一的设置。 下表介绍了多维数据集层次结构的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**已启用**|确定是否针对多维数据集维度启用层次结构。|  
|**HierarchyID**|包含层次结构的唯一标识符 (ID)。|  
|**OptimizedState**|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> **FullyOptimized**：<br />                    实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> **NotOptimized**：<br />                    实例未生成其他索引。|  
|**Visible**|确定多维数据集层次结构的可见性。 默认值是 **True**秒。|  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
