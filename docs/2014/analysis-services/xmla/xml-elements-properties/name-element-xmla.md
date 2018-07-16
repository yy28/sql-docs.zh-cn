---
title: 命名元素 (XMLA) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088dd6aa9ce8d9ecae3e3a8f293f64b3ddc93c70
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194227"
---
# <a name="name-element-xmla"></a>Name 元素 (XMLA)
  包含父级的属性成员的名称[特性](attribute-element-xmla.md)或[翻译](translation-element-xmla.md)元素。  
  
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
|[翻译](translation-element-xmla.md)|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[特性](attribute-element-xmla.md)，[翻译](translation-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对于 `Attribute` 元素，`Name` 元素包含执行 `Insert` 或 `Update` 命令期间要分别插入或更新的属性成员的名称。  
  
 对于 `Translation` 元素，`Name` 元素包含有以父级 `Language` 对象的 `Translation` 元素中指定的语言表示的属性成员标题。 如果未指定 `Name` 元素或其中包含空字符串，则将使用包含 `Name` 元素的 `Attribute` 元素的 `Translation` 元素的值。  
  
## <a name="see-also"></a>请参阅  
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [语言元素&#40;XMLA&#41;](language-element-xmla.md)   
 [Update 元素&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
