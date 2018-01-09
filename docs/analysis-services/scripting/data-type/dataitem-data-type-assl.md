---
title: "DataItem 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DataItem Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DataItem
helpviewer_keywords: DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec40eca06225eef5d9c7e505e4fe2c9dee6972b1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="dataitem-data-type-assl"></a>DataItem 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义表示数据项，如列或属性的内容相关的数据的特征的基元数据类型。  
  
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
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[排序规则](../../../analysis-services/scripting/properties/collation-element-assl.md)， [DataSize](../../../analysis-services/scripting/properties/datasize-element-assl.md)， [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md)，[格式](../../../analysis-services/scripting/properties/format-element-assl.md)， [InvalidXmlCharacters](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md)， [MimeType](../../../analysis-services/scripting/properties/mimetype-element-assl.md)， [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[修剪](../../../analysis-services/scripting/properties/trimming-element-assl.md)|  
|派生元素|请参阅“备注”中的表。|  
  
## <a name="remarks"></a>Remarks  
 **DataItem**数据类型用于任何可绑定的数据项，; 例如，度量值、 属性键和属性名称。 相关的详细信息和适用的默认值取决于用法；例如，属性名称必须为字符串。  
  
 实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]接受某些组的数据类型。 使用其他数据类型将导致错误，而不是隐式转换为一种有效类型。  
  
 下表列出了类型的元素**DataItem**。  
  
|父元素|类型的元素**DataItem**|注释|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)或[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|[数据源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**源**元素**DataItem**的类型必须为[RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)，或[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)或[InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|**源**元素**DataItem**的类型必须为[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
