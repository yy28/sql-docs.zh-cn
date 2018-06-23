---
title: 名称元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d3ae469cc1a02a02dc2bdb2ff7d6db7f75a46a69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127582"
---
# <a name="name-element-xmla"></a>Name 元素 (XMLA)
  包含父级的属性成员的名称[属性](attribute-element-xmla.md)或[转换](translation-element-xmla.md)元素。  
  
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
|祖先或父级：|基数|  
|[Attribute](attribute-element-xmla.md)|1-1：出现一次且仅出现一次的必需元素。|  
|[转换](translation-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](attribute-element-xmla.md)，[转换](translation-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对于 `Attribute` 元素，`Name` 元素包含执行 `Insert` 或 `Update` 命令期间要分别插入或更新的属性成员的名称。  
  
 对于 `Translation` 元素，`Name` 元素包含有以父级 `Language` 对象的 `Translation` 元素中指定的语言表示的属性成员标题。 如果未指定 `Name` 元素或其中包含空字符串，则将使用包含 `Name` 元素的 `Attribute` 元素的 `Translation` 元素的值。  
  
## <a name="see-also"></a>请参阅  
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [语言元素&#40;XMLA&#41;](language-element-xmla.md)   
 [更新元素&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  