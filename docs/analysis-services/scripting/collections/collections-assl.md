---
title: "集合 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- collections [Analysis Services Scripting Language]
- Analysis Services Scripting Language, collections
- ASSL, collections
ms.assetid: 072b8c6b-1550-4cab-ae64-ba0e3e60b059
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9751d6b4052575c85abf41f745817def8f7ae75
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="collections-assl"></a>集合 (ASSL)
  本参考部分包含在 Analysis Services 脚本语言 (ASSL) 架构中作为集合的每个元素的语法和用法信息。  
  
 尽管 ASSL 架构仅包含 XML 元素，从开发人员的角度来看，本部分中描述的元素对应于集合的对象，如**维度**和**多维数据集**集合。  
  
 集合是主要的对象元素，在其中复数名词指定集合的集合 (有关示例，**多维数据集**)，和该集合包含相同名词的单数中指定的元素 (例如， **多维数据集**)。  
  
 在某些情况下，架构不符合此一般规则。 例如， **ClassifiedColumns**集合包含**ClassifiedColumnID**元素。  
  
 在其他情况下，集合包含的元素与对象属性对应，而不是对象。 例如，**别名**集合包含**别名**属性，其中每个是一个简单的字符串值。  
  
|元素|Description|  
|-------------|-----------------|  
|[Accounts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)|包含在中定义的帐户类型的集合[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[操作元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)|包含的操作的集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[AggregationDesigns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|包含可在数据库的多个分区中共享的聚合设计的集合。|  
|[AggregationInstances 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|包含集合中定义的聚合实例[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。|  
|[聚合元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)|包含的聚合为定义集合[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素。|  
|[AlgorithmParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|包含的使用的算法的参数集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[别名元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aliases-element-assl.md)|包含的集合[别名](../../../analysis-services/scripting/properties/alias-element-assl.md)与关联的元素[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)元素|  
|[AllMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)|包含的集合[转换](../../../analysis-services/scripting/objects/translation-element-assl.md)的所有成员的标题元素[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。|  
|[Annotations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/annotations-element-assl.md)|包含的集合[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)与父元素关联的元素。|  
|[Assemblies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)|包含的集合[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)与关联的元素[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[AttributeAllMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributeallmembertranslations-element-assl.md)|包含维度“全部”成员标题对应的翻译的集合。|  
|[AttributePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|包含单个属性权限的集合[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素上的特定维度[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[AttributeRelationships 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md)|包含的集合[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)属性的元素。|  
|[属性元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)|包含关联维度的属性的集合。|  
|[块元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)|包含表示的二进制内容组成的二进制数据块的集合[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|包含的集合[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)与关联的元素[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)元素。|  
|[计算元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculations-element-assl.md)|包含的集合[PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)与关联的元素[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[CellPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|包含的单元格关联的权限的集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[ClassifiedColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/classifiedcolumns-element-assl.md)|包含被归类的相关列的集合[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)元素。|  
|[Columns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)|包含与父元素关联的列的集合。|  
|[命令元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/commands-element-assl.md)|包含与某个 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 元素关联的 [Command](../../../analysis-services/scripting/objects/command-element-assl.md) 元素的集合。|  
|[CubePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md)|包含的权限适用于集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/cubes-element-assl.md)|包含的集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)与关联的元素[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[DatabasePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|包含的集合[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)与关联的元素[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[数据库元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/databases-element-assl.md)|包含的集合[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)与关联的元素[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。|  
|[DataSources 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasources-element-assl.md)|包含的集合[DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)与关联的元素[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)数据类型。|  
|[DataSourcePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|包含的集合[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)与关联的元素[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[DataSourceViews 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/datasourceviews-element-assl.md)|包含的集合[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)与关联的元素[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[DimensionPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/dimensionpermissions-element-assl.md)|包含的权限适用于集合[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)元素或[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)元素。|  
|[维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/dimensions-element-assl.md)|包含与父元素关联的维度的集合。|  
|[Events 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)|定义由捕获的事件元素的集合[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)。|  
|[Files 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/files-element-assl.md)|包含的集合[文件](../../../analysis-services/scripting/objects/file-element-assl.md)构成元素[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)元素。|  
|[ForeignKeyColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/foreignkeycolumns-element-assl.md)|包含列的集合，这些列指定与关系数据源的父表的联接。|  
|[组元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/groups-element-assl.md)|包含绑定到某个属性的成员组的集合。|  
|[Hierarchies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)|包含的集合[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)与父元素关联的元素。|  
|[IncrementalProcessingNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/incrementalprocessingnotifications-element-assl.md)|包含的集合[IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)元素信息提供给[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关查询执行以确定的进度的元素增量处理。|  
|[KeyColumns 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|包含的集合[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)元素定义的父对象。|  
|[Kpi 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/kpis-element-assl.md)|包含的集合[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)与父元素关联的元素。|  
|[Levels 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/levels-element-assl.md)|包含的集合[级别](../../../analysis-services/scripting/objects/level-element-assl.md)中的元素[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。|  
|[Mdxscript 被元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)|包含的集合[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)与关联的元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[Measuregroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|包含的集合[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)与父元素关联的元素。|  
|[度量值元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/measures-element-assl.md)|包含的集合[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)与父元素关联的元素。|  
|[Members 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/members-element-assl.md)|包含的集合[成员](../../../analysis-services/scripting/objects/member-element-assl.md)父元素的元素。|  
|[MiningModelPermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|包含的有关权限的集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[MiningModels 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)|包含的集合[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)与关联的元素[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)。|  
|[添加元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|包含的权限的集合上[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。|  
|[MiningStructures 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|包含的集合[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)中的元素[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[ModelingFlags 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)|包含的集合[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)中某一列的元素[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)。|  
|[NamingTemplateTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md)|提供的本地化翻译的集合[NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)元素的父[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)。|  
|[分区元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/partitions-element-assl.md)|包含的集合[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)所使用的元素[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素或构成超的行的分区绑定的集合[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。|  
|[透视元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|包含的集合[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)与关联的元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[QueryNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/querynotifications-element-assl.md)|包含的集合[QueryNotification](../../../analysis-services/scripting/objects/querynotification-element-assl.md)元素信息提供给[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关查询执行来确定是否已修改数据源的元素。|  
|[ReportFormatParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md)|包含的集合[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)元素[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)元素。|  
|[ReportParameters 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/reportparameters-element-assl.md)|包含的集合[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)元素[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)元素。|  
|[角色元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/roles-element-assl.md)|包含在父元素下定义的 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 元素的集合。|  
|[ServerProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|包含的集合[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)与关联的元素[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。|  
|[TableNotifications 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/tablenotifications-element-assl.md)|包含的集合[TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)元素中提供信息[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关表或视图中的数据源已被修改的元素。|  
|[跟踪元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/traces-element-assl.md)|包含与某个 [Server](../../../analysis-services/scripting/objects/server-element-assl.md) 元素关联的 [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) 元素的集合。|  
|[翻译元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/translations-element-assl.md)|包含的集合[转换](../../../analysis-services/scripting/objects/translation-element-assl.md)与父元素关联的元素。|  
|[UnknownMemberTranslations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/unknownmembertranslations-element-assl.md)|包含的翻译的标题的集合[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)维度元素。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
