---
title: LogFileSize 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileSize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileSize
helpviewer_keywords:
- LogFileSize element
ms.assetid: d2135e68-57a9-4144-8403-9627041f2a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bca304c55b352f68a3d5699f20b000f08831ab89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061237"
---
# <a name="logfilesize-element-assl"></a>LogFileSize 元素 (ASSL)
  指定最大日志文件大小 (MB)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
  
   <LogFileSize>...</LogFileSize>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|`5` (MB)|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Trace](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`LogFileSize`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>请参阅  
 [跟踪元素&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
