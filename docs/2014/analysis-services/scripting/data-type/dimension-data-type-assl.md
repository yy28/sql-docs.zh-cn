---
title: 维度数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Dimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Dimension data type
ms.assetid: 3fe6adc2-5206-44c3-a689-a731705f43ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af61be445ec8b8a0ce71de56d17391ef4c30304b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093437"
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
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[Annotations](../collections/annotations-element-assl.md)、[AttributeAllMemberName](../properties/name-element-assl.md)、[AttributeAllMemberTranslations](../collections/translations-element-assl.md)、[Attributes](../collections/attributes-element-assl.md)、[Collation](../properties/collation-element-assl.md)、[CreatedTimestamp](../properties/createdtimestamp-element-assl.md)、[CurrentStorageMode](../properties/storagemode-element-assl.md)、[DependsOnDimensionID](../properties/id-element-assl.md)、[Description](../properties/description-element-assl.md)、[DimensionPermissions](../collections/dimensionpermissions-element-assl.md)、[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)、[Hierarchies](../collections/hierarchies-element-assl.md)、[ID](../properties/id-element-assl.md)、[Language](../properties/language-element-assl.md)、[LastProcessed](../properties/lastprocessed-element-assl.md)、[LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)、[MdxMissingMemberMode](../properties/mdxmissingmembermode-element-assl.md)、[MiningModelID](../properties/miningmodelid-element-assl.md)、[Name](../properties/name-element-assl.md)、[ProactiveCaching](../objects/proactivecaching-element-assl.md)、[ProcessingMode](../properties/processingmode-element-assl.md)、[ProcessingPriority](../properties/processingpriority-element-assl.md)、[Relationships](../collections/relationships-element-assl.md)、[Source](../properties/source-element-binding-assl.md)、[State](../properties/state-element-assl.md)、[StorageMode](../properties/storagemode-element-assl.md)、[Translations](../collections/translations-element-assl.md)、[Type](../properties/type-element-dimension-assl.md)、[UnknownMember](../objects/member-element-assl.md)、[UnknownMemberName](../properties/unknownmembername-element-assl.md)、[UnknownMemberTranslations](../collections/unknownmembertranslations-element-assl.md)、[WriteEnabled](../properties/enabled-element-assl.md)|  
|派生元素|[Dimension](../objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 此数据类型在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下具有以下验证。  
  
-   *WriteEnabled*子元素必须设置为 `False`  
  
-   *UnknownMember*子元素必须设置为 `AutomaticNull`  
  
-   所有唯一属性必须具有*NullProcessing*子元素设置为 `Error`  
  
 在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下不支持以下子属性。  
  
-   *DimensionPermissions*  
  
-   *MiningModelID*  
  
-   *ProactiveCaching*  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>，并<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
