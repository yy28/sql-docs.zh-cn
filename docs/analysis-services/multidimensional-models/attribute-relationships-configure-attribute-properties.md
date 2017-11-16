---
title: "配置特性关系属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b43a3d43e189279b45d5347b746a047f8f76eb88
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-relationships---configure-attribute-properties"></a>属性关系-配置特性属性
  下表列出了特性关系的属性并对这些属性进行了说明。  
  
|属性|Description|  
|--------------|-----------------|  
|Attribute|包含特性的名称。|  
|基数|指示关系的基数。 对于多对一关系，值为 Many，对于一对一关系，值为 One。 默认值为 Many。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，基数属性不起作用 - 保留以供将来实现中使用。|  
|名称|包含属性的友好名称。|  
|RelationshipType|指示成员关系是否随时间而更改。 值为 Rigid 和 Flexible，前者表示成员之间的关系不随时间而更改，后者表示成员之间的关系随时间而更改。 默认值为 Flexible。 如果您将关系定义为 Flexible（柔性），则将删除聚合并作为增量更新的一部分重新计算（如果只添加了新成员，则将不删除聚合）。 如果您将关系定义为 Rigid（刚性），则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在增量更新维度时保留聚合。 如果定义为刚性的关系发生了实际更改， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在增量处理过程中生成错误。 指定适当的关系和关系属性，可提高查询和处理性能。|  
|Visible|确定属性关系的可见性。 值为 True 或 False。 默认值为 True。|  
  
  

