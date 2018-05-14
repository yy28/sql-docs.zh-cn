---
title: 语言元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84c62a6d1368c66c96e379ed583da3587023aa42
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="language-element-xmla"></a>Language 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含父级的区域设置标识符 (LCID)[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[转换](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **语言**元素指定由父级的 LCID**转换**元素分配**名称**元素的父**转换**为属性成员，指定的语言中，元素期间**插入**或**更新**命令。  
  
## <a name="see-also"></a>另请参阅  
 [插入元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [命名元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [更新元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
