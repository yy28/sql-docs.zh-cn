---
title: DimensionAttribute 数据类型 (ASSL) |Microsoft 文档
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
- DimensionAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DimensionAttribute
helpviewer_keywords:
- DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2d022a0bfb5c11efe38694b614bd65676fb3ee28
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014636"
---
# <a name="dimensionattribute-data-type-assl"></a>DimensionAttribute 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示维度中的属性。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Usage>...</Usage>  
   <Source>...</Source>  
   <EstimatedCount>...</EstimatedCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <ValueColumn>...</ValueColumn>  
   <Translations>...</Translations>  
   <AttributeRelationships>...</AttributeRelationships>  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <RootMemberIf>...</RootMemberIf>  
   <OrderBy>...</OrderBy>  
   <DefaultMember>...</DefaultMember>  
   <OrderByAttributeID>...</OrderByAttributeID>  
   <SkippedLevelsColumn>...</SkippedLevelsColumn>  
   <NamingTemplate>...</NamingTemplate>  
   <MembersWithData>...</MembersWithData>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   <NamingTemplateTranslations>...</NamingTemplateTranslations>  
   <CustomRollupColumn>...</CustomRollupColumn>  
   <CustomRollupPropertiesColumn>...</CustomRollupPropertiesColumn>  
   <UnaryOperatorColumn>...</UnaryOperatorColumn>  
   <AttributeHierarchyOrdered>...</AttributeHierarchyOrdered>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <IsAggregatable>...</IsAggregatable>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <AttributeHierarchyDisplayFolder>...</AttributeHierarchyDisplayFolder>  
   <KeyUniquenessGuarantee>...<KeyUniquenessGuarantee>  
   <InstanceSelection>...</InstanceSelection>  
   <Annotations>...</Annotations>  
</DimensionAttribute>  
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
|子元素|[Annotations](../collections/annotations-element-assl.md), [AttributeHierarchyDisplayFolder](../properties/displayfolder-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md), [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [AttributeHierarchyOrdered](../properties/attributehierarchyordered-element-assl.md), [AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeRelationships](../collections/relationships-element-assl.md), [CustomRollupColumn](../objects/column-element-assl.md), [CustomRollupPropertiesColumn](../objects/customrolluppropertiescolumn-element-assl.md), [DefaultMember](../objects/member-element-assl.md), [Description](../properties/description-element-assl.md), [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../properties/discretizationmethod-element-assl.md), [EstimatedCount](../properties/estimatedcount-element-assl.md), [ID](../properties/id-element-assl.md), [InstanceSelection](../properties/instanceselection-element-assl.md), [IsAggregatable](../properties/isaggregatable-element-assl.md), [KeyColumns](../collections/columns-element-assl.md), [KeyUniquenessGuarantee](../properties/keyuniquenessguarantee-element-assl.md), [MemberNamesUnique](../properties/membernamesunique-element-assl.md), [MembersWithData](../objects/data-element-assl.md), [MembersWithDataCaption](../properties/caption-element-assl.md), [Name](../properties/name-element-assl.md), [NameColumn](../objects/namecolumn-element-assl.md), [NamingTemplate](../properties/namingtemplate-element-assl.md), [NamingTemplateTranslations](../collections/translations-element-assl.md), [OrderBy](../properties/orderby-element-assl.md), [OrderByAttributeID](../properties/attributeid-element-assl.md), [RootMemberIf](../properties/rootmemberif-element-assl.md), [SkippedLevelsColumn](../objects/skippedlevelscolumn-element-assl.md), [Source](../properties/source-element-binding-assl.md), [Translations](../collections/translations-element-assl.md), [Type](../properties/type-element-dimensionattribute-assl.md), [UnaryOperatorColumn](../objects/unaryoperatorcolumn-element-assl.md), [Usage](../properties/usage-element-dimensionattribute-assl.md), [ValueColumn](../objects/valuecolumn-element-assl.md)|  
|派生元素|[属性](../objects/attribute-element-assl.md)([属性](../collections/attributes-element-assl.md)集合[维度](../objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 在 DeploymentMode 配置属性值为 1 和 2（SharePoint 和表格模式，用于运行 PowerPivot 和表格模型数据库）的情况下运行服务时，具有以下限制：  
  
-   Usage 元素只接受 KEY 或 REGULAR 值。  
  
-   IsAggregatable 元素不能为 false。  
  
-   OrderBy 元素只接受 KEY 或 PROPERTYKEY 值。  
  
-   计算列不能是表中的主键。  
  
-   计算列不能在本地中包含 DataSize。  
  
-   对于每个计算列，在保存属性定义之前执行语法验证。  
  
-   对于 AttributeRelationships，RelationshipType 必须设置值 Flexible。  
  
-   由“RowNumber”标识的属性“RowNumber”必须具有整数类型。  
  
-   只有“RowNumber”属性才能具有 RowNumberBinding 类型的 KeyBinding。  
  
-   除“RowNumber”外的所有属性都必须相对于该键具有基数 1，除非该属性本身是键。  
  
-   在 OrderBy 指定的列也是 PropertyKey 时，OrderByAttributeId 不能指向行号列。  
  
-   用作键的属性应该与所有其他属性相关；不支持其他类型的关系。  
  
-   NullProcessing 元素不能设置为“UnknownMember”。  
  
-   绑定不能设置为“Value”。  
  
 在 DeploymentMode 配置属性值为 1 和 2（SharePoint 和表格模式，用于运行 PowerPivot 和表格模型数据库）的情况下运行服务时，不支持以下元素：  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   数据源  
  
-   UnaryOperatorColumn  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  