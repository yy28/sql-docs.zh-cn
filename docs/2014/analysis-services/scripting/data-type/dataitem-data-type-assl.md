---
title: DataItem 数据类型 (ASSL) |Microsoft 文档
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
- DataItem Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d5622ca2cdda5a08bdcfdfd486e44b6fcd8fbf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016936"
---
# <a name="dataitem-data-type-assl"></a>DataItem 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示数据项的数据相关特征，如列或属性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   <DataType>...</DataType>  
   <DataSize>...</DataSize>  
   <MimeType>...</MimeType>  
   <NullProcessing>...</NullProcessing>  
   <Trimming>...</Trimming>  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
      <Collation>...</Collation>  
   <Format>...</Format>  
   <Source>...</Source>  
   <Annotations>...</Annotations>  
</DataItem>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[批注](../collections/annotations-element-assl.md)，[排序规则](../properties/collation-element-assl.md)， [DataSize](../properties/datasize-element-assl.md)， [DataType](../properties/datatype-element-assl.md)，[格式](../properties/format-element-assl.md)， [InvalidXmlCharacters](../properties/invalidxmlcharacters-element-assl.md)， [MimeType](../properties/mimetype-element-assl.md)， [NullProcessing](../properties/nullprocessing-element-assl.md)，[源](../properties/source-element-binding-assl.md)，[修剪](../properties/trimming-element-assl.md)|  
|派生元素|请参阅“备注”中的表。|  
  
## <a name="remarks"></a>Remarks  
 `DataItem` 数据类型可用于任何可以绑定的数据项；例如，度量值、属性键和属性名称。 相关的详细信息和适用的默认值取决于用法；例如，属性名称必须为字符串。  
  
 实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]接受某些组的数据类型。 使用其他数据类型将导致错误，而不是隐式转换为一种有效类型。  
  
 下表列出了 `DataItem` 类型的元素。  
  
|父元素|`DataItem` 类型的元素|注释|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../objects/column-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrollupcolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrolluppropertiescolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/keycolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)， [AttributeBinding](attributebinding-data-type-assl.md)或[TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/namecolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/skippedlevelscolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/unaryoperatorcolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)或[AttributeBinding](attributebinding-data-type-assl.md)|  
|[度量值](../objects/measure-element-assl.md)|[数据源](../properties/source-element-binding-assl.md)|`Source` 元素的`DataItem`的类型必须为[RowBinding](rowbinding-data-type-assl.md)， [ColumnBinding](binding-data-type-assl.md)， [MeasureBinding](measurebinding-data-type-assl.md)，或[CubeDimensionBinding](dimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)， [AttributeBinding](attributebinding-data-type-assl.md)或[InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[NameColumn](../objects/namecolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/foreignkeycolumn-element-assl.md)|`Source` 元素的`DataItem`的类型必须为[ColumnBinding](binding-data-type-assl.md)|  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  