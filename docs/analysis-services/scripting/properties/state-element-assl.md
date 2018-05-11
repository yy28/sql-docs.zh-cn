---
title: 状态元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e2baf0425b1ba82830c991fdbe1057d5d4d5b495
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="state-element-assl"></a>State 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含一个只读值，它说明父元素的当前处理状态。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningModel, MiningStructure, Partition -->  
      ...  
   <State>...</State>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*处理*|该元素已完全处理。|  
|*PartiallyProcessed*|该元素仅进行了部分处理。 ([多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)和[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)仅。)|  
|*未处理*|该元素尚未处理。|  
  
 对应于的允许值为枚举**状态**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AnalysisState>。  
  
 对应的父级的元素**状态**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
