---
title: "DimensionAttribute 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DimensionAttribute Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DimensionAttribute
helpviewer_keywords: DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 722dc94344e144445f07664f54282ac99f1dcdd7
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="dimensionattribute-data-type-assl"></a>DimensionAttribute 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义表示维度中的属性的基元数据类型。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeHierarchyDisplayFolder](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md)， [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)， [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)， [AttributeHierarchyOrdered](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md)， [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)， [AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)， [CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)， [CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)， [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)， [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[InstanceSelection](../../../analysis-services/scripting/properties/instanceselection-element-assl.md)， [IsAggregatable](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md)， [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)， [KeyUniquenessGuarantee](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md)， [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)， [MembersWithData](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)， [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)， [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)， [NamingTemplateTranslations](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)， [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md)， [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)，[其 RootMemberIf](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md)， [SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)， [源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)，[类型](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md)， [UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)，[用法](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)， [ValueColumn](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|  
|派生元素|[属性](../../../analysis-services/scripting/objects/attribute-element-assl.md)([属性](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 以下限制适用 deploymentmode 的情况下配置属性值 1 和 2 中运行服务时 (SharePoint 和表格模式下，用于运行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格模型数据库):  
  
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
  
 1 和 2 的属性值在 deploymentmode 的情况下配置中运行服务时，不支持以下元素 (SharePoint 和表格模式下，用于运行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格模型数据库):  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
