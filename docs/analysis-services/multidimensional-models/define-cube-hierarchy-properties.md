---
title: "定义多维数据集层次结构属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "层次结构 [Analysis Services], 多级"
  - "层次结构 [Analysis Services], 多维数据集"
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# 定义多维数据集层次结构属性
  可以使用多维数据集层次结构属性，为基于同一数据库维度的多维数据集维度中的用户定义层次结构指定唯一的设置。 下表介绍了多维数据集层次结构的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**已启用**|确定是否针对多维数据集维度启用层次结构。|  
|**HierarchyID**|包含层次结构的唯一标识符 (ID)。|  
|**OptimizedState**|确定应用于层次结构的优化级别。 此属性可以有下列值：<br /><br /> **FullyOptimized**：<br />                    实例为层次结构生成索引以提高查询性能。 这是默认值。<br /><br /> **NotOptimized**：<br />                    实例未生成其他索引。|  
|**Visible**|确定多维数据集层次结构的可见性。 默认值是 **True**秒。|  
  
## 另请参阅  
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  