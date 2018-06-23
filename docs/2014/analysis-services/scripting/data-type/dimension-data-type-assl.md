---
title: 维度数据类型 (ASSL) |Microsoft 文档
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
- Dimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Dimension data type
ms.assetid: 3fe6adc2-5206-44c3-a689-a731705f43ca
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1451da2c20228e00b99482a7c9b43a92a8478154
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028034"
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
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[Annotations](../collections/annotations-element-assl.md)、[AttributeAllMemberName](../properties/name-element-assl.md)、[AttributeAllMemberTranslations](../collections/translations-element-assl.md)、[Attributes](../collections/attributes-element-assl.md)、[Collation](../properties/collation-element-assl.md)、[CreatedTimestamp](../properties/createdtimestamp-element-assl.md)、[CurrentStorageMode](../properties/storagemode-element-assl.md)、[DependsOnDimensionID](../properties/id-element-assl.md)、[Description](../properties/description-element-assl.md)、[DimensionPermissions](../collections/dimensionpermissions-element-assl.md)、[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)、[Hierarchies](../collections/hierarchies-element-assl.md)、[ID](../properties/id-element-assl.md)、[Language](../properties/language-element-assl.md)、[LastProcessed](../properties/lastprocessed-element-assl.md)、[LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)、[MdxMissingMemberMode](../properties/mdxmissingmembermode-element-assl.md)、[MiningModelID](../properties/miningmodelid-element-assl.md)、[Name](../properties/name-element-assl.md)、[ProactiveCaching](../objects/proactivecaching-element-assl.md)、[ProcessingMode](../properties/processingmode-element-assl.md)、[ProcessingPriority](../properties/processingpriority-element-assl.md)、[Relationships](../collections/relationships-element-assl.md)、[Source](../properties/source-element-binding-assl.md)、[State](../properties/state-element-assl.md)、[StorageMode](../properties/storagemode-element-assl.md)、[Translations](../collections/translations-element-assl.md)、[Type](../properties/type-element-dimension-assl.md)、[UnknownMember](../objects/member-element-assl.md)、[UnknownMemberName](../properties/unknownmembername-element-assl.md)、[UnknownMemberTranslations](../collections/unknownmembertranslations-element-assl.md)、[WriteEnabled](../properties/enabled-element-assl.md)|  
|派生元素|[Dimension](../objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 此数据类型在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下具有以下验证。  
  
-   *WriteEnabled*子元素必须设置为 `False`  
  
-   *UnknownMember*子元素必须设置为 `AutomaticNull`  
  
-   所有唯一属性都必须具有*NullProcessing*子元素设置为 `Error`  
  
 在 DeploymentMode 值 1 (SharePoint) 和 2（表格）下不支持以下子属性。  
  
-   *DimensionPermissions*  
  
-   *MiningModelID*  
  
-   *ProactiveCaching*  
  
 分析管理对象 (AMO) 对象模型中的相应元素<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>，和<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  