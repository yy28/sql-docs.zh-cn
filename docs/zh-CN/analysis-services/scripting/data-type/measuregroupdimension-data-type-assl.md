---
title: MeasureGroupDimension 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- MeasureGroupDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fc9affe514e806e53d131308105efd1f470062d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="measuregroupdimension-data-type-assl"></a>MeasureGroupDimension 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个抽象的基元数据类型，该类型表示某个维度和度量值组之间的关系。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|[DataMiningMeasureGroupDimension](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)， [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)， [ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)， [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CubeDimensionID](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|派生元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)([维度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)集合[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 每个**MeasureGroupDimension**是对一个维度在多维数据集的引用。 它们定义哪些多维数据集维度应用于度量值组。  
  
 提供的属性集确定度量值组中哪个粒度（范围）的度量值为已知。 例如，表示产品销售额的度量值包含在“销售”度量值组中。 这些度量值的信息将按月，而不是按周或天的粒度存储到基础数据源中。 在这种情况下，仅月属性将不会为列出**MeasureGroupDimension**描述时间维度和 Sales 度量值组之间的关系。 在极少数情况下，粒度可能是以一组属性定义的。 例如，给定属性集 {Day, Week, Month, Year}，其中 Day 隐含 Week 和 Month，但 Week 不隐含 Month，“预测”度量值组中包含的度量值可能对 Month 和 Week 来说为已知，但对 Day 来说为未知。  
  
 如果未提供任何属性，则如同只列出维度的键属性（定义最低级别的粒度）。 度量值组的每个分区必须具有相同的粒度。 列出的属性集的各属性间不应包含冗余的关系。 例如，如果 Month 隐含 Year，则粒度应被定义为 Month，而不应为 Month 和 Year。  
  
 A **MeasureGroupDimension**需要包含层次结构，仅当它具有特定以指示有关它的内容。 （无法选择哪些层次结构应用于特定度量值组）。 同样，它需要包括[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)仅当它具有特定以指示有关它的内容。  
  
 每个层次结构必须是包含在层次结构的子集[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)。 级别无法选择，尽管某些级别会根据度量值组的粒度被自动禁用。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MeasureGroupDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
