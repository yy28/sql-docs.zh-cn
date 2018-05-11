---
title: LogFileSize 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ecb3b43efa7740aeb650cefbd19eddb38587e991
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="logfilesize-element-assl"></a>LogFileSize 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定最大日志文件大小 (MB)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Trace>  
  
   <LogFileSize>...</LogFileSize>  
  
</Trace>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|**5** （兆字节为单位）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**LogFileSize**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Trace>。  
  
## <a name="see-also"></a>另请参阅  
 [跟踪元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/traces-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
