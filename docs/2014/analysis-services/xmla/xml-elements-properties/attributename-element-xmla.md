---
title: AttributeName 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AttributeName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AttributeName
- http://schemas.microsoft.com/analysisservices/2003/engine#AttributeName
- microsoft.xml.analysis.attributename
helpviewer_keywords:
- AttributeName element
ms.assetid: 4dc8260b-522e-46d9-9bd8-22a5a0068982
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f64264e9432ff4f06b375b3d1ad1b0dfd814514
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178737"
---
# <a name="attributename-element-xmla"></a>AttributeName 元素 (XMLA)
  包含父对象所表示的特性的名称[特性](attribute-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Attribute>  
   ...  
   <AttributeName>...</AttributeName>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Attribute](attribute-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [Drop 元素&#40;XMLA&#41;](../xml-elements-commands/drop-element-xmla.md)   
 [插入元素&#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Update 元素&#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [其中元素&#40;XMLA&#41;](where-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
