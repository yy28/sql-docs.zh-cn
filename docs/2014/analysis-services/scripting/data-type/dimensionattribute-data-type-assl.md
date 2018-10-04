---
title: DimensionAttribute 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4624e963a9bca0d7850d2936291d3a7515cac25f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106847"
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
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)， [AttributeHierarchyDisplayFolder](../properties/displayfolder-element-assl.md)， [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)， [AttributeHierarchyOptimizedState](../properties/state-element-assl.md)， [AttributeHierarchyOrdered](../properties/attributehierarchyordered-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeRelationships](../collections/relationships-element-assl.md)， [CustomRollupColumn](../objects/column-element-assl.md)， [CustomRollupPropertiesColumn](../objects/customrolluppropertiescolumn-element-assl.md)， [DefaultMember](../objects/member-element-assl.md)，[说明](../properties/description-element-assl.md)， [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)， [EstimatedCount](../properties/estimatedcount-element-assl.md)， [ID](../properties/id-element-assl.md)， [InstanceSelection](../properties/instanceselection-element-assl.md)， [IsAggregatable](../properties/isaggregatable-element-assl.md)，[KeyColumns](../collections/columns-element-assl.md)， [KeyUniquenessGuarantee](../properties/keyuniquenessguarantee-element-assl.md)， [MemberNamesUnique](../properties/membernamesunique-element-assl.md)， [MembersWithData](../objects/data-element-assl.md)， [MembersWithDataCaption](../properties/caption-element-assl.md)，[名称](../properties/name-element-assl.md)， [NameColumn](../objects/namecolumn-element-assl.md)， [NamingTemplate](../properties/namingtemplate-element-assl.md)， [NamingTemplateTranslations](../collections/translations-element-assl.md)， [OrderBy](../properties/orderby-element-assl.md)， [OrderByAttributeID](../properties/attributeid-element-assl.md)， [RootMemberIf](../properties/rootmemberif-element-assl.md)， [SkippedLevelsColumn](../objects/skippedlevelscolumn-element-assl.md)，[源](../properties/source-element-binding-assl.md)，[翻译](../collections/translations-element-assl.md)，[类型](../properties/type-element-dimensionattribute-assl.md)， [UnaryOperatorColumn](../objects/unaryoperatorcolumn-element-assl.md)，[使用情况](../properties/usage-element-dimensionattribute-assl.md)， [ValueColumn](../objects/valuecolumn-element-assl.md)|  
|派生元素|[特性](../objects/attribute-element-assl.md)([特性](../collections/attributes-element-assl.md)的集合[维度](../objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>备注  
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
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
