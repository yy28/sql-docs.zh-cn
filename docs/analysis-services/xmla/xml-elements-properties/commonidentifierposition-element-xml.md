---
title: CommonIdentifierPosition 元素 (XML) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bdec66672ebe3e75b7cdf14c0a015740df487182
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="commonidentifierposition-element-xml"></a>CommonIdentifierPosition 元素 (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含与元素在元素集合中的位置有关的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|-1|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**RelationshipEndVisualizationProperties**元素， **CommonIdentifierPosition**元素包含的通用标识符元素集合中的详细信息的位置。 默认值**false**指示没有要使用的公共标识符。  
  
  
