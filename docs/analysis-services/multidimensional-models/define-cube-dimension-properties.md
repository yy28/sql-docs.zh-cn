---
title: "定义多维数据集维度属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "维度 [Analysis Services]，特征"
  - "属性 [Analysis Services]，维度"
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# 定义多维数据集维度属性
  多维数据集维度是多维数据集中的数据库维度实例。 一个数据库维度可用于多个多维数据集，多个多维数据集维度可基于单个数据库维度。 下表说明了多维数据集维度的属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|控制 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的聚合设计器如何设计聚合。 此属性可以有下列值：<br /><br /> **完全**：多维数据集的每个聚合都必须包括所有成员。<br /><br /> **无**：多维数据集的任何聚合都不能包括所有成员。 这是默认值。<br /><br /> **无限制**：对聚合设计器不作限制。<br /><br /> **默认值**：与“无限制”功能相同。|  
|**Description**|为该级别提供一个说明性名称。|  
|**DimensionID**|包含数据库维度的唯一标识符 (ID)。|  
|**HierarchyUniqueNameStyle**|确定如何为包含在多维数据集维度中的层次结构生成唯一名称。 此属性可以有下列值：<br /><br /> **IncludeDimensionName**：<br />                    包括维度的名称，将其作为层次结构名称的一部分。 这是默认值。<br /><br /> **ExcludeDimensionName**：<br />                    维度的名称不作为层次结构名称的一部分。|  
|**ID**|包含多维数据集维度的唯一标识符。|  
|**MemberUniqueNameStyle**|确定如何为包含在多维数据集维度中的层次结构的成员生成唯一的名称。 此属性可以有下列值：<br /><br /> **Native**：<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动确定成员的唯一名称。 这是默认值。<br /><br /> **NamePath**：[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将生成由每个级别的名称和成员的标题组成的复合名称。|  
|**名称**|包含多维数据集维度的友好名称。 默认情况下，多维数据集维度与数据库维度同名，除非已经定义了另一个同名的多维数据集维度。|  
|**Visible**|确定多维数据集维度是否是可见的。 默认值是 **True**秒。|  
  
## 另请参阅  
 [维度（Analysis Services - 多维数据）](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  