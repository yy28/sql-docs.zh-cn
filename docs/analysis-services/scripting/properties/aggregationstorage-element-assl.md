---
title: AggregationStorage 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 998ec267ca264401d66f4950b78f1e743f54636a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationstorage-element-assl"></a>AggregationStorage 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识聚合的存储方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <AggregationStorage>...</AggregationStorage>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Regular*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下列字符串之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|*Regular*|聚合数据以默认方式存储。|  
|*MolapOnly*|聚合数据仅使用多维 OLAP (MOLAP) 存储进行存储。|  
  
 *MolapOnly*选项是仅适用于[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。  
  
 对应于的允许值为枚举**AggregationStorage**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ProactiveCachingAggregationStorage>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
