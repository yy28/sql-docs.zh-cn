---
title: 定义多维数据集特性属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e84c49055a1fdb5b11487ab17af19762f86686c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145980"
---
# <a name="define-cube-attribute-properties"></a>定义多维数据集特性属性
  通过使用多维数据集特性属性，您可以为基于同一数据库维度的多维数据集维度中的维度特性指定唯一的设置。 下表介绍了多维数据集特性的属性。  
  
|“属性”|Description|  
|--------------|-----------------|  
|`AggregationUsage`|指定聚合设计向导将如何设计此属性的聚合。 此属性可以有下列值：<br /><br /> `Default`： 默认值。 聚合设计向导根据属性类型应用默认规则（对于键为 Full，对于其他为 Unrestricted）。<br /><br /> `None`： 多维数据集任何聚合都应不包含此属性。<br /><br /> `Unrestricted`： 不作限制对聚合设计向导。<br /><br /> `Full`： 多维数据集每个聚合必须包含此属性。|  
|`AttributeHierarchyEnabled`|标识是否对此多维数据集维度启用属性层次结构。 这可以对特定多维数据集或维度角色禁用属性层次结构。 如果禁用了基础属性层次结构，则此设置不起作用。 默认值是`True`。|  
|`OptimizedState`|指示是否对此多维数据集维度优化属性层次结构。 这可以对特定多维数据集或维度角色优化属性层次结构。 如果未优化基础属性层次结构，则此设置不起作用。 此属性可以有下列值：<br /><br /> `FullyOptimized`： 默认值。 实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> `NotOptimized`： 实例未生成其他索引。|  
|`AttributeHierarchyVisible`|指示属性层次结构在此多维数据集维度上是否可见。 这可以使属性层次结构在特定多维数据集或维度角色上可见。 如果基础属性层次结构不可见，则此设置不起作用。 默认值是 `True`。|  
|`AttributeID`|包含属性的唯一标识符 (ID)。|  
  
## <a name="see-also"></a>请参阅  
 [定义多维数据集维度属性](define-cube-dimension-properties.md)   
 [定义多维数据集层次结构属性](define-cube-hierarchy-properties.md)  
  
  
