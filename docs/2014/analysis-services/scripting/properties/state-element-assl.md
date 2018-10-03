---
title: 状态元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- State Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- State
helpviewer_keywords:
- State element
ms.assetid: b6ee1144-89f7-4ced-bc87-c2e33ca25f73
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1aaf3af4f5a98c8601f9738765a248fe597ccb31
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072087"
---
# <a name="state-element-assl"></a>State 元素 (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../objects/cube-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*处理*|该元素已完全处理。|  
|*PartiallyProcessed*|该元素仅进行了部分处理。 ([多维数据集](../objects/cube-element-assl.md)并[MeasureGroup](../objects/group-element-assl.md)仅。)|  
|*未处理*|该元素尚未处理。|  
  
 与允许的值相对应的枚举`State`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AnalysisState>。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `State` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.MeasureGroup>、<xref:Microsoft.AnalysisServices.MiningModel>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
