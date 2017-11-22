---
title: "ID 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ID
helpviewer_keywords: ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e0f489f02475053495704cdf82c30d5253abf949
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="id-element-assl"></a>ID 元素 (ASSL)
  包含父元素的唯一标识符 (ID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（最多 100 个字符）|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)，[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)，[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)，[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[级别](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)，[角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)，[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 中的每个主要对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]具有**ID**作为属性的元素。 值**ID**元素具有以下限制：  
  
-   该值不可包含前导空格或尾随空格。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]将隐式移除前导空格或尾随空格的值**ID**元素。  
  
-   该值不可包含控制字符。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]隐式将的值从删除的控制字符**ID**元素。  
  
-   不可使用以下保留值：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9（COM1、COM2、COM3 等）  
  
    -   CON  
  
    -   LPT1 到 LPT9（LPT1、LPT2、LPT3 等）  
  
    -   NUL  
  
    -   PRN  
  
 下表列出的值不能使用的其他字符**ID**元素，具体取决于父元素。  
  
|父元素|字符|  
|--------------------|----------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|此值必须遵循 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 计算机名称规则。 （IP 地址无效。）|  
|[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[级别](../../../analysis-services/scripting/objects/level-element-assl.md)，[属性元素](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|所有其他父元素|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>另请参阅  
 [Name 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
