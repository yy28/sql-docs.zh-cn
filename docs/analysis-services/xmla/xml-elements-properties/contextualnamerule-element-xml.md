---
title: ContextualNameRule 元素 (XML) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e25061be21fdeea6d303ffce8f9ce9f66f687a34
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="contextualnamerule-element-xml"></a>ContextualNameRule 元素 (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  提供有关为属性构建复合名称的最佳方法的提示。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|-1|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 提供有关如何为此属性创建明确名称的针对客户端应用程序的提示。  
  
 值**ContextualNameRule**元素被限制为下表中列出的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*InclusionThresholdSetting*|使用属性的名称。|  
|*上下文*|使用传入关系的名称。|  
|*合并*|按照应用程序语言的规则，将传入关系的名称和属性名称串联在一起。|  
  
  
