---
title: 定义多维数据集层次结构属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ace708cc4ee09295380b814bbf21f5a1c350974
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075704"
---
# <a name="define-cube-hierarchy-properties"></a>定义多维数据集层次结构属性
  可以使用多维数据集层次结构属性，为基于同一数据库维度的多维数据集维度中的用户定义层次结构指定唯一的设置。 下表介绍了多维数据集层次结构的属性。  
  
|properties|说明|  
|--------------|-----------------|  
|`Enabled`|确定是否针对多维数据集维度启用层次结构。|  
|`HierarchyID`|包含层次结构的唯一标识符 (ID)。|  
|`OptimizedState`|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> 
  `FullyOptimized`：实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> 
  `NotOptimized`：实例不生成其他索引。|  
|`Visible`|确定多维数据集层次结构的可见性。 默认值是 `True`。|  
  
## <a name="see-also"></a>另请参阅  
 [用户层次结构](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
