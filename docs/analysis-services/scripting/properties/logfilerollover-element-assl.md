---
title: LogFileRollover 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 97a472f44cf840093d2b7f92bd7184e41561274a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="logfilerollover-element-assl"></a>LogFileRollover 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定的日志记录是否[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)输出应将鼠标移到新文件或者应停止时，它是大小最大的日志文件中指定的[LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)为止。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 如果值**LogFileRollover**元素设置为 True，则日志文件的大小超过中指定的值时启动新的文件**LogFileSize**元素**跟踪**父元素; 否则为日志记录停止。  
  
 对应于的父元素**LogFileRollover**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另请参阅  
 [跟踪元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
