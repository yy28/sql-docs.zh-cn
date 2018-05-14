---
title: OnlineMode 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e02252c66333e6d75bb72871105604f35cd688c5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="onlinemode-element-assl"></a>OnlineMode 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*立即*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*立即*|重新生成缓存刚一开始就立即使数据库恢复到联机状态。|  
|*OnCacheComplete*|在完成重新生成缓存后才使数据库恢复到联机状态。|  
  
 对应于的允许值为枚举**OnlineMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>另请参阅  
 [ProactiveCaching 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
  
