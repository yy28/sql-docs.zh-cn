---
title: ID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71de55c773ce75ec75b38b774ad0a5e8ec35ed9b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170257"
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（最多 100 个字符）|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[操作](../objects/action-element-assl.md)，[聚合](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)，[程序集](../objects/assembly-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)， [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)，[数据库](../objects/database-element-assl.md)， [DataSource](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[层次结构](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[级别](../objects/level-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)，[度量值](../objects/measure-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)，[分区](../objects/partition-element-assl.md)，[权限](../data-type/permission-data-type-assl.md)，[角度来看](../objects/perspective-element-assl.md)，[角色](../objects/role-element-assl.md)， [Server](../objects/server-element-assl.md)，[跟踪](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 在每个主要对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]具有`ID`作为属性的元素。 `ID` 元素的值有下列限制：  
  
-   该值不可包含前导空格或尾随空格。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将隐式删除 `ID` 元素值中的前导空格或尾随空格。  
  
-   该值不可包含控制字符。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将隐式删除 `ID` 元素值中的控制字符。  
  
-   不可使用以下保留值：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9（COM1、COM2、COM3 等）  
  
    -   CON  
  
    -   LPT1 到 LPT9（LPT1、LPT2、LPT3 等）  
  
    -   NUL  
  
    -   PRN  
  
 下表列出了不能使用的值中的其他字符`ID`元素，具体取决于父元素。  
  
|父元素|字符|  
|--------------------|----------------|  
|[Server](../objects/server-element-assl.md)|此值必须遵循 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 计算机名称规则。 （IP 地址无效。）|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?"（) []{}<>|  
|[级别](../objects/level-element-assl.md)，[属性元素](../objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"& %$！ + = []{}<>|  
|所有其他父元素|.,;'`:/\\*&#124;?"& %$！ + = （) []{}<>|  
  
## <a name="see-also"></a>请参阅  
 [命名元素&#40;ASSL&#41;](name-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
