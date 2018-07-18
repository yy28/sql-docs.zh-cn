---
title: 时间元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5c7cb1b1eb18d02bd2ae043181ccc9f72a758432
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051695"
---
# <a name="time-element-xmla"></a>Time 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指定时间限制由[DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)命令用于设计聚合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Time>...</Time>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Duration|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
