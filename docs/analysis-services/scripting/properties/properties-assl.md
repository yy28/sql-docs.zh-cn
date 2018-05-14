---
title: 属性 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: af118a27fb1228d801cc7619efb268fbf7d56674
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="properties-assl"></a>属性 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本参考部分包含作为 Analysis Services 脚本语言 (ASSL) 架构中的对象属性的所有元素的语法和用法信息。  
  
 尽管 ASSL 架构只包含 XML 元素，但是从开发人员的角度来说，本节中介绍的元素是与介绍对象的属性对应的。  
  
 在 ASSL 架构中，属性为叶级元素，且不包含子元素或与其拥有的属性相对应的元素。  
  
 在少数情况下，架构中显示为属性的叶级元素可归类为对象，这是因为该元素的类型是对象类型。 例如，**源**的**维度**对象属于类型**DimensionBinding**。  
  
## <a name="in-this-section"></a>本節內容  
  
|元素|Description|  
|-------------|-----------------|  
|[访问元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/access-element-assl.md)|指示提供给访问级别[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)元素。|  
|[帐户元素&#40;ImpersonationInfo&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md)|包含的用户帐户的名称[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)数据类型。|  
|[AccountType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/accounttype-element-assl.md)|包含帐户类型中定义的名称[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[操作 Id 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/actionid-element-assl.md)|包含名称的[操作](../../../analysis-services/scripting/objects/action-element-assl.md)元素上定义[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)在中可用的元素[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素作为[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)元素。|  
|[管理元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/administer-element-assl.md)|指示在关联的权限是否包含管理权限**数据库**元素。|  
|[AggregateFunction 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md)|定义使用的聚合函数的类型[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)元素。|  
|[AggregationDesignID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)|标识[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素与关联[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。|  
|[AggregationFunction 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationfunction-element-assl.md)|包含要用于帐户类型的聚合函数。|  
|[AggregationID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationid-element-assl.md)|标识从聚合定义**AggregationDesign**元素，用于创建聚合实例。|  
|[AggregationInstanceSource 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)|标识的用户定义聚合实例绑定到数据源**分区**元素。|  
|[AggregationPrefix 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)|定义整个关联父元素中聚合名称所用的通用前缀。|  
|[AggregationStorage 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md)|标识聚合的存储方法。|  
|[AggregationType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md)|定义的由存储的聚合类型**分区**元素。|  
|[AggregationUsage 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)|控件如何聚合设计器中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]设计聚合。|  
|[算法元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)|定义使用的算法[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[Alias 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/alias-element-assl.md)|定义的别名[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)元素。|  
|[AllMemberAggregationUsage 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md)|控制 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的聚合设计器如何设计聚合。|  
|[AllMemberName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allmembername-element-assl.md)|默认语言的标题中包含的所有成员的[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)元素。|  
|[AllowBrowsing 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md)|定义是否的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有浏览权限**MiningModel**元素。|  
|[AllowDrillThrough 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|确定是否允许在父元素上执行钻取操作。|  
|[AllowDuplicateNames 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowduplicatenames-element-assl.md)|确定是否允许重复的名称在**层次结构**元素。|  
|[AllowedSet 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowedset-element-assl.md)|包含定义的允许权限集是集表达式**角色**特性的元素。|  
|[应用程序元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/application-element-assl.md)|标识与关联的应用程序**操作**元素。|  
|[AssociatedMeasureGroupID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)|包含的标识符 (ID) 的[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素与关联[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)元素或[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)元素。|  
|[AttributeAllMemberName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributeallmembername-element-assl.md)|包含以默认语言显示的维度的“全部”成员的标题。|  
|[AttributeHierarchyDisplayFolder 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md)|指定在其中显示关联的属性层次结构的文件夹。|  
|[AttributeHierarchyEnabled 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)|确定是否为属性启用属性层次结构。|  
|[AttributeHierarchyOptimizedState 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)|确定应用于属性层次结构的优化级别。|  
|[AttributeHierarchyOrdered 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md)|确定关联的属性层次结构是否已排序。|  
|[AttributeHierarchyVisible 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)|确定属性层次结构是否对客户端应用程序可见。|  
|[AttributeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|包含与父元素关联的属性的 ID。|  
|[审核元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/audit-element-assl.md)|指定[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素无法删除任何事件，即使这会导致服务器上的性能下降。|  
|[自动重新启动元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/autorestart-element-assl.md)|确定是否**跟踪**元素应自动重启[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服务会停止并重启。|  
|[BackColor 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/backcolor-element-assl.md)|描述父元素的颜色相关显示特征。|  
|[CacheMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/cachemode-element-assl.md)|确定用于定型在处理挖掘结构时检索的数据的缓存机制。|  
|[CalculationReference 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/calculationreference-element-assl.md)|包含命名的集或引用的计算的单元的名称**CalculationProperty**元素。|  
|[CalculationType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)|介绍的一种在关联中定义计算**CalculationProperty**元素。|  
|[CalendarEndDate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarenddate-element-assl.md)|定义结束日期的日历时间段[TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)元素。|  
|[CalendarLanguage 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarlanguage-element-assl.md)|定义使用的日历语言**TimeBinding**元素。|  
|[CalendarStartDate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/calendarstartdate-element-assl.md)|定义开始日期的日历时间段**TimeBinding**元素。|  
|[标题元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/caption-element-assl.md)|包含关联父元素的标题。|  
|[CaptionIsMdx 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/captionismdx-element-assl.md)|定义是否为标题**操作**元素是一个多维表达式 (MDX) 表达式。|  
|[基数元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/cardinality-element-assl.md)|指示所描述的关系的基数[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)或[RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)。|  
|[CaseCubeDimensionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/casecubedimensionid-element-assl.md)|包含关联数据挖掘维度与度量值组的多维数据集维度的 ID。|  
|[ClassifiedColumnID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/classifiedcolumnid-element-assl.md)|包含由分类的相关列的 ID [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)元素。|  
|[排序规则元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/collation-element-assl.md)|确定父元素使用的排序规则。|  
|[ColumnID 元素&#40;ColumnBinding&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/columnid-element-columnbinding-assl.md)|包含数据项所绑定到的表中的列的 ID。|  
|[ColumnID 元素&#40;EventColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|包含要作为的一部分捕获的事件信息的列的 ID**跟踪**元素。|  
|[条件元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/condition-element-assl.md)|包含一个 MDX 表达式，确定是否**操作**父元素将应用到目标。|  
|[ConnectionString 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/connectionstring-element-assl.md)|包含的加密的连接字符串[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。|  
|[ConnectionStringSecurity 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md)|指定是否出于安全目的从数据源连接字符串中抽取用户的密码。|  
|[内容元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/content-element-assl.md)|描述中的列内容[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。|  
|[CreatedTimestamp 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)|包含父元素的只读创建时间戳。|  
|[CubeDimensionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/cubedimensionid-element-assl.md)|标识[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)与父元素相关联的元素。|  
|[CubeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/cubeid-element-assl.md)|标识**多维数据集**元素与关联[绑定](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)元素。|  
|[CurrentStorageMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)|确定父元素的当前存储模式。|  
|[CurrentTimeMember 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/currenttimemember-element-assl.md)|定义与维度关联的时间的当前成员**Kpi**元素。|  
|[DataAggregation 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/dataaggregation-element-assl.md)|确定实例是否可以聚合持久化的数据或缓存的数据的**MeasureGroup**。|  
|[DatabaseID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/databaseid-element-assl.md)|标识**数据库**超的行与关联的元素**绑定**元素。|  
|[DataSize 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasize-element-assl.md)|包含以字节为单位的大小[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)元素。|  
|[DataSourceID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)|标识**数据源**与父元素相关联的元素。|  
|[DataSourceImpersonationInfo 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)|包含用于连接到数据源时确定模拟行为的信息**数据库**元素。|  
|[DataSourceViewID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md)|标识[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)元素与关联**绑定**父元素。|  
|[数据类型元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/datatype-element-assl.md)|定义关联元素的数据类型。|  
|[DbSchemaName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md)|包含使用标识的表中的父元素的架构的名称[DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)元素。|  
|[DbTableName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|包含父元素绑定到的表的名称。|  
|[默认元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/default-element-assl.md)|确定是否**DrillThroughAction**默认钻取操作。|  
|[DefaultMeasure 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md)|包含定义的默认度量值的 MDX 语言表达式**多维数据集**或**透视**元素。|  
|[DefaultMember 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultmember-element-assl.md)|包含标识父元素的默认成员的 MDX 表达式。|  
|[DefaultScript 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultscript-element-assl.md)|标识默认[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)中的元素[mdxscript 被](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)集合。|  
|[DefaultValue 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/defaultvalue-element-assl.md)|包含关联的只读的默认值[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)元素。|  
|[DeniedSet 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/deniedset-element-assl.md)|包含一个集表达式，该表达式定义关联属性所拒绝的权限的列表。|  
|[DependsOnDimensionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/dependsondimensionid-element-assl.md)|包含父维度所依赖的其他维度的 ID。|  
|[Description 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/description-element-assl.md)|包含父元素的说明。|  
|[DimensionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)|包含维度的 ID。|  
|[DiscretizationBucketCount 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)|包含以其进行离散化的存储桶数。|  
|[DiscretizationMethod 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)|定义用于离散化的方法。|  
|[DisplayFlag 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/displayflag-element-assl.md)|包含一个只读的提示，指示是否应显示用户界面组件关联**ServerProperty**元素。|  
|[DisplayFolder 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)|指定要在其中列出父元素的文件夹。 对于开发人员和管理员来说，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 应用程序可能支持使用显示文件夹，从而直观地对多个元素进行分类。|  
|[分发元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/distribution-element-assl.md)|包含一个提供程序特定值，描述如何标量值的列中分发**MiningStructure**元素。|  
|[版本元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/edition-element-assl.md)|包含的实例的只读版本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。|  
|[启用元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/enabled-element-assl.md)|指示是否启用了父元素。|  
|[EndOfData 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/endofdata-element-assl.md)|指示从接收的数据的末尾[PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)元素。|  
|[EstimatedCount 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md)|包含属性的估计的成员数。|  
|[EstimatedPerformanceGain 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md)|包含估计的分区性能提升的只读百分比。|  
|[EstimatedRows 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)|包含由父元素表示的估计行数。|  
|[EstimatedSize 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md)|包含父元素的只读估计大小（以字节为单位）。|  
|[EventID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/eventid-element-assl.md)|唯一标识[事件](../../../analysis-services/scripting/objects/event-element-assl.md)元素要作为的一部分捕获**跟踪**元素。|  
|[表达式元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/expression-element-assl.md)|包含定义父元素内容的 MDX 表达式。|  
|[筛选元素&#40;绑定&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/filter-element-binding-assl.md)|包含筛选父元素内容的 MDX 表达式。|  
|[筛选元素&#40;跟踪&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/filter-element-trace-assl.md)|包含 XML 文档片段描述**跟踪**筛选器。|  
|[FirstDayOfWeek 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/firstdayofweek-element-assl.md)|定义为一周的第一天**TimeBinding**元素。|  
|[FiscalFirstDayOfMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalfirstdayofmonth-element-assl.md)|定义的会计月份的第一天**TimeBinding**元素。|  
|[FiscalFirstMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalfirstmonth-element-assl.md)|定义的会计期间的第一个月**TimeBinding**元素。|  
|[FiscalYearName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fiscalyearname-element-assl.md)|定义的命名约定为会计年度的名称为**TimeBinding**元素。|  
|[FontFlags 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontflags-element-assl.md)|描述字体相关显示特征**CalculationProperty**或**度量值**父元素。|  
|[字体名称元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontname-element-assl.md)|描述字体相关显示特征**CalculationProperty**或**度量值**父元素。|  
|[FontSize 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/fontsize-element-assl.md)|描述字体相关显示特征**CalculationProperty**或**度量值**父元素。|  
|[ForceRebuildInterval 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md)|确定在多维 OLAP (MOLAP) 映像可用后经过多长时间才能无条件开始 MOLAP 映像处理。|  
|[前景色元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/forecolor-element-assl.md)|介绍颜色相关显示特征**CalculationProperty**或**度量值**父元素。|  
|[设置元素的格式&#40;ASSL&#41;](../../../analysis-services/scripting/properties/format-element-assl.md)|包含所需的格式的**DataItem**元素。|  
|[FormatString 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/formatstring-element-assl.md)|描述的显示格式**CalculationProperty**元素或**度量值**元素。|  
|[目标元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/goal-element-assl.md)|标识在所需的目标**Kpi**元素。|  
|[GranularityAttributeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/granularityattributeid-element-assl.md)|包含与父项关联的属性 ID [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)数据类型。|  
|[HideMemberIf 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/hidememberif-element-assl.md)|指示是否应该从客户端应用程序中隐藏某一级别的成员以及何时隐藏。|  
|[HierarchyID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)|包含的 ID [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)， [MeasureGroupHierarchy](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)，或[PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)元素。|  
|[HierarchyUniqueNameStyle 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md)|确定如何唯一的名称中包含的层次结构生成**CubeDimension**。|  
|[ID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/id-element-assl.md)|包含父元素的唯一 ID。|  
|[IgnoreUnrelatedDimensions 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/ignoreunrelateddimensions-element-assl.md)|确定当查询中包括与度量值组无关的维度的成员时，是否将无关维度强制为顶级。|  
|[ImpersonationInfo 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)|包含用于确定访问或执行程序集时的模拟行为的信息。|  
|[ImpersonationInfoSecurity 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationinfosecurity-element-assl.md)|包含只读的值，该值指示是否已对中提供的安全凭据进行任何更改**ImpersonationInfo**数据类型。|  
|[ImpersonationMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)|包含一个值，指示派生自的元素的方法的模拟**ImpersonationInfo**数据类型。|  
|[InstanceSelection 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/instanceselection-element-assl.md)|提供对客户端应用程序建议如何的项列表的提示应显示，基于预期数量的列表中的项。|  
|[IntermediateCubeDimensionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/intermediatecubedimensionid-element-assl.md)|包含关联引用维度与度量值组的维度的 ID。|  
|[IntermediateGranularityAttributeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/intermediategranularityattributeid-element-assl.md)|包含中间多维数据集维度中的粒度属性的 ID，该 ID 用于关联引用维度和中间维度。|  
|[InvalidXmlCharacters 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md)|指定源数据中无效 XML 字符的处理方法。|  
|[调用元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/invocation-element-assl.md)|指定如何**操作**应被调用。|  
|[IsAggregatable 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md)|指定是否的值[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)可以聚合元素。|  
|[IsKey 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/iskey-element-assl.md)|指示列是否提供的密钥，这种情况在**MiningStructure**元素。|  
|[Isolation 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/isolation-element-assl.md)|该值指示元素派生自的隔离级别[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)数据类型。|  
|[KeyDuplicate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md)|确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何处理处理期间遇到的重复键错误。|  
|[KeyErrorAction 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md)|指定键发生错误时 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的操作。|  
|[KeyErrorLimit 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)|包含处理期间可接受的错误数。|  
|[KeyErrorLimitAction 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md)|指定的操作，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中指定键错误计数时采用[KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md)达到元素。|  
|[KeyErrorLogFile 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md)|包含记录处理错误的文件名。|  
|[KeyNotFound 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keynotfound-element-assl.md)|指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 遇到引用完整性错误时如何响应。|  
|[KeyUniquenessGuarantee 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md)|指示属性键和其名称之间的关系以及属性键和相关属性之间的关系是否保证有效。|  
|[KpiID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/kpiid-element-assl.md)|包含将相关联的 ID **Kpi**具有元素**透视**元素。|  
|[语言元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/language-element-assl.md)|包含父元素的语言标识符。|  
|[LastProcessed 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)|包含只读时间戳，该时间戳指示上次处理包含父元素的数据库的时间。|  
|[LastSchemaUpdate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)|包含父元素的只读元数据更新时间戳。|  
|[LastUpdate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/lastupdate-element-assl.md)|包含一个只读的时间戳指示上次时间关联**数据库**或任何主数据库包含的对象已更改。|  
|[延迟元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/latency-element-assl.md)|定义最早通知与 MOLAP 图像被破坏时刻之间的“宽限期”。|  
|[LogFileAppend 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfileappend-element-assl.md)|确定是否**跟踪**元素将其日志记录输出追加到现有的日志文件，或者覆盖它。|  
|[LogFileName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilename-element-assl.md)|包含的日志文件的文件名**跟踪**元素。|  
|[LogFileRollover 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilerollover-element-assl.md)|指定的日志记录是否**跟踪**输出应将鼠标移到新文件或者应停止时，它是大小最大的日志文件中指定的[LogFileSize](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)为止。|  
|[LogFileSize 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/logfilesize-element-assl.md)|指定最大日志文件大小 (MB)。|  
|[ManagedProvider 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/managedprovider-element-assl.md)|包含派生自元素所用的托管提供程序的名称**数据源**数据类型。|  
|[ManufacturingExtraMonthQuarter 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingextramonthquarter-element-assl.md)|定义为其分配额外月份的有关生产时间的月份**TimeBinding**元素。|  
|[ManufacturingFirstMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingfirstmonth-element-assl.md)|定义 **TimeBinding** 元素的第一个生产月。|  
|[ManufacturingFirstWeekOfMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/manufacturingfirstweekofmonth-element-assl.md)|定义生产月的第一周**TimeBinding**元素。|  
|[MasterDatasourceID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/masterdatasourceid-element-assl.md)|包含的主数据源 ID**数据库**元素。|  
|[具体化元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/materialization-element-assl.md)|指示度量值组和引用维度之间的关系类型。|  
|[MaxActiveConnections 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md)|包含的最大允许的元素派生自的并发连接数**数据源**数据类型。|  
|[MdxMissingMemberMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/mdxmissingmembermode-element-assl.md)|确定如何处理 MDX 语句中缺少的成员。|  
|[MeasureExpression 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/measureexpression-element-assl.md)|包含定义度量值的 MDX 表达式。|  
|[MeasureGroupID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md)|将相关联**MeasureGroup**与父元素、 绑定或扩展的外部绑定。|  
|[MeasureID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/measureid-element-assl.md)|将相关联**度量值**与父元素的元素。|  
|[MeasureQualificaton 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/measurequalificaton-element-assl.md)|确定是否对中的度量值应用前缀**MeasureGroup**。|  
|[MemberNamesUnique 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md)|确定父元素的成员名称是否必须是唯一的。|  
|[MemberUniqueNameStyle 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md)|确定如何唯一名称的层次结构中包含的成员生成**CubeDimension**元素。|  
|[MembersWithData 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)|确定是否显示父属性中非叶成员的数据成员。|  
|[MembersWithDataCaption 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)|提供用于为系统生成的数据成员创建标题的模板字符串。|  
|[MimeType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/mimetype-element-assl.md)|如果适用，则父级所表示的数据包含多用途 Internet 邮件扩展 (MIME) 类型， **DataItem**元素。|  
|[MiningModelID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/miningmodelid-element-assl.md)|将挖掘模型与数据挖掘维度关联。|  
|[命名元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)|包含父元素的名称。|  
|[NamingTemplate 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md)|定义级别从构造的父-子层次结构中的命名方式**DimensionAttribute**父元素。|  
|[NonEmptyBehavior 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md)|确定与的父项关联的非空行为**CalculationProperty**元素。|  
|[NotificationTechnique 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/notificationtechnique-element-assl.md)|指定是否[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或外部的客户端应用程序处理的通知。|  
|[NullKeyConvertedToUnknown 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md)|指定遇到空转换错误时要执行的操作。|  
|[NullKeyNotAllowed 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 处理引擎如何处理在处理过程中遇到空键错误。|  
|[NullProcessing 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)|定义如何处理空值。|  
|[OnlineMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/onlinemode-element-assl.md)|指定是在重新生成缓存刚一开始就立即使数据库恢复到联机状态，还是在完成重新生成缓存后才使数据库恢复到联机状态。|  
|[OptimizedState 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)|确定应用于层次结构的优化级别。|  
|[Optionality 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/optionality-element-assl.md)|指示成员的 optionality **AttributeRelationship**元素。|  
|[OrderBy 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/orderby-element-assl.md)|说明如何对属性中包含的成员进行排序。|  
|[OrderByAttributeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md)|标识所依据的成员进行排序的另一个属性[维度](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)属性。|  
|[序号元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/ordinal-element-assl.md)|指示要绑定到集合（如键和翻译）中的序号。|  
|[OverrideBehavior 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/overridebehavior-element-assl.md)|指示所描述的关系的重写行为**AttributeRelationship**元素。|  
|[PartitionID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/partitionid-element-assl.md)|将相关联**分区**具有父元素、 绑定或外部的绑定元素。|  
|[密码元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/password-element-assl.md)|包含的用户帐户的密码**ImpersonationInfo**元素。|  
|[路径元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/path-element-assl.md)|包含路径，则提供由的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，报表使用的[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)元素。|  
|[PendingValue 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/pendingvalue-element-assl.md)|包含只读的值关联的挂起**ServerProperty**元素。|  
|[PermissionSet 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|标识与关联的权限集[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 程序集。|  
|[持久性元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)|确定绑定的源数据的哪些部分是动态的并使用指定的频率更新检查[RefreshPolicy](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)元素。|  
|[处理元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/process-element-assl.md)|确定用户是否可以处理父元素的所有者。|  
|[ProcessingMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingmode-element-assl.md)|指示该实例应该在处理期间还是处理后进行索引和聚合。|  
|[ProcessingPriority 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)|确定在后台操作期间（例如迟缓聚合、索引或群集），父对象的处理优先级。|  
|[ProcessingQuery 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/processingquery-element-assl.md)|包含要为增量处理状态通知执行的查询的参数化文本。|  
|[ProductName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/productname-element-assl.md)|包含的实例的只读的产品名称[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]关联**服务器**元素。|  
|[查询元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/query-element-assl.md)|包含要为通知执行的查询的文本。|  
|[QueryDefinition 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/querydefinition-element-assl.md)|包含关联的查询的不透明表达式**数据源**中的元素[QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)元素。|  
|[读取元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/read-element-assl.md)|确定是否可以为读取数据或元数据给定[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)或[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)元素。|  
|[ReadDefinition 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/readdefinition-element-assl.md)|确定成员是否可以读取数据库的定义或数据库中对象的定义。|  
|[ReadSourceData 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/readsourcedata-element-assl.md)|确定如何唯一的名称中包含的层次结构生成**CubePermission**。|  
|[RefreshInterval 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md)|指定与父元素关联的绑定数据的刷新时间间隔。|  
|[RefreshPolicy 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/refreshpolicy-element-assl.md)|频率确定维度或度量值组的动态部分 (所指定的[持久性](../../../analysis-services/scripting/properties/persistence-element-assl.md)元素) 检查的更改。|  
|[RelationshipType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/relationshiptype-element-assl.md)|指示是否成员关系**AttributeRelationship**可以更改。|  
|[RemoteDatasourceID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)|指定 OLAP 数据源的 ID，该数据源指向存储远程分区的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。|  
|[ReportingFirstMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingfirstmonth-element-assl.md)|定义报表的第一个月**TimeBinding**元素。|  
|[ReportingFirstWeekOfMonth 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingfirstweekofmonth-element-assl.md)|定义报表一个月的第一周**TimeBinding**元素。|  
|[ReportingWeekToMonthPattern 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportingweektomonthpattern-element-assl.md)|定义的报表周月模式**TimeBinding**元素。|  
|[ReportServer 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|包含名称的[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]由的实例**ReportAction**。|  
|[RequiresRestart 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/requiresrestart-element-assl.md)|包含与关联的只读的值**ServerProperty**确定是否更改服务器属性的值需要以使更改生效，重新启动实例的元素。|  
|[RoleID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/roleid-element-assl.md)|标识要为其定义权限的角色。|  
|[根元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/root-element-assl.md)|包含数据源的数据（行集）。|  
|[其 RootMemberIf 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md)|确定如何识别父级属性的根成员或成员。|  
|[架构元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/schema-element-assl.md)|包含数据源视图的架构。|  
|[ScriptCacheProcessingMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md)|指示服务器在处理期间或处理之后是否生成脚本缓存。|  
|[SilenceInterval 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md)|定义在启动 MOLAP 图像处理进程之前，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例暂停的最短时间。|  
|[SilenceOverrideInterval 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md)|定义在接收初始通知之后，必须经过多长时间才能无条件开始 MOLAP 图像处理。|  
|[切片元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/slice-element-assl.md)|包含定义分区中的切片的 MDX 表达式。|  
|[SolveOrder 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/solveorder-element-assl.md)|指示在其中的求解次序**CalculationProperty**元素应用于计算的成员或计算的单元定义。|  
|[源元素&#40;绑定&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|标识父元素绑定到的数据源。|  
|[源元素&#40;ComAssembly&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-comassembly-assl.md)|包含组件对象模型 (COM) 组件的文件名或编程标识符 (ProgID)。|  
|[源元素&#40;度量值&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/source-element-measure-assl.md)|包含包含的值的源的详细信息**度量值**元素。|  
|[SourceAttributeID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/sourceattributeid-element-assl.md)|包含在其上的源属性 ID[级别](../../../analysis-services/scripting/objects/level-element-assl.md)基于元素。|  
|[SourceColumnID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/sourcecolumnid-element-assl.md)|包含在祖先的源挖掘结构列的 ID **MiningStructure**元素。|  
|[状态元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/state-element-assl.md)|包含一个只读值，它说明父元素的当前处理状态。|  
|[Status 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/status-element-assl.md)|包含一个 MDX 表达式，返回的状态指示器**Kpi**元素。|  
|[StatusGraphic 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/statusgraphic-element-assl.md)|包含的状态的建议图形表示形式**Kpi**元素。|  
|[停止时间元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/stoptime-element-assl.md)|指定的日期和时间**跟踪**元素应停止。|  
|[StorageLocation 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)|包含文件系统中的父元素内容存储位置。|  
|[StorageMode 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/storagemode-element-assl.md)|确定父元素的存储模式。|  
|[TableID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/tableid-element-assl.md)|包含表的 ID (从**DataSourceView**元素) 与父元素相关联。|  
|[目标元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/target-element-assl.md)|标识的目标**操作**元素。|  
|[TargetType 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/targettype-element-assl.md)|标识中标识的项的项类型[目标](../../../analysis-services/scripting/properties/target-element-assl.md)元素。|  
|[文本元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/text-element-assl.md)|包含文本的[命令](../../../analysis-services/scripting/objects/command-element-assl.md)元素。|  
|[超时元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/timeout-element-assl.md)|指定以秒为单位的一段时间，这段时间之后再试图检索数据将报告超时。|  
|[趋势元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)|包含一个 MDX 表达式，返回的趋势指示器**Kpi**元素。|  
|[TrendGraphic 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/trendgraphic-element-assl.md)|包含的趋势的建议图形表示形式**Kpi**元素。|  
|[修剪元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/trimming-element-assl.md)|指定如何修整数据源的数据。|  
|[类型元素&#40;操作&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-action-assl.md)|包含的一种**操作**元素。|  
|[类型元素&#40;绑定&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-binding-assl.md)|包含属性绑定的类型。|  
|[类型元素&#40;ClrAssemblyFile&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-clrassemblyfile-assl.md)|指定一个属于.NET Framework 程序集的文件的文件类型。|  
|[类型元素&#40;维度&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-dimension-assl.md)|提供有关维度内容的信息。|  
|[类型元素&#40;DimensionAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md)|包含属性的类型。|  
|[类型元素&#40;MeasureGroup&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-measuregroup-assl.md)|指定的一种**MeasureGroup**。|  
|[类型元素&#40;MeasureGroupAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-measuregroupattribute-assl.md)|包含的一种[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)元素。|  
|[类型元素&#40;MiningStructureColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-miningstructurecolumn-assl.md)|包含的一种[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)元素。|  
|[类型元素&#40;分区&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|包含的一种**分区**元素。|  
|[类型元素&#40;PerspectiveCalculation&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/type-element-perspectivecalculation-assl.md)|指示的一种[PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)元素。|  
|[UnknownMember 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/unknownmember-element-assl.md)|指示未知成员是否可见。|  
|[UnknownMemberName 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)|包含维度的未知成员的标题（以维度的默认语言显示）|  
|[使用情况元素&#40;DimensionAttribute&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)|说明如何使用属性。|  
|[使用情况元素&#40;MiningModelColumn&#41; &#40;ASSL&#41;](../../../analysis-services/scripting/properties/usage-element-miningmodelcolumn-assl.md)|描述如何关联的列的父代中**MiningStructure**使用。|  
|[值元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/value-element-assl.md)|包含父元素的值。|  
|[版本元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/version-element-assl.md)|包含只读版本的实例数[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]由**服务器**元素。|  
|[可见性元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/visibility-element-assl.md)|定义的可见性[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)元素。|  
|[可见元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/visible-element-assl.md)|确定父元素的可见性。|  
|[VisualTotals 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/visualtotals-element-assl.md)|包含一个 MDX 表达式，该表达式可确定是否显示此属性成员的直观合计。|  
|[写入元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/write-element-assl.md)|确定是否可以为编写数据或元数据给定**CubeDimensionPermission**或**权限**元素。|  
|[WriteEnabled 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/writeenabled-element-assl.md)|指示维度写回是否可用（视安全权限而定）。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构 & #40;ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
