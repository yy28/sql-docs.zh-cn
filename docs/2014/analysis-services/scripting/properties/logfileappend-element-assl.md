---
title: LogFileAppend 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2d337d4110afc07d8aa211bc17685bc0fc2e8d81
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124868"
---
# <a name="logfileappend-element-assl"></a>LogFileAppend 元素 (ASSL)
  确定是否[跟踪](../objects/trace-element-assl.md)元素将其日志记录输出追加到现有的日志文件，或者覆盖它。  
  
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
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应于的父元素`LogFileAppend`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>请参阅  
 [跟踪元素&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  