---
title: AggregationType 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21b6f4c4ca55ee77a07a92510bb09f8ea78526ae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationtype-element-assl"></a>AggregationType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义的由存储的聚合类型[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AggregationInstance>  
   ...  
   <AggregationType>...</AggregationType>  
   ...  
</AggregationInstance>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*IndexedView*|聚合存储在索引视图中。|  
|*表*|聚合存储在表中。|  
|*用户定义*|聚合是用户定义的。|  
  
 对应于的允许值为枚举**AggregationType**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
