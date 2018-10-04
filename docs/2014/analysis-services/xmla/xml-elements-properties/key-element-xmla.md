---
title: 密钥元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Key Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords:
- Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1532db273c83f16678d278f068befefcd8df4b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101277"
---
# <a name="key-element-xmla"></a>Key 元素 (XMLA)
  包含属性成员的成员键值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Any|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[密钥](keys-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素使用的数据类型应与指定属性的相应键列的数据类型相匹配。 如果未指定父 `Key` 元素的 `Attribute` 元素，则在父 `AttributeName` 元素中指定的 `Name` 和 `Attribute` 元素用于标识要修改的属性成员。  
  
## <a name="see-also"></a>请参阅  
 [属性元素&#40;XMLA&#41;](attribute-element-xmla.md)   
 [AttributeName 元素&#40;XMLA&#41;](name-element-xmla.md)   
 [Drop 元素&#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [KeyColumn 元素&#40;ASSL&#41;](../../scripting/objects/column-element-assl.md)   
 [Update 元素&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [其中元素&#40;XMLA&#41;](where-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
