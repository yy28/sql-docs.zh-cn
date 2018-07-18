---
title: return 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e8746fb9f8b397ef50b1a5c66a2132e5f0cf5c87
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968439"
---
# <a name="return-element-xmla"></a>return 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含返回的信息[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)元素为响应[Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法调用或[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)元素为响应[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>元素的特性  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)， [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|子元素|请参阅下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)或[结果](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **返回**元素包含返回的数据**Discover**并**Execute**方法。 通常情况下，**返回**元素包含一个**根**元素，其中包含由成功返回的数据**发现**或**Execute**方法调用或 XML for Analysis (XMLA) 异常的失败的方法调用返回。 如果**Execute**方法包含**Batch**执行多个操作的命令**返回**元素包含**结果**元素，该元素又包含一个**根**每个命令执行成功或失败**批处理**命令。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
