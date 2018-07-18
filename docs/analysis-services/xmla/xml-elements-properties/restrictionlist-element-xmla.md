---
title: RestrictionList 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c802b20b0e2d6212f68fa4dc43c35426ff377957
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994779"
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 方法使用的限制列和值的集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[限制](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|子元素|限制列和值（请参阅“备注”）。|  
  
## <a name="remarks"></a>Remarks  
 **RestrictionList** 元素包含限制列的集合，可在这些列上筛选 **Discover** 方法返回的数据。 **RestrictionList** 元素中的每个限制列由一个单独的 XML 元素定义。 限制列的值是 XML 元素中包含的数据，限制列的名称与 XML 元素的名称相对应。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
