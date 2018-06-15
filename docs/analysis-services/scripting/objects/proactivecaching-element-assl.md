---
title: ProactiveCaching 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d8c6f09789b261d9a3518df900a531fb1a2d15ef
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030398"
---
# <a name="proactivecaching-element-assl"></a>ProactiveCaching 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义父元素的主动缓存设置。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProactiveCaching>  
      <OnlineMode>...</OnlineMode>  
      <AggregationStorage>...</AggregationStorage>  
      <Source>...</Source>  
      <SilenceInterval>...</SilenceInterval>  
      <Latency>...</Latency>  
      <SilenceOverrideInterval>...</SilenceOverrideInterval>  
      <ForceRebuildInterval>...</ForceRebuildInterval>  
      <Enabled >...</Enabled>  
   </ProactiveCaching>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|[AggregationStorage](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md)，[启用](../../../analysis-services/scripting/properties/enabled-element-assl.md)， [ForceRebuildInterval](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md)，[延迟](../../../analysis-services/scripting/properties/latency-element-assl.md)， [OnlineMode](../../../analysis-services/scripting/properties/onlinemode-element-assl.md)， [SilenceInterval](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md)， [SilenceOverrideInterval](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
