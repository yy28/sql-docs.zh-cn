---
title: LogFileRollover 元素 (ASSL) |Microsoft Docs
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
- LogFileRollover Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileRollover
helpviewer_keywords:
- LogFileRollover element
ms.assetid: 5484e167-b891-431a-bbae-946ea6eb4a3c
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12ed8df0217baeb5f760273ad6998e2344f4fbb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299017"
---
# <a name="logfilerollover-element-assl"></a>LogFileRollover 元素 (ASSL)
  指定的日志记录[跟踪](../objects/trace-element-assl.md)输出应转到新文件，还是应停止时的最大日志文件大小时，它是指定在[LogFileSize](logfilesize-element-assl.md)为止。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
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
 如果 `LogFileRollover` 元素的值设置为 True，则当日志文件的大小超出 `LogFileSize` 父元素的 `Trace` 元素中所指定的值时，打开一个新文件，否则停止日志记录。  
  
 父级对应的元素`LogFileRollover`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>请参阅  
 [跟踪元素&#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
