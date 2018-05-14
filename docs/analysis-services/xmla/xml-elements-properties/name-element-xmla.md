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
ms.openlocfilehash: 5ade2d80141163c3a2cb0effb805f82ee837390c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|请参阅下表。|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)，[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**属性**元素，**名称**元素包含要插入或更新期间，分别的属性成员的名称**插入**或**更新**命令。  
  
 有关**转换**元素，**名称**元素包含所指定的语言中的属性成员的标题**语言**父级元素**转换**对象。 如果**名称**元素未指定，或包含一个空字符串，值**名称**元素**属性**包含的元素**转换**使用元素。  
  
## <a name="see-also"></a>另请参阅  
 [插入元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [语言元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [更新元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
