---
title: SilenceOverrideInterval 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b05517f0a02a7788e49b541cfb550a817365014b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="silenceoverrideinterval-element-assl"></a>SilenceOverrideInterval 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义在收到初始通知后经过多长时间才能无条件开始多维 OLAP (MOLAP) 映像处理。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <SilenceOverrideInterval>...</SilenceOverrideInterval>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|duration|  
|默认值|P0s|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**SilenceOverrideInterval**将重写的值**SilenceInterval**如果在静默期内收到通知。  
  
 对应于的父元素**SilenceOverrideInterval**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
