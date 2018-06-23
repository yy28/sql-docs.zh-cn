---
title: 列元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Columns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- COLUMNS
helpviewer_keywords:
- Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e635738dddc7eabda62f0c35df860db3d9a10b60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026635"
---
# <a name="columns-element-assl"></a>Columns 元素 (ASSL)
  包含与父元素关联的列的集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
  
|祖先或父级|基数|  
|------------------------|-----------------|  
|[事件](../objects/event-element-assl.md)|1-1：出现一次且仅出现一次的必需元素。|  
|其他|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)类型的[DrillThroughAction](../data-type/action-data-type-assl.md)，[事件](../objects/event-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md)或[MeasureBinding](../data-type/measurebinding-data-type-assl.md)|  
|[事件](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)， [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 有关`DrillThroughAction`元素，`Columns`集合标识包含数据时执行的操作返回的列。  
  
 有关`TableMiningStructureColumn`元素，`Columns`集合只允许一级递归。 换而言之，任何`TableMiningStructureColumn`此集合中包含的元素不能包含任何`TableMiningStructureColumn`中的元素及其`Columns`集合。  
  
 在 Analysis Management Objects (AMO) 对象模型中，部分对应的元素为 <xref:Microsoft.AnalysisServices.TraceColumnCollection>、<xref:Microsoft.AnalysisServices.MiningModelColumnCollection> 和 <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  