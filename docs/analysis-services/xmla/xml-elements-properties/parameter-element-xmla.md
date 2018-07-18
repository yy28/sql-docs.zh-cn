---
title: Parameter 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e361215425c1e7b0e54b2e8a92b2987d30b00790
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050355"
---
# <a name="parameter-element-xmla"></a>Parameter 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含名称和使用的一个参数的值[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
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
|父元素|[Parameters](../../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md)|  
|子元素|[名称](../../../analysis-services/xmla/xml-elements-properties/name-element-parameter-xmla.md)，[值](../../../analysis-services/xmla/xml-elements-properties/value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 某些 XML for Analysis (XMLA) 命令，如[进程](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令，可能需要其他信息。 **参数**元素提供了一种机制，用于提供其他信息，包括成块的信息，为 XMLA 命令。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
