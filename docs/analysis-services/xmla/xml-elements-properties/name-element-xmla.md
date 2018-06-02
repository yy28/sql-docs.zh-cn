---
title: 名称元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c0686dfbb5949c9b2fe3a20e34824e731369b266
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575809"
---
# <a name="name-element-xmla"></a>Name 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的属性成员的名称[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)或[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|请参阅下表。|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)，[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关**属性**元素，**名称**元素包含要插入或更新期间，分别的属性成员的名称**插入**或**更新**命令。  
  
 有关**转换**元素，**名称**元素包含所指定的语言中的属性成员的标题**语言**父级元素**转换**对象。 如果**名称**元素未指定，或包含一个空字符串，值**名称**元素**属性**包含的元素**转换**使用元素。  
  
## <a name="see-also"></a>另请参阅
 [插入元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [语言元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [更新元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
