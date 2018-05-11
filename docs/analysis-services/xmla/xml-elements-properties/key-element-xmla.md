---
title: 密钥元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd43ad594acb118be0e7fb8d39cb34f2ae3e6ef6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="key-element-xmla"></a>Key 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含属性成员的成员键值。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[密钥](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素使用的数据类型应与指定属性的相应键列的数据类型相匹配。 如果**密钥**元素未指定父**属性**元素， **AttributeName**和**名称**中指定的元素父**属性**元素用于标识要修改的属性成员。  
  
## <a name="see-also"></a>另请参阅  
 [Attribute 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [AttributeName 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [删除元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [更新元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [其中元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
