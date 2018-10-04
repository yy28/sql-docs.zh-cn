---
title: InvalidXmlCharacters 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- InvalidXmlCharacters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- InvalidXmlCharacters
helpviewer_keywords:
- InvalidXmlCharacters element
ms.assetid: 92b1210c-1075-4f2f-a2c4-dfdc6d7e5c05
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0832f4138adc3f278af0d735b70251590fb3ba41
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059631"
---
# <a name="invalidxmlcharacters-element-assl"></a>InvalidXmlCharacters 元素 (ASSL)
  指定源数据中无效 XML 字符的处理方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
   ...  
</DataItem  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*保留*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*保留*|保留无效 XML 字符。|  
|*删除*|删除无效 XML 字符。|  
|*替换*|用问号 (?) 字符替换无效的 XML 字符。|  
  
 与允许的值相对应的枚举`InvalidXmlCharacters`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.InvalidXmlCharacters>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
