---
title: 度量值元素 (ASSL) |Microsoft Docs
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
- Measure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Measure
helpviewer_keywords:
- Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d59a5356bf1c0b5712e729f230fff9383603cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159328"
---
# <a name="measure-element-assl"></a>Measure 元素 (ASSL)
  定义一个度量值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Measures>  
   <Measure> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <AggregateFunction>...</AggregateFunction>  
            <DataType>...</DataType>  
            <Source>...</Source>  
      <Visible>...</Visible>  
      <MeasureExpression>...</MeasureExpression>  
      <DisplayFolder>...</DisplayFolder>  
      <FormatString>...</FormatString>  
      <BackColor>...</BackColor>  
      <ForeColor>...</ForeColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Measure>  
   <!-- or  -->  
   <Measure xsi:type="AggregationInstanceMeasure">...</Measure> <!-- parent: AggregationInstance -->  
      <!-- or  -->  
   <Measure xsi:type="MeasureBinding">...</Measure> <!-- ancestor: MeasureGroupBinding (out-of-line) -->  
   <!-- or  -->  
   <Measure xsi:type="PerspectiveMeasure">...</Measure> <!-- ancestor: PerspectiveMeasureGroup -->  
</Measures>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[度量值组](group-element-assl.md)|InclusionThresholdSetting|  
|[MeasureGroupBinding （外部）](../data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[度量值](../collections/measures-element-assl.md)|  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/aggregatefunction-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [BackColor](../properties/backcolor-element-assl.md)，[数据类型](../properties/datatype-element-assl.md)，[说明](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [FontFlags](../properties/fontflags-element-assl.md)， [FontName](../properties/name-element-assl.md)， [FontSize](../properties/fontsize-element-assl.md)， [ForeColor](../properties/forecolor-element-assl.md)，[格式字符串](../properties/formatstring-element-assl.md)， [ID](../properties/id-element-assl.md)， [MeasureExpression](../properties/expression-element-assl.md)，[名称](../properties/name-element-assl.md)，[源](../properties/source-element-measure-assl.md)，[翻译](../collections/translations-element-assl.md)，[可见](../properties/visible-element-assl.md)|  
|其他|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 可以为度量值提供绑定详细信息。 这些详细信息可用作每个分区的默认值。  
  
 在较大的多维数据集中，可能有几百个度量值和层次结构。 `DisplayFolder` 属性可定义客户端的用户外观。 `DisplayFolder` 属性的值可包含任何下列选项之一：  
  
-   为空，表示该度量值不属于文件夹。  
  
-   包含单个文件夹名称，表示该度量值应呈现为属于具有相同名称的文件夹。  
  
-   包含由反斜杠分隔的多个文件夹名称 (\\)，表示嵌入的文件夹层次结构。  
  
 `DisplayFolder` 属性还适用于计算度量值和层次结构。  
  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.Measure> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasure>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
