---
title: 集合 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a56b577f39c2b2f4ef7a4033203fcda9706d1370
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300987"
---
# <a name="collections-assl"></a>集合 (ASSL)
  本参考部分包含在 Analysis Services 脚本语言 (ASSL) 架构中作为集合的每个元素的语法和用法信息。  
  
 尽管 ASSL 架构只包含 XML 元素，但是从开发人员的角度来说，本节中介绍的元素与对象的集合（如 `Dimensions` 和 `Cubes` 集合）是对应的。  
  
 集合主要是对象元素的集合，其中复数名词指集合（例如，`Cubes`），而此名词的单数形式指该集合中包含的元素（例如，`Cube`）。  
  
 在某些情况下，架构不符合此一般规则。 例如，`ClassifiedColumns` 集合包含 `ClassifiedColumnID` 元素。  
  
 在其他情况下，集合包含的元素与对象属性对应，而不是对象。 例如，`Aliases` 集合包含 `Alias` 属性，每个属性都是一个简单字符串值。  
  
|元素|Description|  
|-------------|-----------------|  
|[帐户元素&#40;ASSL&#41;](accounts-element-assl.md)|包含集合中定义的帐户类型[数据库](../objects/database-element-assl.md)元素。|  
|[Actions 元素&#40;ASSL&#41;](actions-element-assl.md)|包含的操作的集合[多维数据集](../objects/cube-element-assl.md)或[角度来看](../objects/perspective-element-assl.md)元素。|  
|[AggregationDesigns 元素&#40;ASSL&#41;](aggregationdesigns-element-assl.md)|包含可在数据库的多个分区中共享的聚合设计的集合。|  
|[AggregationInstances 元素&#40;ASSL&#41;](aggregationinstances-element-assl.md)|包含在中定义的聚合实例的集合[分区](../objects/partition-element-assl.md)元素。|  
|[Aggregations 元素&#40;ASSL&#41;](aggregations-element-assl.md)|包含用于定义聚合的集合[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素。|  
|[AlgorithmParameters 元素&#40;ASSL&#41;](algorithmparameters-element-assl.md)|包含的使用的算法的参数集合[MiningModel](../objects/miningmodel-element-assl.md)元素。|  
|[Aliases 元素&#40;ASSL&#41;](aliases-element-assl.md)|包含的集合[别名](../properties/alias-element-assl.md)与关联的元素[帐户](../objects/account-element-assl.md)元素|  
|[AllMemberTranslations 元素&#40;ASSL&#41;](translations-element-assl.md)|包含的集合[翻译](../objects/translation-element-assl.md)元素的所有成员的标题对应[层次结构](../objects/hierarchy-element-assl.md)元素。|  
|[Annotations 元素&#40;ASSL&#41;](annotations-element-assl.md)|包含的集合[批注](../objects/annotation-element-assl.md)与父元素关联的元素。|  
|[程序集元素&#40;ASSL&#41;](assemblies-element-assl.md)|包含的集合[程序集](../objects/assembly-element-assl.md)与关联的元素[服务器](../objects/server-element-assl.md)元素或[数据库](../objects/database-element-assl.md)元素。|  
|[AttributeAllMemberTranslations 元素&#40;ASSL&#41;](attributeallmembertranslations-element-assl.md)|包含维度“全部”成员标题对应的翻译的集合。|  
|[AttributePermissions 元素&#40;ASSL&#41;](attributepermissions-element-assl.md)|包含的属性权限的个人的集合[角色](../objects/role-element-assl.md)上的特定维度的元素[多维数据集](../objects/cube-element-assl.md)元素。|  
|[AttributeRelationships 元素&#40;ASSL&#41;](relationships-element-assl.md)|包含的集合[AttributeRelationship](../objects/attributerelationship-element-assl.md)元素的属性。|  
|[Attributes 元素&#40;ASSL&#41;](attributes-element-assl.md)|包含关联维度的属性的集合。|  
|[阻止元素&#40;ASSL&#41;](blocks-element-assl.md)|包含表示的二进制内容的二进制数据块的集合[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[CalculationProperties 元素&#40;ASSL&#41;](calculationproperties-element-assl.md)|包含的集合[CalculationProperty](../objects/calculationproperty-element-assl.md)与关联的元素[MdxScript](../objects/mdxscript-element-assl.md)元素。|  
|[Calculations 元素&#40;ASSL&#41;](calculations-element-assl.md)|包含的集合[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)与关联的元素[角度来看](../objects/perspective-element-assl.md)元素。|  
|[CellPermissions 元素&#40;ASSL&#41;](cellpermissions-element-assl.md)|包含的单元格关联的权限的集合[多维数据集](../objects/cube-element-assl.md)元素。|  
|[ClassifiedColumns 元素&#40;ASSL&#41;](columns-element-assl.md)|包含按分类的相关列的集合[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)元素。|  
|[Columns 元素&#40;ASSL&#41;](columns-element-assl.md)|包含与父元素关联的列的集合。|  
|[命令元素&#40;ASSL&#41;](commands-element-assl.md)|包含与某个 [MdxScript](../objects/mdxscript-element-assl.md) 元素关联的 [Command](../objects/command-element-assl.md) 元素的集合。|  
|[CubePermissions 元素&#40;ASSL&#41;](cubepermissions-element-assl.md)|包含适用于权限的集合[多维数据集](../objects/cube-element-assl.md)元素。|  
|[多维数据集元素&#40;ASSL&#41;](cubes-element-assl.md)|包含的集合[多维数据集](../objects/cube-element-assl.md)与关联的元素[数据库](../objects/database-element-assl.md)元素。|  
|[DatabasePermissions 元素&#40;ASSL&#41;](databasepermissions-element-assl.md)|包含的集合[DatabasePermission](../objects/databasepermission-element-assl.md)与关联的元素[数据库](../objects/database-element-assl.md)元素。|  
|[Databases 元素&#40;ASSL&#41;](databases-element-assl.md)|包含的集合[数据库](../objects/database-element-assl.md)与关联的元素[Server](../objects/server-element-assl.md)元素。|  
|[DataSources 元素&#40;ASSL&#41;](datasources-element-assl.md)|包含的集合[DataSourcePermission](../objects/datasourcepermission-element-assl.md)与关联的元素[数据源](../data-type/datasource-data-type-assl.md)数据类型。|  
|[DataSourcePermissions 元素&#40;ASSL&#41;](datasourcepermissions-element-assl.md)|包含的集合[数据源](../objects/datasource-element-assl.md)与关联的元素[数据库](../objects/database-element-assl.md)元素。|  
|[DataSourceViews 元素&#40;ASSL&#41;](datasourceviews-element-assl.md)|包含的集合[DataSourceView](../objects/datasourceview-element-assl.md)与关联的元素[数据库](../objects/database-element-assl.md)元素。|  
|[DimensionPermissions 元素&#40;ASSL&#41;](dimensionpermissions-element-assl.md)|包含适用于权限的集合[维度](../objects/dimension-element-assl.md)元素或[CubePermission](../objects/cubepermission-element-assl.md)元素。|  
|[维度元素&#40;ASSL&#41;](dimensions-element-assl.md)|包含与父元素关联的维度的集合。|  
|[Events 元素&#40;ASSL&#41;](events-element-assl.md)|定义要捕获的事件元素的集合[跟踪](../objects/trace-element-assl.md)。|  
|[文件元素&#40;ASSL&#41;](files-element-assl.md)|包含的集合[文件](../objects/file-element-assl.md)构成元素[ClrAssembly](../data-type/assembly-data-type-assl.md)元素。|  
|[ForeignKeyColumns 元素&#40;ASSL&#41;](keycolumns-element-assl.md)|包含列的集合，这些列指定与关系数据源的父表的联接。|  
|[Groups 元素&#40;ASSL&#41;](groups-element-assl.md)|包含绑定到某个属性的成员组的集合。|  
|[Hierarchies 元素&#40;ASSL&#41;](hierarchies-element-assl.md)|包含的集合[层次结构](../objects/hierarchy-element-assl.md)与父元素关联的元素。|  
|[IncrementalProcessingNotifications 元素&#40;ASSL&#41;](incrementalprocessingnotifications-element-assl.md)|包含的集合[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)元素的信息提供给[ProactiveCaching](../objects/proactivecaching-element-assl.md)为确定的进度而执行的查询元素增量处理。|  
|[KeyColumns 元素&#40;ASSL&#41;](keycolumns-element-assl.md)|包含的集合[KeyColumn](../objects/column-element-assl.md)元素定义的父对象。|  
|[Kpi 元素&#40;ASSL&#41;](kpis-element-assl.md)|包含的集合[Kpi](../objects/kpi-element-assl.md)与父元素关联的元素。|  
|[级别元素&#40;ASSL&#41;](levels-element-assl.md)|包含的集合[级别](../objects/level-element-assl.md)中的元素[层次结构](../objects/hierarchy-element-assl.md)元素。|  
|[MdxScripts 元素&#40;ASSL&#41;](mdxscripts-element-assl.md)|包含的集合[MdxScript](../objects/mdxscript-element-assl.md)与关联的元素[多维数据集](../objects/cube-element-assl.md)元素。|  
|[MeasureGroups 元素&#40;ASSL&#41;](measuregroups-element-assl.md)|包含的集合[MeasureGroup](../objects/group-element-assl.md)与父元素关联的元素。|  
|[测量元素&#40;ASSL&#41;](measures-element-assl.md)|包含的集合[度量值](../objects/measure-element-assl.md)与父元素关联的元素。|  
|[Members 元素&#40;ASSL&#41;](members-element-assl.md)|包含的集合[成员](../objects/member-element-assl.md)父元素的元素。|  
|[MiningModelPermissions 元素&#40;ASSL&#41;](miningmodelpermissions-element-assl.md)|包含的权限的集合[MiningModel](../objects/miningmodel-element-assl.md)元素。|  
|[MiningModels 元素&#40;ASSL&#41;](miningmodels-element-assl.md)|包含的集合[MiningModel](../objects/miningmodel-element-assl.md)与关联的元素[MiningStructure](../objects/miningstructure-element-assl.md)。|  
|[MiningStructurePermissions 元素&#40;ASSL&#41;](miningstructurepermissions-element-assl.md)|在包含的权限的集合[MiningStructure](../objects/miningstructure-element-assl.md)元素。|  
|[MiningStructures 元素&#40;ASSL&#41;](miningstructures-element-assl.md)|包含的集合[MiningStructure](../objects/miningstructure-element-assl.md)中的元素[数据库](../objects/database-element-assl.md)元素。|  
|[ModelingFlags 元素&#40;ASSL&#41;](modelingflags-element-assl.md)|包含的集合[ModelingFlag](../objects/modelingflag-element-assl.md)元素中的列[MiningStructure](../objects/miningstructure-element-assl.md)或[MiningModel](../objects/miningmodel-element-assl.md)。|  
|[NamingTemplateTranslations 元素&#40;ASSL&#41;](namingtemplatetranslations-element-assl.md)|提供的本地化翻译的集合[NamingTemplate](../properties/namingtemplate-element-assl.md)父元素[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)。|  
|[分区元素&#40;ASSL&#41;](partitions-element-assl.md)|包含的集合[分区](../objects/partition-element-assl.md)所使用的元素[MeasureGroup](../objects/group-element-assl.md)元素或构成掉的行的分区绑定的集合[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。|  
|[Perspectives 元素&#40;ASSL&#41;](perspectives-element-assl.md)|包含的集合[角度来看](../objects/perspective-element-assl.md)与关联的元素[多维数据集](../objects/cube-element-assl.md)元素。|  
|[QueryNotifications 元素&#40;ASSL&#41;](querynotifications-element-assl.md)|包含的集合[QueryNotification](../objects/querynotification-element-assl.md)元素的信息提供给[ProactiveCaching](../objects/proactivecaching-element-assl.md)执行，以确定是否已修改数据源的查询的元素。|  
|[ReportFormatParameters 元素&#40;ASSL&#41;](reportformatparameters-element-assl.md)|包含的集合[ReportFormatParameter](../objects/reportformatparameter-element-asl.md)元素[ReportAction](../data-type/action-data-type-assl.md)元素。|  
|[ReportParameters 元素&#40;ASSL&#41;](reportparameters-element-assl.md)|包含的集合[ReportParameter](../objects/reportparameter-element-assl.md)元素[ReportAction](../data-type/action-data-type-assl.md)元素。|  
|[Roles 元素&#40;ASSL&#41;](roles-element-assl.md)|包含在父元素下定义的 [Role](../objects/role-element-assl.md) 元素的集合。|  
|[ServerProperties 元素&#40;ASSL&#41;](serverproperties-element-assl.md)|包含的集合[ServerProperty](../objects/serverproperty-element-assl.md)与关联的元素[Server](../objects/server-element-assl.md)元素。|  
|[TableNotifications 元素&#40;ASSL&#41;](tablenotifications-element-assl.md)|包含的集合[TableNotification](../objects/tablenotification-element-assl.md)提供的信息的元素[ProactiveCaching](../objects/proactivecaching-element-assl.md)有关表或视图的数据源中修改过的元素。|  
|[跟踪元素&#40;ASSL&#41;](traces-element-assl.md)|包含与某个 [Server](../objects/server-element-assl.md) 元素关联的 [Trace](../objects/trace-element-assl.md) 元素的集合。|  
|[Translations 元素&#40;ASSL&#41;](translations-element-assl.md)|包含的集合[翻译](../objects/translation-element-assl.md)与父元素关联的元素。|  
|[UnknownMemberTranslations 元素&#40;ASSL&#41;](unknownmembertranslations-element-assl.md)|包含的标题的翻译的集合[UnknownMember](../properties/unknownmember-element-assl.md)维度的元素。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
