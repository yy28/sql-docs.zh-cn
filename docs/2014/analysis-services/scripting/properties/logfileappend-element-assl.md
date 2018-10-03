---
title: LogFileAppend 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileAppend Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileAppend
helpviewer_keywords:
- LogFileAppend element
ms.assetid: f85e94a9-e5c5-478a-a5a0-fc99ed19b582
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bea470af9f145be58e9a6e0d2645f2173097a587
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200447"
---
# <a name="logfileappend-element-assl"></a>LogFileAppend 元素 (ASSL)
  确定是否[跟踪](../objects/trace-element-assl.md)元素将其日志记录输出追加到现有日志文件，或将其覆盖。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
  
   <LogFileAppend>...</LogFileAppend>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Trace](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`LogFileAppend`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>请参阅  
 [跟踪元素&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
