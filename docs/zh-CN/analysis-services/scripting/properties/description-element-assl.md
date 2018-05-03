---
title: Description 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Description Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30b8c25a0718c5cf3351917f28a8448f9719c97e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="description-element-assl"></a>Description 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)，[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)，[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)， [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)， [CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[级别](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)， [分区](../../../analysis-services/scripting/objects/partition-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)，[角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)， [跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)，[转换](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 值**说明**元素具有以下限制：  
  
-   该值不可包含前导空格或尾随空格。 如果的值中包含前导空格或尾随空格**说明**元素，这些空间会隐式移除[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   该值不可包含控制字符。 如果控制字符中的值包括**说明**元素，这些字符会隐式移除[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [命名元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
