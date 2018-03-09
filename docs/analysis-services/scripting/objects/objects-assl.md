---
title: "对象 (ASSL) |Microsoft 文档"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ea027aba8d0d49c752bd31569f84d0f0cec022bd
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="objects-assl"></a>对象 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
本参考部分包含在 Analysis Services 脚本语言 (ASSL) 架构中作为对象的每个元素的语法和用法信息。  
  
 尽管 ASSL 架构仅包含 XML 元素，从开发人员的角度来看，本部分中描述的元素的对象相对应，如**数据库**，**多维数据集**，和**维度**对象，包含的实例的对象的层次结构中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 对象在 ASSL 架构中从不是叶级元素，而是包含了子元素和与对象属性对应的元素。  
  
 在少数情况下，架构中显示为属性的叶级元素可归类为对象，这是因为该元素的类型是对象类型。 例如，**源**的**维度**对象属于类型**DimensionBinding**。  
  
## <a name="in-this-section"></a>本節內容  
  
|元素|Description|  
|-------------|-----------------|  
|[帐户元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|包含有关中的帐户类型的详细信息[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[Action 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|包含 [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) 或 [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) 元素中提供的操作的相关信息。|  
|[聚合元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|定义为单个聚合[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。|  
|[AggregationDesign 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|定义一组可由数据库中的多个分区共享的聚合定义。|  
|[AggregationInstance 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|定义分区的聚合实例。|  
|[AlgorithmParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|定义了一个参数使用的算法[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[AllMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|包含的转换是为标题的所有成员的[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。|  
|[批注元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|包含用于扩展 ASSL 架构的元素。|  
|[Assembly 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集或 COM 动态链接库 (DLL) 与关联[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[Attribute 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|包含对属性的说明。|  
|[AttributeAllMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|包含的转换是为标题的所有成员的[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)元素。|  
|[AttributePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|定义的权限的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素对中的各个维度的特性[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[AttributeRelationship 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|提供有关两个属性之间的关系的详细信息。|  
|[块元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|包含全部或部分二进制内容组成[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[计算元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|一个具有计算 Asssociates[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[CalculationProperty 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|包含集合的计算中使用的用户界面属性[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)元素。|  
|[CaptionColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|定义提供属性标题的列。|  
|[CellPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|描述的权限的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素对中的各个单元格[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[列元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|描述与父元素关联的列集合中的一列。|  
|[Command 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|定义可在 Commands 集合的父元素的上下文中使用的命令。|  
|[多维数据集元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|定义正则、 虚拟的或链接的多维数据集在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)][数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[CubePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|定义的特定成员的权限[角色](../../../analysis-services/scripting/objects/role-element-assl.md)中特定元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[CustomRollupColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|定义提供自定义汇总公式的列的详细信息。|  
|[CustomRollupPropertiesColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|定义用于提供自定义汇总公式属性的列的详细信息。|  
|[数据元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|包含 (中的子集合**块**元素) 的二进制内容组成[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[数据库元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|定义 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库。|  
|[DatabasePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|定义中的默认权限[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)的特定元素[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素。|  
|[数据源元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|定义中的数据源[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[DataSourcePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|定义中的默认权限[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)特定的数据类型[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素。|  
|[DataSourceView 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|定义数据源视图使用[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[维度元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|定义维度。|  
|[DimensionPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|定义属于特定的权限[角色](../../../analysis-services/scripting/objects/role-element-assl.md)特定数据库维度或多维数据集维度元素。|  
|[ErrorConfiguration 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|指定在处理父元素时可能出现的错误的处理设置。|  
|[Event 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|定义一个事件，它作为的一部分捕获[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素。|  
|[文件元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|定义一个组成的文件[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)元素。|  
|[ForeignKeyColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|标识加入关系数据源的父表的联接。|  
|[组元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|定义一组绑定到某个属性的成员。|  
|[层次结构元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|定义维度中的层次结构。|  
|[IncrementalProcessingNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|包含信息[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关要执行以确定的进度增量处理的查询的元素。|  
|[KeyColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|包含某个列的定义，该列用作属性键或属性键的一部分。|  
|[Kpi 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|在定义关键绩效指标 (KPI)[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[级别元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|定义中的级别[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。|  
|[MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|包含与关联的多维表达式 (MDX) 脚本信息[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[度量值元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|定义一个度量值。|  
|[MeasureGroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|定义一组属于同一粒度级别的度量值。|  
|[成员元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|包含的一个成员的名称[组](../../../analysis-services/scripting/objects/group-element-assl.md)元素或[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素。|  
|[MiningModel 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|定义一个数据挖掘模型。|  
|[MiningModelPermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|定义的权限成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有对单个[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[MiningStructure 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|定义一组挖掘模型的结构。|  
|[MiningStructurePermission 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|定义的权限的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有对单个[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。|  
|[ModelingFlag 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|包含挖掘结构或挖掘模型中的某个列的建模标志。|  
|[NameColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|标识提供父元素名称的列。|  
|[NamingTemplateTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|提供的本地化的翻译**NamingTemplate**的父元素[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)数据类型。|  
|[分区元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|定义的分区[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素或扩展的行中的分区绑定[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。|  
|[透视元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|定义的透视的详细信息[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[ProactiveCaching 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|定义父元素的主动缓存设置。|  
|[QueryNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|包含信息[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关要执行来确定是否已修改数据源的查询的元素。|  
|[ReportFormatParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|包含的名称和值的一个参数，指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]报表格式在运行时。|  
|[ReportParameter 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|包含在运行时传递给 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表的参数的名称和值。|  
|[Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|包含有关安全角色的信息。|  
|[服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。|  
|[ServerProperty 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|定义与关联的服务器属性[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。|  
|[SkippedLevelsColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|提供列的详细信息，该列存储每个成员及其父级之间跳过的（空的）级别数。|  
|[SourceMeasureGroup 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|标识用作挖掘结构列的数据源的度量值组。|  
|[TableNotification 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|包含信息[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关的表或视图已修改的数据源中的元素。|  
|[跟踪元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|定义可查询的跟踪。|  
|[转换元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|提供的本地化的翻译的父级[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)集合。|  
|[UnaryOperatorColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|定义提供一元运算符的列的详细信息。|  
|[UnknownMemberTranslation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|包含的转换是为标题[UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)元素[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)元素。|  
|[ValueColumn 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|标识提供父元素值的列。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
