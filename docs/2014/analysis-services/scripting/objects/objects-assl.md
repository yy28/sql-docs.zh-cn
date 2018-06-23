---
title: 对象 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 246126f6ec82a104b05687c088c0bf3d2a614da6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025342"
---
# <a name="objects-assl"></a>对象 (ASSL)
  本参考部分包含在 Analysis Services 脚本语言 (ASSL) 架构中作为对象的每个元素的语法和用法信息。  
  
 尽管 ASSL 架构仅包含 XML 元素，从开发人员的角度来看，本部分中描述的元素的对象相对应，如`Database`， `Cube`，和`Dimension`对象，包含的对象的层次结构中实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 对象在 ASSL 架构中从不是叶级元素，而是包含了子元素和与对象属性对应的元素。  
  
 在少数情况下，架构中显示为属性的叶级元素可归类为对象，这是因为该元素的类型是对象类型。 例如，`Source` 对象的 `Dimension` 为 `DimensionBinding` 类型。  
  
## <a name="in-this-section"></a>本节内容  
  
|元素|Description|  
|-------------|-----------------|  
|[帐户元素&#40;ASSL&#41;](account-element-assl.md)|包含有关中的帐户类型的详细信息[数据库](database-element-assl.md)元素。|  
|[Action 元素&#40;ASSL&#41;](action-element-assl.md)|包含有关中可用的操作信息[多维数据集](cube-element-assl.md)元素或[透视](perspective-element-assl.md)元素。|  
|[聚合元素&#40;ASSL&#41;](aggregation-element-assl.md)|定义为单个聚合[分区](partition-element-assl.md)元素。|  
|[AggregationDesign 元素&#40;ASSL&#41;](aggregationdesign-element-assl.md)|定义一组可由数据库中的多个分区共享的聚合定义。|  
|[AggregationInstance 元素&#40;ASSL&#41;](aggregationinstance-element-assl.md)|定义分区的聚合实例。|  
|[AlgorithmParameter 元素&#40;ASSL&#41;](algorithmparameter-element-assl.md)|定义了一个参数使用的算法[MiningModel](miningmodel-element-assl.md)元素。|  
|[AllMemberTranslation 元素&#40;ASSL&#41;](translation-element-assl.md)|包含的转换是为标题的所有成员的[层次结构](hierarchy-element-assl.md)元素。|  
|[批注元素&#40;ASSL&#41;](annotation-element-assl.md)|包含用于扩展 ASSL 架构的元素。|  
|[Assembly 元素&#40;ASSL&#41;](assembly-element-assl.md)|表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集或 COM 动态链接库 (DLL) 与关联[服务器](server-element-assl.md)元素或[数据库](database-element-assl.md)元素。|  
|[属性元素&#40;ASSL&#41;](attribute-element-assl.md)|包含对属性的说明。|  
|[AttributeAllMemberTranslation 元素&#40;ASSL&#41;](attributeallmembertranslation-element-assl.md)|包含的转换是为标题的所有成员的[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)元素。|  
|[AttributePermission 元素&#40;ASSL&#41;](attributepermission-element-assl.md)|定义的权限的成员[角色](role-element-assl.md)元素对中的各个维度的特性[多维数据集](cube-element-assl.md)元素。|  
|[AttributeRelationship 元素&#40;ASSL&#41;](attributerelationship-element-assl.md)|提供有关两个属性之间的关系的详细信息。|  
|[阻止元素&#40;ASSL&#41;](block-element-assl.md)|包含全部或部分二进制内容组成[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[计算元素&#40;ASSL&#41;](calculation-element-assl.md)|一个具有计算 Asssociates[透视](perspective-element-assl.md)元素。|  
|[CalculationProperty 元素&#40;ASSL&#41;](calculationproperty-element-assl.md)|包含集合的计算中使用的用户界面属性[MdxScript](mdxscript-element-assl.md)元素。|  
|[CaptionColumn 元素&#40;ASSL&#41;](column-element-assl.md)|定义提供属性标题的列。|  
|[CellPermission 元素&#40;ASSL&#41;](cellpermission-element-assl.md)|描述的权限的成员[角色](role-element-assl.md)元素对中的各个单元格[多维数据集](cube-element-assl.md)元素。|  
|[列元素&#40;ASSL&#41;](column-element-assl.md)|描述与父元素关联的列集合中的一列。|  
|[命令元素&#40;ASSL&#41;](command-element-assl.md)|定义可在 Commands 集合的父元素的上下文中使用的命令。|  
|[多维数据集元素&#40;ASSL&#41;](cube-element-assl.md)|定义正则、 虚拟的或链接的多维数据集在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)][数据库](database-element-assl.md)元素。|  
|[CubePermission 元素&#40;ASSL&#41;](cubepermission-element-assl.md)|定义的特定成员的权限[角色](role-element-assl.md)中特定元素[多维数据集](cube-element-assl.md)元素。|  
|[CustomRollupColumn 元素&#40;ASSL&#41;](customrollupcolumn-element-assl.md)|定义提供自定义汇总公式的列的详细信息。|  
|[CustomRollupPropertiesColumn 元素&#40;ASSL&#41;](customrolluppropertiescolumn-element-assl.md)|定义用于提供自定义汇总公式属性的列的详细信息。|  
|[数据元素&#40;ASSL&#41;](data-element-assl.md)|包含 (中的子集合`Block`元素) 的二进制内容组成[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[数据库元素&#40;ASSL&#41;](database-element-assl.md)|定义 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库。|  
|[DatabasePermission 元素&#40;ASSL&#41;](databasepermission-element-assl.md)|定义中的默认权限[数据库](database-element-assl.md)的特定元素[角色](role-element-assl.md)元素。|  
|[数据源元素&#40;ASSL&#41;](datasource-element-assl.md)|定义中的数据源[数据库](database-element-assl.md)元素。|  
|[DataSourcePermission 元素&#40;ASSL&#41;](datasourcepermission-element-assl.md)|定义中的默认权限[数据源](../data-type/datasource-data-type-assl.md)特定的数据类型[角色](role-element-assl.md)元素。|  
|[DataSourceView 元素&#40;ASSL&#41;](datasourceview-element-assl.md)|定义数据源视图使用[数据库](database-element-assl.md)元素。|  
|[维度元素&#40;ASSL&#41;](dimension-element-assl.md)|定义维度。|  
|[DimensionPermission 元素&#40;ASSL&#41;](dimensionpermission-element-assl.md)|定义属于特定的权限[角色](role-element-assl.md)特定数据库维度或多维数据集维度元素。|  
|[ErrorConfiguration 元素&#40;ASSL&#41;](errorconfiguration-element-assl.md)|指定在处理父元素时可能出现的错误的处理设置。|  
|[Event 元素&#40;ASSL&#41;](event-element-assl.md)|定义一个事件，它作为的一部分捕获[跟踪](trace-element-assl.md)元素。|  
|[文件元素&#40;ASSL&#41;](file-element-assl.md)|定义一个组成的文件[ClrAssembly](../data-type/assembly-data-type-assl.md)元素。|  
|[ForeignKeyColumn 元素&#40;ASSL&#41;](keycolumn-element-assl.md)|标识加入关系数据源的父表的联接。|  
|[组元素&#40;ASSL&#41;](group-element-assl.md)|定义一组绑定到某个属性的成员。|  
|[层次结构元素&#40;ASSL&#41;](hierarchy-element-assl.md)|定义维度中的层次结构。|  
|[IncrementalProcessingNotification 元素&#40;ASSL&#41;](incrementalprocessingnotification-element-assl.md)|包含信息[ProactiveCaching](proactivecaching-element-assl.md)有关要执行以确定的进度增量处理的查询的元素。|  
|[KeyColumn 元素&#40;ASSL&#41;](keycolumn-element-assl.md)|包含某个列的定义，该列用作属性键或属性键的一部分。|  
|[Kpi 元素&#40;ASSL&#41;](kpi-element-assl.md)|在定义关键绩效指标 (KPI)[多维数据集](cube-element-assl.md)元素或[透视](perspective-element-assl.md)元素。|  
|[级别元素&#40;ASSL&#41;](level-element-assl.md)|定义中的级别[层次结构](hierarchy-element-assl.md)元素。|  
|[MdxScript 元素&#40;ASSL&#41;](mdxscript-element-assl.md)|包含与关联的多维表达式 (MDX) 脚本信息[多维数据集](cube-element-assl.md)元素。|  
|[测量元素&#40;ASSL&#41;](measure-element-assl.md)|定义一个度量值。|  
|[MeasureGroup 元素&#40;ASSL&#41;](measuregroup-element-assl.md)|定义一组属于同一粒度级别的度量值。|  
|[成员元素&#40;ASSL&#41;](member-element-assl.md)|包含的一个成员的名称[组](group-element-assl.md)元素或[角色](role-element-assl.md)元素。|  
|[MiningModel 元素&#40;ASSL&#41;](miningmodel-element-assl.md)|定义一个数据挖掘模型。|  
|[MiningModelPermission 元素&#40;ASSL&#41;](miningmodelpermission-element-assl.md)|定义的权限成员[角色](role-element-assl.md)元素具有对单个[MiningModel](miningmodel-element-assl.md)元素。|  
|[MiningStructure 元素&#40;ASSL&#41;](miningstructure-element-assl.md)|定义一组挖掘模型的结构。|  
|[MiningStructurePermission 元素&#40;ASSL&#41;](miningstructurepermission-element-assl.md)|定义的权限的成员[角色](role-element-assl.md)元素具有对单个[MiningStructure](miningstructure-element-assl.md)元素。|  
|[ModelingFlag 元素&#40;ASSL&#41;](modelingflag-element-assl.md)|包含挖掘结构或挖掘模型中的某个列的建模标志。|  
|[NameColumn 元素&#40;ASSL&#41;](namecolumn-element-assl.md)|标识提供父元素名称的列。|  
|[NamingTemplateTranslation 元素&#40;ASSL&#41;](namingtemplatetranslation-element-assl.md)|提供的本地化的翻译`NamingTemplate`的父元素[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)数据类型。|  
|[分区元素&#40;ASSL&#41;](partition-element-assl.md)|定义的分区[MeasureGroup](measuregroup-element-assl.md)元素或扩展的行中的分区绑定[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)元素。|  
|[透视元素&#40;ASSL&#41;](perspective-element-assl.md)|定义的透视的详细信息[多维数据集](cube-element-assl.md)元素。|  
|[ProactiveCaching 元素&#40;ASSL&#41;](proactivecaching-element-assl.md)|定义父元素的主动缓存设置。|  
|[QueryNotification 元素&#40;ASSL&#41;](querynotification-element-assl.md)|包含信息[ProactiveCaching](proactivecaching-element-assl.md)有关要执行来确定是否已修改数据源的查询的元素。|  
|[ReportFormatParameter 元素&#40;ASSL&#41;](reportformatparameter-element-asl.md)|包含的名称和值的一个参数，指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]报表格式在运行时。|  
|[ReportParameter 元素&#40;ASSL&#41;](reportparameter-element-assl.md)|包含在运行时传递给 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表的参数的名称和值。|  
|[Role 元素&#40;ASSL&#41;](role-element-assl.md)|包含有关安全角色的信息。|  
|[服务器元素&#40;ASSL&#41;](server-element-assl.md)|描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。|  
|[ServerProperty 元素&#40;ASSL&#41;](serverproperty-element-assl.md)|定义与关联的服务器属性[服务器](server-element-assl.md)元素。|  
|[SkippedLevelsColumn 元素&#40;ASSL&#41;](skippedlevelscolumn-element-assl.md)|提供列的详细信息，该列存储每个成员及其父级之间跳过的（空的）级别数。|  
|[SourceMeasureGroup 元素&#40;ASSL&#41;](sourcemeasuregroup-element-assl.md)|标识用作挖掘结构列的数据源的度量值组。|  
|[TableNotification 元素&#40;ASSL&#41;](tablenotification-element-assl.md)|包含信息[ProactiveCaching](proactivecaching-element-assl.md)有关的表或视图已修改的数据源中的元素。|  
|[跟踪元素&#40;ASSL&#41;](trace-element-assl.md)|定义可查询的跟踪。|  
|[转换元素&#40;ASSL&#41;](translation-element-assl.md)|提供的本地化的翻译的父级[翻译](../collections/translations-element-assl.md)集合。|  
|[UnaryOperatorColumn 元素&#40;ASSL&#41;](unaryoperatorcolumn-element-assl.md)|定义提供一元运算符的列的详细信息。|  
|[UnknownMemberTranslation 元素&#40;ASSL&#41;](unknownmembertranslation-element-assl.md)|包含的转换是为标题[UnknownMember](../properties/unknownmember-element-assl.md)元素[维度](dimension-element-assl.md)元素。|  
|[ValueColumn 元素&#40;ASSL&#41;](valuecolumn-element-assl.md)|标识提供父元素值的列。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  