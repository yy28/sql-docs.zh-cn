---
title: Trimming 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Trimming Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trimming
helpviewer_keywords:
- Trimming element
ms.assetid: 8b3bbf89-8309-4d00-9aea-a5918f0c7027
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 250394f67c79eec799f75dd0b6f590f6bff8f988
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198777"
---
# <a name="trimming-element-assl"></a>Trimming 元素 (ASSL)
  指定如何修整数据源的数据。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <Trimming>...</Trimming>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*右侧*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*左侧*|对数据的左侧进行修整。|  
|*右侧*|对数据的右侧进行修整。|  
|*LeftRight*|对数据的左侧和右侧进行修整。|  
|*无*|不修整数据。|  
  
 与允许的值相对应的枚举`Trimming`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Trimming>。  
  
 父级对应的元素`Trimming`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
