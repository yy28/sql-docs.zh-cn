---
title: 定义多维数据集层次结构属性 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 199e00331e26cea5c84242582f9c6382215ad411
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014930"
---
# <a name="define-cube-hierarchy-properties"></a>定义多维数据集层次结构属性
  可以使用多维数据集层次结构属性，为基于同一数据库维度的多维数据集维度中的用户定义层次结构指定唯一的设置。 下表介绍了多维数据集层次结构的属性。  
  
|“属性”|Description|  
|--------------|-----------------|  
|`Enabled`|确定是否针对多维数据集维度启用层次结构。|  
|`HierarchyID`|包含层次结构的唯一标识符 (ID)。|  
|`OptimizedState`|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> `FullyOptimized`： 该实例生成索引以提高查询性能的层次结构。 这是默认值。<br /><br /> `NotOptimized`： 该实例不会生成其他索引。|  
|`Visible`|确定多维数据集层次结构的可见性。 默认值是 `True`。|  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  