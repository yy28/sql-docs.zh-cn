---
title: Description 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Description Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 43e54f7c6f72703c0ddaff7776594fe0ac80ac64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029317"
---
# <a name="description-element-assl"></a>Description 元素 (ASSL)
  包含父元素的说明。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [AttributePermission](../objects/attributepermission-element-assl.md), [CalculationProperty](../objects/calculationproperty-element-assl.md), [CellPermission](../objects/cellpermission-element-assl.md), [Cube](../objects/cube-element-assl.md), [CubeDimensionPermission](../data-type/permission-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [Trace](../objects/trace-element-assl.md), [Translation](../objects/translation-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Description` 元素的值具有下列限制：  
  
-   该值不可包含前导空格或尾随空格。 如果的值中包含前导空格或尾随空格`Description`元素，这些空间会隐式移除[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   该值不可包含控制字符。 如果 `Description` 元素的值中包含控制字符，则这些字符将会被 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 隐式删除。  
  
## <a name="see-also"></a>请参阅  
 [命名元素&#40;ASSL&#41;](name-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  