---
title: "维度数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Dimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Dimension data type
ms.assetid: 3fe6adc2-5206-44c3-a689-a731705f43ca
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aec187232caf3bab2c6108c7424ba75bb49795e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dimension-data-type-assl"></a>Dimension 数据类型 (ASSL)
  定义表示数据库维度的基元数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Source>...</Source>  
   <MiningModelID>...</MiningModelID>  
   <Type>...</Type>  
   <UnknownMember>...</UnknownMember>  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   <ErrorConfiguration>...</ErrorConfiguration>  
   <StorageMode>...</StorageMode>  
   <WriteEnabled>...</WriteEnabled>  
   <ProcessingPriority>...</ProcessingPriority>  
   <LastProcessed>...</LastProcessed>  
   <DimensionPermissions>...</DimensionPermissions>  
   <DependsOnDimensionID>...</DependsOnDimensionID>  
   <Language>...</Language>  
   <Collation>...</Collation>  
   <UnknownMemberName>...</UnknownMemberName>  
   <UnknownMemberTranslations>...</UnknownMemberTranslations>  
   <State>...</State>  
   <ProactiveCaching>...</ProactiveCaching>  
   <ProcessingMode>...</ProcessingMode>  
   <CurrentStorageMode>...</CurrentStorageMode>  
   <Translations>...</Translations>  
   <Attributes>...</Attributes>  
   <AttributeAllMemberName>...</AttributeAllMemberName>  
   <AttributeAllMemberTranslations>...</AttributeAllMemberTranslations>  
   <Hierarchies>...</Hierarchies>  
   <Relationships>...</Annotations>  
   <Annotations>...</Annotations>  
</Dimension>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)、[AttributeAllMemberName](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md)、[AttributeAllMemberTranslations](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)、[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md)、[Collation](../../../analysis-services/scripting/properties/collation-element-assl.md)、[CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)、[CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)、[DependsOnDimensionID](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md)、[Description](../../../analysis-services/scripting/properties/description-element-assl.md)、[DimensionPermissions](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)、[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)、[Hierarchies](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)、[ID](../../../analysis-services/scripting/properties/id-element-assl.md)、[Language](../../../analysis-services/scripting/properties/language-element-assl.md)、[LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)、[LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)、[MdxMissingMemberMode](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md)、[MiningModelID](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md)、[Name](../../../analysis-services/scripting/properties/name-element-assl.md)、[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)、[ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)、[ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)、[Relationships](../../../analysis-services/scripting/collections/relationships-element-assl.md)、[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)、[State](../../../analysis-services/scripting/properties/state-element-assl.md)、[StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md)、[Translations](../../../analysis-services/scripting/collections/translations-element-assl.md)、[Type](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)、[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)、[UnknownMemberName](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)、[UnknownMemberTranslations](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)、[WriteEnabled](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|  
|派生元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 此数据类型在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下具有以下验证。  
  
-   *WriteEnabled* 子元素必须设置为 **False**  
  
-   *UnknownMember* 子元素必须设置为 **AutomaticNull**  
  
-   所有唯一属性都必须将 *NullProcessing* 子元素设置为 **Error**  
  
 在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下不支持以下子属性。  
  
-   *DimensionPermissions*  
  
-   *MiningModelID*  
  
-   *ProactiveCaching*  
  
 分析管理对象 (AMO) 对象模型中的相应元素<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>，和<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
