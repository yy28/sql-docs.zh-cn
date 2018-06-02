---
title: CubeID 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57c8075b87fbd71bdafcb6f8116dd067e62e722d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579089"
---
# <a name="cubeid-element-xmla"></a>CubeID 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  标识父元素中包含对象引用的多维数据集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element relationships table -->  
   ...  
   <CubeID>...</CubeID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|请参阅下表。|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[数据源](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|其他|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)、[ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)、[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)、[Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
