---
title: 返回元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d6130d367f38a9f2ca04d2ae3ac26c9bcb93c9b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="return-element-xmla"></a>return 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含返回的信息[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)到响应中的元素[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法调用或[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)到响应中的元素[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
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
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
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
  
## <a name="remarks"></a>注释  
 **返回**元素包含返回的数据**发现**和**执行**方法。 通常情况下，**返回**元素包含一个**根**包含返回成功的任一的数据元素**发现**或**执行**方法调用或的 XML for Analysis (XMLA) 失败的方法调用所返回的异常。 如果**执行**方法包含**批处理**命令执行多项操作，**返回**元素包含**结果**元素，它又包含一个**根**元素为每个命令执行成功或失败由**批处理**命令。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
