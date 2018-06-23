---
title: OnlineMode 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- OnlineMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3efda242b0563f4b6b853d3bf87b831da1ea8e00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130218"
---
# <a name="onlinemode-element-assl"></a>OnlineMode 元素 (ASSL)
  指定是在重新生成缓存刚一开始就立即使数据库恢复到联机状态，还是在完成重新生成缓存后才使数据库恢复到联机状态。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*立即*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*立即*|重新生成缓存刚一开始就立即使数据库恢复到联机状态。|  
|*OnCacheComplete*|在完成重新生成缓存后才使数据库恢复到联机状态。|  
  
 对应于的允许值为枚举`OnlineMode`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>请参阅  
 [ProactiveCaching 元素&#40;ASSL&#41;](../objects/proactivecaching-element-assl.md)  
  
  