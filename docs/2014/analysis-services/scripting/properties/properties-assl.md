---
title: 属性 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- properties [Analysis Services Scripting Language]
- Analysis Services Scripting Language, properties
- ASSL, properties
ms.assetid: 9a38cdc9-a210-421a-90e9-6391876765fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6371a751cdd5a4d647b781373ab74629103e0c44
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061397"
---
# <a name="properties-assl"></a>属性 (ASSL)
  本参考部分包含作为 Analysis Services 脚本语言 (ASSL) 架构中的对象属性的所有元素的语法和用法信息。  
  
 尽管 ASSL 架构只包含 XML 元素，但是从开发人员的角度来说，本节中介绍的元素是与介绍对象的属性对应的。  
  
 在 ASSL 架构中，属性为叶级元素，且不包含子元素或与其拥有的属性相对应的元素。  
  
 在少数情况下，架构中显示为属性的叶级元素可归类为对象，这是因为该元素的类型是对象类型。 例如，`Source` 对象的 `Dimension` 为 `DimensionBinding` 类型。  
  
## <a name="in-this-section"></a>本节内容  
  
|元素|Description|  
|-------------|-----------------|  
|[访问元素&#40;ASSL&#41;](access-element-assl.md)|指示到提供的访问级别[CellPermission](../objects/cellpermission-element-assl.md)元素。|  
|[帐户元素&#40;ImpersonationInfo&#41; &#40;ASSL&#41;](account-element-impersonationinfo-assl.md)|包含用户帐户的名称[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)数据类型。|  
|[AccountType 元素&#40;ASSL&#41;](accounttype-element-assl.md)|包含在中定义的帐户类型的名称[数据库](../objects/database-element-assl.md)元素。|  
|[ActionID 元素&#40;ASSL&#41;](id-element-assl.md)|包含名称的[操作](../objects/action-element-assl.md)元素中定义[多维数据集](../objects/cube-element-assl.md)中可用的元素[角度来看](../objects/perspective-element-assl.md)元素作为[PerspectiveAction](../data-type/action-data-type-assl.md)元素。|  
|[Administer 元素&#40;ASSL&#41;](administer-element-assl.md)|指示关联权限是否包括管理 `Database` 元素的权利。|  
|[AggregateFunction 元素&#40;ASSL&#41;](aggregatefunction-element-assl.md)|定义使用的聚合函数的类型[度量值](../objects/measure-element-assl.md)元素。|  
|[AggregationDesignID 元素&#40;ASSL&#41;](aggregationdesignid-element-assl.md)|标识[AggregationDesign](../objects/aggregationdesign-element-assl.md)元素与关联[分区](../objects/partition-element-assl.md)元素。|  
|[AggregationFunction 元素&#40;ASSL&#41;](aggregationfunction-element-assl.md)|包含要用于帐户类型的聚合函数。|  
|[AggregationID 元素&#40;ASSL&#41;](aggregationid-element-assl.md)|标识来自用于创建聚合实例的 `AggregationDesign` 元素的聚合定义。|  
|[AggregationInstanceSource 元素&#40;ASSL&#41;](aggregationinstancesource-element-assl.md)|标识绑定到 `Partition` 元素的、用户定义的聚合实例的数据源。|  
|[AggregationPrefix 元素&#40;ASSL&#41;](aggregationprefix-element-assl.md)|定义整个关联父元素中聚合名称所用的通用前缀。|  
|[AggregationStorage 元素&#40;ASSL&#41;](aggregationstorage-element-assl.md)|标识聚合的存储方法。|  
|[AggregationType 元素&#40;ASSL&#41;](aggregationtype-element-assl.md)|定义 `Partition` 元素存储的聚合类型。|  
|[AggregationUsage 元素&#40;ASSL&#41;](aggregationusage-element-assl.md)|控件如何聚合设计器中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]设计聚合。|  
|[Algorithm 元素&#40;ASSL&#41;](algorithm-element-assl.md)|定义使用的算法[MiningModel](../objects/miningmodel-element-assl.md)元素。|  
|[Alias 元素&#40;ASSL&#41;](alias-element-assl.md)|定义的别名[帐户](../objects/account-element-assl.md)元素。|  
|[AllMemberAggregationUsage 元素&#40;ASSL&#41;](allmemberaggregationusage-element-assl.md)|控制 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的聚合设计器如何设计聚合。|  
|[AllMemberName 元素&#40;ASSL&#41;](name-element-assl.md)|包含所有成员的默认语言的标题[层次结构](../objects/hierarchy-element-assl.md)元素。|  
|[AllowBrowsing 元素&#40;ASSL&#41;](allowbrowsing-element-assl.md)|定义是否的成员[角色](../objects/role-element-assl.md)元素有浏览权限`MiningModel`元素。|  
|[AllowDrillThrough 元素&#40;ASSL&#41;](allowdrillthrough-element-assl.md)|确定是否允许在父元素上执行钻取操作。|  
|[AllowDuplicateNames 元素&#40;ASSL&#41;](allowduplicatenames-element-assl.md)|确定 `Hierarchy` 元素中是否允许重复的名称。|  
|[AllowedSet 元素&#40;ASSL&#41;](allowedset-element-assl.md)|包含一个集表达式，该表达式定义 `Role` 元素对某属性的允许权限集。|  
|[应用程序元素&#40;ASSL&#41;](application-element-assl.md)|标识与 `Action` 元素关联的应用程序。|  
|[AssociatedMeasureGroupID 元素&#40;ASSL&#41;](measuregroupid-element-assl.md)|包含的标识符 (ID) [MeasureGroup](../objects/group-element-assl.md)元素与关联[CalculationProperty](../objects/calculationproperty-element-assl.md)元素或[Kpi](../objects/kpi-element-assl.md)元素。|  
|[AttributeAllMemberName 元素&#40;ASSL&#41;](attributeallmembername-element-assl.md)|包含以默认语言显示的维度的“全部”成员的标题。|  
|[AttributeHierarchyDisplayFolder 元素&#40;ASSL&#41;](displayfolder-element-assl.md)|指定在其中显示关联的属性层次结构的文件夹。|  
|[AttributeHierarchyEnabled 元素&#40;ASSL&#41;](enabled-element-assl.md)|确定是否为属性启用属性层次结构。|  
|[AttributeHierarchyOptimizedState 元素&#40;ASSL&#41;](state-element-assl.md)|确定应用于属性层次结构的优化级别。|  
|[AttributeHierarchyOrdered 元素&#40;ASSL&#41;](attributehierarchyordered-element-assl.md)|确定关联的属性层次结构是否已排序。|  
|[AttributeHierarchyVisible 元素&#40;ASSL&#41;](visible-element-assl.md)|确定属性层次结构是否对客户端应用程序可见。|  
|[AttributeID 元素&#40;ASSL&#41;](attributeid-element-assl.md)|包含与父元素关联的属性的 ID。|  
|[Audit 元素&#40;ASSL&#41;](audit-element-assl.md)|指定的[跟踪](../objects/trace-element-assl.md)元素不能删除任何事件，即使这会导致服务器的性能下降。|  
|[AutoRestart 元素&#40;ASSL&#41;](autorestart-element-assl.md)|确定当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务停止并重新启动时，`Trace` 元素是否应自动重新启动。|  
|[BackColor 元素&#40;ASSL&#41;](backcolor-element-assl.md)|描述父元素的颜色相关显示特征。|  
|[CacheMode 元素&#40;ASSL&#41;](cachemode-element-assl.md)|确定用于定型在处理挖掘结构时检索的数据的缓存机制。|  
|[CalculationReference 元素&#40;ASSL&#41;](calculationreference-element-assl.md)|包含 `CalculationProperty` 元素引用的命名集或计算单元的名称。|  
|[CalculationType 元素&#40;ASSL&#41;](calculationtype-element-assl.md)|描述关联的 `CalculationProperty` 元素中定义的计算类型。|  
|[CalendarEndDate 元素&#40;ASSL&#41;](calendarenddate-element-assl.md)|定义的日历周期的结束日期[TimeBinding](../data-type/binding-data-type-assl.md)元素。|  
|[CalendarLanguage 元素&#40;ASSL&#41;](language-element-assl.md)|定义用于 `TimeBinding` 元素的日历语言。|  
|[CalendarStartDate 元素&#40;ASSL&#41;](calendarstartdate-element-assl.md)|定义 `TimeBinding` 元素的日历周期的开始日期。|  
|[标题元素&#40;ASSL&#41;](caption-element-assl.md)|包含关联父元素的标题。|  
|[CaptionIsMdx 元素&#40;ASSL&#41;](captionismdx-element-assl.md)|定义 `Action` 元素的标题是否为多维表达式 (MDX) 表达式。|  
|[Cardinality 元素&#40;ASSL&#41;](cardinality-element-assl.md)|指示描述的关系的基数[AttributeRelationship](../objects/attributerelationship-element-assl.md)或[RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)。|  
|[CaseCubeDimensionID 元素&#40;ASSL&#41;](dimensionid-element-assl.md)|包含关联数据挖掘维度与度量值组的多维数据集维度的 ID。|  
|[ClassifiedColumnID 元素&#40;ASSL&#41;](classifiedcolumnid-element-assl.md)|包含按分类的相关列的 ID [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)元素。|  
|[排序规则元素&#40;ASSL&#41;](collation-element-assl.md)|确定父元素使用的排序规则。|  
|[ColumnID 元素&#40;ColumnBinding&#41; &#40;ASSL&#41;](columnid-element-columnbinding-assl.md)|包含数据项所绑定到的表中的列的 ID。|  
|[ColumnID 元素&#40;EventColumn&#41; &#40;ASSL&#41;](columnid-element-eventcolumn-assl.md)|包含将会作为 `Trace` 元素一部分而被事件捕获的信息列的 ID。|  
|[条件元素&#40;ASSL&#41;](condition-element-assl.md)|包含用于确定是否将 `Action` 父元素应用于目标的 MDX 表达式。|  
|[ConnectionString 元素&#40;ASSL&#41;](connectionstring-element-assl.md)|包含的加密的连接字符串[数据源](../objects/datasource-element-assl.md)元素。|  
|[ConnectionStringSecurity 元素&#40;ASSL&#41;](connectionstringsecurity-element-assl.md)|指定是否出于安全目的从数据源连接字符串中抽取用户的密码。|  
|[内容元素&#40;ASSL&#41;](content-element-assl.md)|描述中的列的内容[MiningStructure](../objects/miningstructure-element-assl.md)元素。|  
|[CreatedTimestamp 元素&#40;ASSL&#41;](createdtimestamp-element-assl.md)|包含父元素的只读创建时间戳。|  
|[CubeDimensionID 元素&#40;ASSL&#41;](cubedimensionid-element-assl.md)|标识[CubeDimension](../data-type/cubedimension-data-type-assl.md)元素与父元素相关联。|  
|[CubeID 元素&#40;ASSL&#41;](cubeid-element-assl.md)|标识`Cube`元素与关联[绑定](../data-type/binding-data-type-assl.md)元素。|  
|[CurrentStorageMode 元素&#40;ASSL&#41;](storagemode-element-assl.md)|确定父元素的当前存储模式。|  
|[CurrentTimeMember 元素&#40;ASSL&#41;](../objects/member-element-assl.md)|定义与 `Kpi` 元素关联的时间维度的当前成员。|  
|[DataAggregation 元素&#40;ASSL&#41;](../objects/aggregation-element-assl.md)|确定实例是否可为 `MeasureGroup` 聚合持久化数据或缓存数据。|  
|[DatabaseID 元素&#40;ASSL&#41;](databaseid-element-assl.md)|标识与外部 `Database` 元素关联的 `Binding` 元素。|  
|[DataSize 元素&#40;ASSL&#41;](datasize-element-assl.md)|包含以字节为单位的大小[DataItem](../data-type/dataitem-data-type-assl.md)元素。|  
|[DataSourceID 元素&#40;ASSL&#41;](datasourceid-element-assl.md)|标识与父元素关联的 `DataSource` 元素。|  
|[DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)|包含用于确定连接到 `Database` 元素的数据源时的模拟行为相关信息。|  
|[DataSourceViewID 元素&#40;ASSL&#41;](datasourceviewid-element-assl.md)|标识[DataSourceView](../objects/datasourceview-element-assl.md)元素与关联`Binding`父元素。|  
|[DataType 元素&#40;ASSL&#41;](datatype-element-assl.md)|定义关联元素的数据类型。|  
|[DbSchemaName 元素&#40;ASSL&#41;](dbschemaname-element-assl.md)|包含父元素中标识的表使用的架构的名称[DbTableName](dbtablename-element-assl.md)元素。|  
|[DbTableName 元素&#40;ASSL&#41;](dbtablename-element-assl.md)|包含父元素绑定到的表的名称。|  
|[默认元素&#40;ASSL&#41;](default-element-assl.md)|确定 `DrillThroughAction` 是否为默认钻取操作。|  
|[DefaultMeasure 元素&#40;ASSL&#41;](defaultmeasure-element-assl.md)|包含用于定义 `Cube` 或 `Perspective` 元素的默认度量值的 MDX 语言表达式。|  
|[DefaultMember 元素&#40;ASSL&#41;](defaultmember-element-assl.md)|包含标识父元素的默认成员的 MDX 表达式。|  
|[DefaultScript 元素&#40;ASSL&#41;](defaultscript-element-assl.md)|标识默认[MdxScript](../objects/mdxscript-element-assl.md)中的元素[MdxScripts](../collections/mdxscripts-element-assl.md)集合。|  
|[DefaultValue 元素&#40;ASSL&#41;](value-element-assl.md)|包含关联的只读默认值[ServerProperty](../objects/serverproperty-element-assl.md)元素。|  
|[DeniedSet 元素&#40;ASSL&#41;](deniedset-element-assl.md)|包含一个集表达式，该表达式定义关联属性所拒绝的权限的列表。|  
|[DependsOnDimensionID 元素&#40;ASSL&#41;](dependsondimensionid-element-assl.md)|包含父维度所依赖的其他维度的 ID。|  
|[Description 元素&#40;ASSL&#41;](description-element-assl.md)|包含父元素的说明。|  
|[DimensionID 元素&#40;ASSL&#41;](dimensionid-element-assl.md)|包含维度的 ID。|  
|[DiscretizationBucketCount 元素&#40;ASSL&#41;](discretizationbucketcount-element-assl.md)|包含以其进行离散化的存储桶数。|  
|[DiscretizationMethod 元素&#40;ASSL&#41;](discretizationmethod-element-assl.md)|定义用于离散化的方法。|  
|[DisplayFlag 元素&#40;ASSL&#41;](displayflag-element-assl.md)|包含一个只读提示，指示用户界面组件是否应显示关联的 `ServerProperty` 元素。|  
|[DisplayFolder 元素&#40;ASSL&#41;](displayfolder-element-assl.md)|指定要在其中列出父元素的文件夹。 对于开发人员和管理员来说，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 应用程序可能支持使用显示文件夹，从而直观地对多个元素进行分类。|  
|[Distribution 元素&#40;ASSL&#41;](distribution-element-assl.md)|包含特定于提供程序的值，该值介绍标量值在 `MiningStructure` 元素的列内的分布情况。|  
|[Edition 元素&#40;ASSL&#41;](edition-element-assl.md)|包含的实例的只读版本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由此[Server](../objects/server-element-assl.md)元素。|  
|[启用元素&#40;ASSL&#41;](enabled-element-assl.md)|指示是否启用了父元素。|  
|[EndOfData 元素&#40;ASSL&#41;](../objects/data-element-assl.md)|指示从接收的数据的结尾[PushedDataSource](../data-type/datasource-data-type-assl.md)元素。|  
|[EstimatedCount 元素&#40;ASSL&#41;](estimatedcount-element-assl.md)|包含属性的估计的成员数。|  
|[EstimatedPerformanceGain 元素&#40;ASSL&#41;](estimatedperformancegain-element-assl.md)|包含估计的分区性能提升的只读百分比。|  
|[EstimatedRows 元素&#40;ASSL&#41;](estimatedrows-element-assl.md)|包含由父元素表示的估计行数。|  
|[EstimatedSize 元素&#40;ASSL&#41;](estimatedsize-element-assl.md)|包含父元素的只读估计大小（以字节为单位）。|  
|[EventID 元素&#40;ASSL&#41;](eventid-element-assl.md)|唯一标识[事件](../objects/event-element-assl.md)是作为的一部分捕获的元素`Trace`元素。|  
|[Expression 元素&#40;ASSL&#41;](expression-element-assl.md)|包含定义父元素内容的 MDX 表达式。|  
|[Filter 元素&#40;绑定&#41; &#40;ASSL&#41;](filter-element-binding-assl.md)|包含筛选父元素内容的 MDX 表达式。|  
|[Filter 元素&#40;跟踪&#41; &#40;ASSL&#41;](filter-element-trace-assl.md)|包含介绍 `Trace` 筛选器的 XML 文档片断。|  
|[FirstDayOfWeek 元素&#40;ASSL&#41;](firstdayofweek-element-assl.md)|为 `TimeBinding` 元素定义周的第一天。|  
|[FiscalFirstDayOfMonth 元素&#40;ASSL&#41;](fiscalfirstdayofmonth-element-assl.md)|为 `TimeBinding` 元素定义会计月的第一天。|  
|[FiscalFirstMonth 元素&#40;ASSL&#41;](fiscalfirstmonth-element-assl.md)|为 `TimeBinding` 元素定义会计周期的第一个月。|  
|[FiscalYearName 元素&#40;ASSL&#41;](fiscalyearname-element-assl.md)|定义 `TimeBinding` 元素的会计年度名称的命名约定。|  
|[FontFlags 元素&#40;ASSL&#41;](fontflags-element-assl.md)|介绍 `CalculationProperty` 或 `Measure` 父元素的字体相关显示特征。|  
|[FontName 元素&#40;ASSL&#41;](fontname-element-assl.md)|介绍 `CalculationProperty` 或 `Measure` 父元素的字体相关显示特征。|  
|[FontSize 元素&#40;ASSL&#41;](fontsize-element-assl.md)|介绍 `CalculationProperty` 或 `Measure` 父元素的字体相关显示特征。|  
|[ForceRebuildInterval 元素&#40;ASSL&#41;](forcerebuildinterval-element-assl.md)|确定在多维 OLAP (MOLAP) 映像可用后经过多长时间才能无条件开始 MOLAP 映像处理。|  
|[ForeColor 元素&#40;ASSL&#41;](forecolor-element-assl.md)|介绍 `CalculationProperty` 或 `Measure` 父元素的颜色相关显示特征。|  
|[设置元素的格式&#40;ASSL&#41;](format-element-assl.md)|包含 `DataItem` 元素的所需格式。|  
|[FormatString 元素&#40;ASSL&#41;](formatstring-element-assl.md)|介绍 `CalculationProperty` 元素或 `Measure` 元素的显示格式。|  
|[Goal 元素&#40;ASSL&#41;](goal-element-assl.md)|标识 `Kpi` 元素中的所需目标。|  
|[GranularityAttributeID 元素&#40;ASSL&#41;](granularityattributeid-element-assl.md)|包含与父项关联的属性的 ID [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)数据类型。|  
|[HideMemberIf 元素&#40;ASSL&#41;](hidememberif-element-assl.md)|指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。|  
|[HierarchyID 元素&#40;ASSL&#41;](hierarchyid-element-assl.md)|包含的 ID [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../data-type/perspectivehierarchy-data-type-assl.md)元素。|  
|[HierarchyUniqueNameStyle 元素&#40;ASSL&#41;](hierarchyuniquenamestyle-element-assl.md)|确定如何为包含在 `CubeDimension` 中的层次结构生成唯一名称。|  
|[ID 元素&#40;ASSL&#41;](id-element-assl.md)|包含父元素的唯一 ID。|  
|[IgnoreUnrelatedDimensions 元素&#40;ASSL&#41;](../collections/dimensions-element-assl.md)|确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。|  
|[ImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)|包含用于确定访问或执行程序集时的模拟行为的信息。|  
|[ImpersonationInfoSecurity 元素&#40;ASSL&#41;](impersonationinfosecurity-element-assl.md)|包含一个只读值，该值指示是否对 `ImpersonationInfo` 数据类型中提供的安全凭据进行了更改。|  
|[ImpersonationMode 元素&#40;ASSL&#41;](impersonationmode-element-assl.md)|包含一个值，该值指示从 `ImpersonationInfo` 数据类型派生的元素的模拟方法。|  
|[InstanceSelection 元素&#40;ASSL&#41;](instanceselection-element-assl.md)|提供了应显示提示客户端应用程序建议如何的项的列表，根据预期的列表中的项目数。|  
|[IntermediateCubeDimensionID 元素&#40;ASSL&#41;](intermediatecubedimensionid-element-assl.md)|包含关联引用维度与度量值组的维度的 ID。|  
|[IntermediateGranularityAttributeID 元素&#40;ASSL&#41;](intermediategranularityattributeid-element-assl.md)|包含中间多维数据集维度中的粒度属性的 ID，该 ID 用于关联引用维度和中间维度。|  
|[InvalidXmlCharacters 元素&#40;ASSL&#41;](invalidxmlcharacters-element-assl.md)|指定源数据中无效 XML 字符的处理方法。|  
|[Invocation 元素&#40;ASSL&#41;](invocation-element-assl.md)|指定应如何调用 `Action`。|  
|[IsAggregatable 元素&#40;ASSL&#41;](isaggregatable-element-assl.md)|指定是否的值[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)元素可进行聚合。|  
|[IsKey 元素&#40;ASSL&#41;](iskey-element-assl.md)|指示列是否为 `MiningStructure` 元素中的事例提供键。|  
|[Isolation 元素&#40;ASSL&#41;](isolation-element-assl.md)|指示派生自的元素的隔离级别[数据源](../data-type/datasource-data-type-assl.md)数据类型。|  
|[KeyDuplicate 元素&#40;ASSL&#41;](keyduplicate-element-assl.md)|确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何处理处理期间遇到的重复键错误。|  
|[KeyErrorAction 元素&#40;ASSL&#41;](keyerroraction-element-assl.md)|指定键发生错误时 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的操作。|  
|[KeyErrorLimit 元素&#40;ASSL&#41;](keyerrorlimit-element-assl.md)|包含处理期间可接受的错误数。|  
|[KeyErrorLimitAction 元素&#40;ASSL&#41;](keyerrorlimitaction-element-assl.md)|指定的操作的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定的键错误数时， [KeyErrorLimit](keyerrorlimit-element-assl.md)到达元素。|  
|[KeyErrorLogFile 元素&#40;ASSL&#41;](../objects/file-element-assl.md)|包含记录处理错误的文件名。|  
|[KeyNotFound 元素&#40;ASSL&#41;](keynotfound-element-assl.md)|指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遇到引用完整性错误时如何响应。|  
|[KeyUniquenessGuarantee 元素&#40;ASSL&#41;](keyuniquenessguarantee-element-assl.md)|指示属性键和其名称之间的关系以及属性键和相关属性之间的关系是否保证有效。|  
|[KpiID 元素&#40;ASSL&#41;](kpiid-element-assl.md)|包含关联 `Kpi` 元素与 `Perspective` 元素的 ID。|  
|[语言元素&#40;ASSL&#41;](language-element-assl.md)|包含父元素的语言标识符。|  
|[LastProcessed 元素&#40;ASSL&#41;](lastprocessed-element-assl.md)|包含只读时间戳，该时间戳指示上次处理包含父元素的数据库的时间。|  
|[LastSchemaUpdate 元素&#40;ASSL&#41;](lastschemaupdate-element-assl.md)|包含父元素的只读元数据更新时间戳。|  
|[LastUpdate 元素&#40;ASSL&#41;](lastupdate-element-assl.md)|包含一个只读时间戳，指示关联 `Database` 或该数据库包含的任何主要对象的最后更改时间。|  
|[Latency 元素&#40;ASSL&#41;](latency-element-assl.md)|定义最早通知与 MOLAP 图像被破坏时刻之间的“宽限期”。|  
|[LogFileAppend 元素&#40;ASSL&#41;](logfileappend-element-assl.md)|确定 `Trace` 元素是将其日志记录输出附加到现有日志文件，还是覆盖该文件。|  
|[LogFileName 元素&#40;ASSL&#41;](logfilename-element-assl.md)|包含用于 `Trace` 元素的日志文件的文件名。|  
|[LogFileRollover 元素&#40;ASSL&#41;](logfilerollover-element-assl.md)|指定的日志记录`Trace`输出应转到新文件，还是应停止时的最大日志文件大小时，它是指定在[LogFileSize](logfilesize-element-assl.md)为止。|  
|[LogFileSize 元素&#40;ASSL&#41;](logfilesize-element-assl.md)|指定最大日志文件大小 (MB)。|  
|[ManagedProvider 元素&#40;ASSL&#41;](managedprovider-element-assl.md)|包含从 `DataSource` 数据类型派生的元素所使用的托管访问接口名称。|  
|[ManufacturingExtraMonthQuarter 元素&#40;ASSL&#41;](manufacturingextramonthquarter-element-assl.md)|定义生产周期的月份，在 `TimeBinding` 元素中向生产周期额外分配一个月。|  
|[ManufacturingFirstMonth 元素&#40;ASSL&#41;](manufacturingfirstmonth-element-assl.md)|定义 `TimeBinding` 元素的第一个生产月。|  
|[ManufacturingFirstWeekOfMonth 元素&#40;ASSL&#41;](manufacturingfirstweekofmonth-element-assl.md)|为 `TimeBinding` 元素定义生产月的第一周。|  
|[MasterDatasourceID 元素&#40;ASSL&#41;](masterdatasourceid-element-assl.md)|包含 `Database` 元素的主数据源 ID。|  
|[Materialization 元素&#40;ASSL&#41;](materialization-element-assl.md)|指示度量值组和引用维度之间的关系类型。|  
|[MaxActiveConnections 元素&#40;ASSL&#41;](maxactiveconnections-element-assl.md)|包含派生自 `DataSource` 数据类型的元素允许的最大并发连接数。|  
|[MdxMissingMemberMode 元素&#40;ASSL&#41;](mdxmissingmembermode-element-assl.md)|确定如何处理 MDX 语句中缺少的成员。|  
|[MeasureExpression 元素&#40;ASSL&#41;](measureexpression-element-assl.md)|包含定义度量值的 MDX 表达式。|  
|[MeasureGroupID 元素&#40;ASSL&#41;](measuregroupid-element-assl.md)|将 `MeasureGroup` 与父元素、绑定或外部绑定关联。|  
|[MeasureID 元素&#40;ASSL&#41;](measureid-element-assl.md)|将 `Measure` 元素与父元素相关联。|  
|[MeasureQualificaton 元素&#40;ASSL&#41;](measurequalificaton-element-assl.md)|确定前缀是否应用于 `MeasureGroup` 中的度量值。|  
|[MemberNamesUnique 元素&#40;ASSL&#41;](membernamesunique-element-assl.md)|确定父元素的成员名称是否必须是唯一的。|  
|[MemberUniqueNameStyle 元素&#40;ASSL&#41;](memberuniquenamestyle-element-assl.md)|确定如何为包含在 `CubeDimension` 元素中的层次结构成员生成唯一名称。|  
|[MembersWithData 元素&#40;ASSL&#41;](memberswithdata-element-assl.md)|确定是否显示父属性中非叶成员的数据成员。|  
|[MembersWithDataCaption 元素&#40;ASSL&#41;](memberswithdatacaption-element-assl.md)|提供用于为系统生成的数据成员创建标题的模板字符串。|  
|[MimeType 元素&#40;ASSL&#41;](mimetype-element-assl.md)|包含父 `DataItem` 元素表示的数据的多用途 Internet 邮件扩展 (MIME) 类型（如果适用）。|  
|[MiningModelID 元素&#40;ASSL&#41;](miningmodelid-element-assl.md)|将挖掘模型与数据挖掘维度关联。|  
|[命名元素&#40;ASSL&#41;](name-element-assl.md)|包含父元素的名称。|  
|[NamingTemplate 元素&#40;ASSL&#41;](namingtemplate-element-assl.md)|定义如何在基于 `DimensionAttribute` 父元素构造的父子层次结构中命名级别。|  
|[NonEmptyBehavior 元素&#40;ASSL&#41;](nonemptybehavior-element-assl.md)|确定与 `CalculationProperty` 元素的父级关联的非空行为。|  
|[NotificationTechnique 元素&#40;ASSL&#41;](notificationtechnique-element-assl.md)|指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部客户端应用程序处理通知。|  
|[NullKeyConvertedToUnknown 元素&#40;ASSL&#41;](nullkeyconvertedtounknown-element-assl.md)|指定遇到空转换错误时要执行的操作。|  
|[NullKeyNotAllowed 元素&#40;ASSL&#41;](nullkeynotallowed-element-assl.md)|确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 处理引擎如何处理在处理过程中遇到空键错误。|  
|[NullProcessing 元素&#40;ASSL&#41;](nullprocessing-element-assl.md)|定义如何处理空值。|  
|[OnlineMode 元素&#40;ASSL&#41;](onlinemode-element-assl.md)|指定是在重新生成缓存刚一开始就立即使数据库恢复到联机状态，还是在完成重新生成缓存后才使数据库恢复到联机状态。|  
|[OptimizedState 元素&#40;ASSL&#41;](state-element-assl.md)|确定应用于层次结构的优化级别。|  
|[Optionality 元素&#40;ASSL&#41;](optionality-element-assl.md)|指示 `AttributeRelationship` 元素的成员的可选性。|  
|[OrderBy 元素&#40;ASSL&#41;](orderby-element-assl.md)|说明如何对属性中包含的成员进行排序。|  
|[OrderByAttributeID 元素&#40;ASSL&#41;](orderbyattributeid-element-assl.md)|标识另一个属性的成员进行排序[维度](../data-type/dimensionattribute-data-type-assl.md)属性。|  
|[Ordinal 元素&#40;ASSL&#41;](ordinal-element-assl.md)|指示要绑定到集合（如键和翻译）中的序号。|  
|[OverrideBehavior 元素&#40;ASSL&#41;](overridebehavior-element-assl.md)|指示 `AttributeRelationship` 元素描述的关系的覆盖行为。|  
|[PartitionID 元素&#40;ASSL&#41;](partitionid-element-assl.md)|将 `Partition` 元素与父元素、绑定或外部绑定关联。|  
|[Password 元素&#40;ASSL&#41;](password-element-assl.md)|包含 `ImpersonationInfo` 元素的用户帐户的密码。|  
|[Path 元素&#40;ASSL&#41;](path-element-assl.md)|包含路径，则由的实例提供[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，通过使用的报告[ReportAction](../data-type/reportaction-data-type-assl.md)元素。|  
|[PendingValue 元素&#40;ASSL&#41;](pendingvalue-element-assl.md)|包含关联的 `ServerProperty` 元素的只读挂起值。|  
|[PermissionSet 元素&#40;ASSL&#41;](permissionset-element-assl.md)|标识与关联的权限集[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 程序集。|  
|[Persistence 元素&#40;ASSL&#41;](persistence-element-assl.md)|确定绑定的源数据的哪些部分是动态的使用指定的频率更新检查[RefreshPolicy](refreshpolicy-element-assl.md)元素。|  
|[处理元素&#40;ASSL&#41;](process-element-assl.md)|确定用户是否可以处理父元素的所有者。|  
|[ProcessingMode 元素&#40;ASSL&#41;](processingmode-element-assl.md)|指示该实例应该在处理期间还是处理后进行索引和聚合。|  
|[ProcessingPriority 元素&#40;ASSL&#41;](processingpriority-element-assl.md)|确定在后台操作期间（例如迟缓聚合、索引或群集），父对象的处理优先级。|  
|[ProcessingQuery 元素&#40;ASSL&#41;](query-element-assl.md)|包含要为增量处理状态通知执行的查询的参数化文本。|  
|[ProductName 元素&#40;ASSL&#41;](productname-element-assl.md)|包含与 `Server` 元素关联的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的只读产品名。|  
|[查询元素&#40;ASSL&#41;](query-element-assl.md)|包含要为通知执行的查询的文本。|  
|[QueryDefinition 元素&#40;ASSL&#41;](querydefinition-element-assl.md)|包含关联的查询的不透明表达式`DataSource`中的元素[QueryBinding](../data-type/querybinding-data-type-assl.md)元素。|  
|[读取元素&#40;ASSL&#41;](read-element-assl.md)|确定是否可用于读取数据或元数据给定[CubeDimensionPermission](../data-type/permission-data-type-assl.md)或[权限](../data-type/permission-data-type-assl.md)元素。|  
|[ReadDefinition 元素&#40;ASSL&#41;](readdefinition-element-assl.md)|确定成员是否可以读取数据库的定义或数据库中对象的定义。|  
|[ReadSourceData 元素&#40;ASSL&#41;](readsourcedata-element-assl.md)|确定如何为包含在 `CubePermission` 中的层次结构生成唯一名称。|  
|[RefreshInterval 元素&#40;ASSL&#41;](refreshinterval-element-assl.md)|指定与父元素关联的绑定数据的刷新时间间隔。|  
|[RefreshPolicy 元素&#40;ASSL&#41;](refreshpolicy-element-assl.md)|何种频率确定维度或度量值组的动态部分 (所指定的[持久性](persistence-element-assl.md)元素) 的更改检查。|  
|[RelationshipType 元素&#40;ASSL&#41;](relationshiptype-element-assl.md)|指示 `AttributeRelationship` 的成员关系能否更改。|  
|[RemoteDatasourceID 元素&#40;ASSL&#41;](remotedatasourceid-element-assl.md)|指定 OLAP 数据源的 ID，该数据源指向存储远程分区的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。|  
|[ReportingFirstMonth 元素&#40;ASSL&#41;](reportingfirstmonth-element-assl.md)|定义 `TimeBinding` 元素的第一个报表月。|  
|[ReportingFirstWeekOfMonth 元素&#40;ASSL&#41;](reportingfirstweekofmonth-element-assl.md)|为 `TimeBinding` 元素定义报表月的第一周。|  
|[ReportingWeekToMonthPattern 元素&#40;ASSL&#41;](reportingweektomonthpattern-element-assl.md)|为 `TimeBinding` 元素定义周对月报表模式。|  
|[ReportServer 元素&#40;ASSL&#41;](reportserver-element-assl.md)|包含 `ReportAction` 所使用的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 实例的名称。|  
|[RequiresRestart 元素&#40;ASSL&#41;](requiresrestart-element-assl.md)|包含与 `ServerProperty` 元素关联的只读值，该元素确定是否需要重新启动实例才能使对服务器属性值的更改有效。|  
|[RoleID 元素&#40;ASSL&#41;](roleid-element-assl.md)|标识要为其定义权限的角色。|  
|[根元素&#40;ASSL&#41;](root-element-assl.md)|包含数据源的数据（行集）。|  
|[RootMemberIf 元素&#40;ASSL&#41;](rootmemberif-element-assl.md)|确定如何识别父级属性的根成员或成员。|  
|[架构元素&#40;ASSL&#41;](schema-element-assl.md)|包含数据源视图的架构。|  
|[ScriptCacheProcessingMode 元素&#40;ASSL&#41;](scriptcacheprocessingmode-element-assl.md)|指示服务器在处理期间或处理之后是否生成脚本缓存。|  
|[SilenceInterval 元素&#40;ASSL&#41;](silenceinterval-element-assl.md)|定义在启动 MOLAP 图像处理进程之前，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例暂停的最短时间。|  
|[SilenceOverrideInterval 元素&#40;ASSL&#41;](silenceoverrideinterval-element-assl.md)|定义在接收初始通知之后，必须经过多长时间才能无条件开始 MOLAP 图像处理。|  
|[Slice 元素&#40;ASSL&#41;](slice-element-assl.md)|包含定义分区中的切片的 MDX 表达式。|  
|[SolveOrder 元素&#40;ASSL&#41;](solveorder-element-assl.md)|指示用以将 `CalculationProperty` 元素应用到计算成员或计算单元定义的求解次序。|  
|[Source 元素&#40;绑定&#41; &#40;ASSL&#41;](source-element-binding-assl.md)|标识父元素绑定到的数据源。|  
|[Source 元素&#40;ComAssembly&#41; &#40;ASSL&#41;](source-element-comassembly-assl.md)|包含组件对象模型 (COM) 组件的文件名或编程标识符 (ProgID)。|  
|[Source 元素&#40;度量值&#41; &#40;ASSL&#41;](source-element-measure-assl.md)|提供包含 `Measure` 元素值的源的详细信息。|  
|[SourceAttributeID 元素&#40;ASSL&#41;](sourceattributeid-element-assl.md)|包含在其上的源属性的 ID[级别](../objects/level-element-assl.md)基于元素。|  
|[SourceColumnID 元素&#40;ASSL&#41;](sourcecolumnid-element-assl.md)|包含祖先 `MiningStructure` 元素中的源挖掘结构列的 ID。|  
|[状态元素&#40;ASSL&#41;](state-element-assl.md)|包含一个只读值，它说明父元素的当前处理状态。|  
|[Status 元素&#40;ASSL&#41;](status-element-assl.md)|包含返回 `Kpi` 元素的状态指示器的 MDX 表达式。|  
|[StatusGraphic 元素&#40;ASSL&#41;](statusgraphic-element-assl.md)|包含 `Kpi` 元素状态的建议图形表示形式。|  
|[StopTime 元素&#40;ASSL&#41;](stoptime-element-assl.md)|指定 `Trace` 元素的停止日期和时间。|  
|[StorageLocation 元素&#40;ASSL&#41;](storagelocation-element-assl.md)|包含文件系统中的父元素内容存储位置。|  
|[StorageMode 元素&#40;ASSL&#41;](storagemode-element-assl.md)|确定父元素的存储模式。|  
|[TableID 元素&#40;ASSL&#41;](tableid-element-assl.md)|包含与父元素关联的表（来自 `DataSourceView` 元素）的 ID。|  
|[Target 元素&#40;ASSL&#41;](target-element-assl.md)|标识 `Action` 元素的目标。|  
|[TargetType 元素&#40;ASSL&#41;](targettype-element-assl.md)|标识的标识中的项的项类型[目标](target-element-assl.md)元素。|  
|[文本元素&#40;ASSL&#41;](text-element-assl.md)|包含的文本[命令](../objects/command-element-assl.md)元素。|  
|[Timeout 元素&#40;ASSL&#41;](timeout-element-assl.md)|指定以秒为单位的一段时间，这段时间之后再试图检索数据将报告超时。|  
|[Trend 元素&#40;ASSL&#41;](trend-element-assl.md)|包含返回 `Kpi` 元素的走向指示器的 MDX 表达式。|  
|[TrendGraphic 元素&#40;ASSL&#41;](trendgraphic-element-assl.md)|包含 `Kpi` 元素走向的建议图形表示形式。|  
|[Trimming 元素&#40;ASSL&#41;](trimming-element-assl.md)|指定如何修整数据源的数据。|  
|[Type 元素&#40;操作&#41; &#40;ASSL&#41;](type-element-action-assl.md)|包含 `Action` 元素的类型。|  
|[Type 元素&#40;绑定&#41; &#40;ASSL&#41;](type-element-binding-assl.md)|包含属性绑定的类型。|  
|[Type 元素&#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](type-element-clrassemblyfile-assl.md)|指定一个属于.NET Framework 程序集的文件的文件类型。|  
|[Type 元素&#40;维度&#41; &#40;ASSL&#41;](type-element-dimension-assl.md)|提供有关维度内容的信息。|  
|[Type 元素&#40;DimensionAttribute&#41; &#40;ASSL&#41;](type-element-dimensionattribute-assl.md)|包含属性的类型。|  
|[Type 元素&#40;度量值组&#41; &#40;ASSL&#41;](type-element-measuregroup-assl.md)|指定的类型`MeasureGroup`。|  
|[Type 元素&#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](type-element-measuregroupattribute-assl.md)|包含的类型[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)元素。|  
|[Type 元素&#40;MiningStructureColumn&#41; &#40;ASSL&#41;](type-element-miningstructurecolumn-assl.md)|包含的类型[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)元素。|  
|[Type 元素&#40;分区&#41; &#40;ASSL&#41;](type-element-partition-assl.md)|包含 `Partition` 元素的类型。|  
|[Type 元素&#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](type-element-perspectivecalculation-assl.md)|指示的类型[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)元素。|  
|[UnknownMember 元素&#40;ASSL&#41;](unknownmember-element-assl.md)|指示未知成员是否可见。|  
|[UnknownMemberName 元素&#40;ASSL&#41;](unknownmembername-element-assl.md)|包含维度的未知成员的标题（以维度的默认语言显示）|  
|[Usage 元素&#40;DimensionAttribute&#41; &#40;ASSL&#41;](usage-element-dimensionattribute-assl.md)|说明如何使用属性。|  
|[Usage 元素&#40;MiningModelColumn&#41; &#40;ASSL&#41;](usage-element-miningmodelcolumn-assl.md)|介绍如何使用父级 `MiningStructure` 中的相关列。|  
|[值元素&#40;ASSL&#41;](value-element-assl.md)|包含父元素的值。|  
|[Version 元素&#40;ASSL&#41;](version-element-assl.md)|包含 `Server` 元素表示的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的只读版本号。|  
|[Visibility 元素&#40;ASSL&#41;](visibility-element-assl.md)|定义的可见性[批注](../objects/annotation-element-assl.md)元素。|  
|[Visible 元素&#40;ASSL&#41;](visible-element-assl.md)|确定父元素的可见性。|  
|[VisualTotals 元素&#40;ASSL&#41;](visualtotals-element-assl.md)|包含一个 MDX 表达式，该表达式可确定是否显示此属性成员的直观合计。|  
|[将元素写入&#40;ASSL&#41;](write-element-assl.md)|确定是否可为给定 `CubeDimensionPermission` 或 `Permission` 元素编写数据或元数据。|  
|[WriteEnabled 元素&#40;ASSL&#41;](writeenabled-element-assl.md)|指示维度写回是否可用（视安全权限而定）。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构&#40;ASSL&#41;](../analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
