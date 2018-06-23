---
title: 名称元素 (ASSL) |Microsoft 文档
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
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cb2185d9d2a87a2abc3ebb96ad8186fe288e6190
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028880"
---
# <a name="name-element-assl"></a>Name 元素 (ASSL)
  包含父元素的名称。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（最多 100 个字符）|  
|默认值|不定|  
|基数|1-1： 发生一次，并且一次的必需的元素|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Action](../objects/action-element-assl.md), [Aggregation](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [Annotation](../objects/annotation-element-assl.md), [Assembly](../objects/assembly-element-assl.md), [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md), [Cube](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [Database](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [Dimension](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Group](../objects/group-element-assl.md), [Hierarchy](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [Level](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Measure](../objects/measure-element-assl.md), [MeasureGroup](../objects/measuregroup-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [Partition](../objects/partition-element-assl.md), [Permission](../data-type/permission-data-type-assl.md), [Perspective](../objects/perspective-element-assl.md), [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [Role](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md), [Trace](../objects/trace-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 每个元素，用于定义对象 (实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，层次结构和属性，等) 具有`Name`作为属性的元素。 `Name` 元素的值具有下列限制：  
  
-   该值不可包含前导空格或尾随空格。 如果 `Name` 元素的值中包含前导空格或尾随空格，则这些空格将会被 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 隐式删除。  
  
-   该值不应包含控制字符。 强烈建议名称中不要出现控制字符，这些字符有时会导致 XML 验证错误。  
  
     对于使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 `GetNewName` 方法创建的对象，AMO 将检查并随后删除名称中的任何控制字符、前导空格或尾随空格。 因此，使用 `GetNewName` 是设置对象名称的推荐方法。  
  
     但是，如果直接设置 `Name` 属性，将不会执行相同的验证检查，这可能导致 XML 验证错误。 实际是否会出现错误取决于名称中出现的是哪种控制字符。  
  
     虽然对象名称中绝对不应该使用控制字符，但 Analysis Services 并未严格阻止它们。 之前版本的 Analysis Services 有时接受对象名称中的控制字符。 因此，[!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 将忽略对象名称中的控制字符以避免使早期的解决方案失效。  
  
-   不可使用以下保留值：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9（COM1、COM2、COM3 等）  
  
    -   CON  
  
    -   LPT1 到 LPT9（LPT1、LPT2、LPT3 等）  
  
    -   NUL  
  
    -   PRN  
  
 下表列出了不可在 `Name` 元素的值中使用的其他字符，具体取决于父元素。  
  
|父元素|无效的字符|  
|--------------------|------------------------|  
|[Server](../objects/server-element-assl.md)|此名称必须遵循 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 计算机名称规则。 IP 地址无效。|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?"（) []{}<>|  
|[级别](../objects/level-element-assl.md)，[属性元素](../objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"& %$！ + = []{}<>|  
|所有其他父元素|.,;'`:/\\*&#124;?"& %$！ + = （) []{}<>|  
  
## <a name="see-also"></a>请参阅  
 [ID 元素&#40;ASSL&#41;](id-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  