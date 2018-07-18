---
title: Description 元素 (ASSL) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dadef861a5b54dafddd6f2dcf3072cd4e0d510ad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194127"
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
|父元素|[操作](../objects/action-element-assl.md)，[聚合](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)，[程序集](../objects/assembly-element-assl.md)， [AttributePermission](../objects/attributepermission-element-assl.md)， [CalculationProperty](../objects/calculationproperty-element-assl.md)， [CellPermission](../objects/cellpermission-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [CubeDimensionPermission](../data-type/permission-data-type-assl.md)，[数据库](../objects/database-element-assl.md)[数据源](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[层次结构](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[级别](../objects/level-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)，[度量值](../objects/measure-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)， [分区](../objects/partition-element-assl.md)，[权限](../data-type/permission-data-type-assl.md)，[角度来看](../objects/perspective-element-assl.md)，[角色](../objects/role-element-assl.md)， [Server](../objects/server-element-assl.md)， [跟踪](../objects/trace-element-assl.md)，[翻译](../objects/translation-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Description` 元素的值具有下列限制：  
  
-   该值不可包含前导空格或尾随空格。 如果的值中包含前导或尾部空格`Description`元素，这些空格将被隐式删除通过[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   该值不可包含控制字符。 如果 `Description` 元素的值中包含控制字符，则这些字符将会被 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 隐式删除。  
  
## <a name="see-also"></a>请参阅  
 [命名元素&#40;ASSL&#41;](name-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
