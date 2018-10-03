---
title: Text 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Text Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- text
helpviewer_keywords:
- Text element
ms.assetid: 0edece73-236f-4661-8102-3fcc29326bf4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a53693bc2a102061c84e7c44c4155c21adb51756
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057793"
---
# <a name="text-element-assl"></a>Text 元素 (ASSL)
  包含的文本[命令](../objects/command-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../objects/command-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`Text`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Command>。  
  
## <a name="see-also"></a>请参阅  
 [命令元素&#40;ASSL&#41;](../collections/commands-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
