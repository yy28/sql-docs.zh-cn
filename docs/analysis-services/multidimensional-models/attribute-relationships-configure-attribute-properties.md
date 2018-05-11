---
title: 配置特性关系属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0fd5bc7535cb4bfe45fcaae3a904d5574d540b9c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-relationships---configure-attribute-properties"></a>属性关系-配置特性属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  下表列出了特性关系的属性并对这些属性进行了说明。  
  
|属性|Description|  
|--------------|-----------------|  
|Attribute|包含特性的名称。|  
|基数|指示关系的基数。 对于多对一关系，值为 Many，对于一对一关系，值为 One。 默认值为 Many。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，基数属性不起作用 - 保留以供将来实现中使用。|  
|名称|包含属性的友好名称。|  
|RelationshipType|指示成员关系是否随时间而更改。 值为 Rigid 和 Flexible，前者表示成员之间的关系不随时间而更改，后者表示成员之间的关系随时间而更改。 默认值为 Flexible。 如果您将关系定义为 Flexible（柔性），则将删除聚合并作为增量更新的一部分重新计算（如果只添加了新成员，则将不删除聚合）。 如果您将关系定义为 Rigid（刚性），则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在增量更新维度时保留聚合。 如果定义为刚性的关系发生了实际更改， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在增量处理过程中生成错误。 指定适当的关系和关系属性，可提高查询和处理性能。|  
|Visible|确定属性关系的可见性。 值为 True 或 False。 默认值为 True。|  
  
  
