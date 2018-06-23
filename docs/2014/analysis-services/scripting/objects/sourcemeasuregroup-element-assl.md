---
title: SourceMeasureGroup 元素 (ASSL) |Microsoft 文档
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
- SourceMeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SourceMeasureGroup
helpviewer_keywords:
- SourceMeasureGroup element
ms.assetid: aaa7cc0b-162a-4c31-ab03-a90f81eeca00
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9eab12a6f29d73d242c8987f7719092e9974e164
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028884"
---
# <a name="sourcemeasuregroup-element-assl"></a>SourceMeasureGroup 元素 (ASSL)
  标识用作挖掘结构列的数据源的度量值组。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <SourceMeasureGroup xsi:type="MeasureGroupBinding">...</SourceMeasureGroup>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)类型的[TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 有关详细信息`Binding`类型，包括表的 Analysis Services 脚本语言 (ASSL) 对象`Binding`类型和继承层次结构的`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](../data-type/binding-data-type-assl.md).  
  
 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 对应的父级的元素`SourceMeasureGroup`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.MiningStructureColumn>和<xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  