---
title: "Analysis Services 脚本语言 XML 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Analysis Services Scripting Language XML Data Types
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
ms.assetid: 8e527916-932e-48ec-9010-f22cd4b721e2
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 63371810e2a7c41fab2935dfeb94a03b9250385a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-scripting-language-xml-data-types-assl"></a>Analysis Services 脚本语言 XML 数据类型 (ASSL)
  本参考部分包含在 Analysis Services 脚本语言 (ASSL) 架构中作为类型的每个元素的语法和用法信息。  
  
 尽管 ASSL 架构仅包含 XML 元素，从开发人员的角度来看，本部分中描述的元素对应于的类型，如**绑定**和**权限**，这是用于定义的子元素和其他对象的属性。  
  
 类型元素与对象元素类似，它们在 ASSL 架构中从不是叶级元素，而是包含了子元素和与对象属性对应的元素。  
  
 Type 元素但是永远不会显示为在定义或介绍的脚本元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象。 而是显示为其他对象指定的元素，通常与类型**类型**属性从 XML 架构实例架构使用**xsi: type**或**xs:type**。 例如， `<Assembly xsi:type="ClrAssembly">...</Assembly>`。  
  
 在某些情况下，一个类型派生自另一个类型。 例如， **CubeBinding**类型派生自父**绑定**类型。  
  
|元素|Description|  
|-------------|-----------------|  
|[操作数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|定义表示中的操作的抽象基元数据类型[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[AggregationAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationattribute-data-type-assl.md)|定义一个基元数据类型，表示之间的关联[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)元素和属性。|  
|[AggregationDesignAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)|定义表示属性之间的关联的基元数据类型和[AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)元素。|  
|[AggregationDesignDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)|定义一个基元数据类型，表示多维数据集维度之间的关系和[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素。|  
|[AggregationDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)|定义一个基元数据类型，表示维度之间的关系和[聚合](../../../analysis-services/scripting/objects/aggregation-element-assl.md)元素。|  
|[AggregationInstanceAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)|定义一个基元数据类型，该类型表示聚合实例使用的属性的相关信息。|  
|[AggregationInstanceCubeDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)|定义一个基元数据类型，该类型表示聚合实例使用的多维数据集维度的信息。|  
|[AggregationInstanceMeasure 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)|定义一个基元数据类型，该类型表示聚合实例所使用的度量值的相关信息。|  
|[程序集的数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/assembly-data-type-assl.md)|定义表示的抽象基元数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集或 COM 动态链接库 (DLL) 与关联[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[AttributeBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|定义一个派生的数据类型，表示的绑定[属性](../../../analysis-services/scripting/objects/attribute-element-assl.md)元素。|  
|[AttributeTranslation 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|定义一个派生的数据类型，表示与关联的翻译[属性](../../../analysis-services/scripting/objects/attribute-element-assl.md)元素|  
|[绑定数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|定义一个抽象的基元数据类型，该类型表示两个对象之间的依赖关系：在这两个对象中，一个对象的数据或元数据依赖于绑定对象的数据或元数据。|  
|[ClrAssembly 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|定义一个派生的数据类型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]与关联的程序集[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)或[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素|  
|[ClrAssemblyFile 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|定义一个基元数据类型，表示组成的文件之一[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程序集 ([ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)元素)。|  
|[ColumnBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|定义一个派生的数据类型，表示到数据源视图中的列的绑定[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)元素。|  
|[ComAssembly 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|定义一个派生的数据类型，表示与关联的 COM 库[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)或[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[CubeAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)|定义一个基元数据类型，表示与关联的特性[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[CubeAttributeBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|定义一个派生数据类型，该类型表示多维数据集维度中的属性与操作或挖掘结构列的绑定。|  
|[CubeBinding 数据类型 &#40; 超行 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|定义一个基元数据类型，表示之间的关系[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素和[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。|  
|[CubeDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|定义一个基元数据类型，该类型表示维度和多维数据集之间的关系。|  
|[CubeDimensionBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|定义一个派生的数据类型，表示的绑定[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[度量值](../../../analysis-services/scripting/objects/measure-element-assl.md)，或[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)到多维数据集维度的元素。|  
|[CubeDimensionPermission 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)|定义一个基元数据类型，该类型表示单个角色针对多维数据集中的某个特定维度具有的权限。|  
|[CubeHierarchy 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|定义一个基元数据类型，表示有关的信息[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)中的元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[DataBlock 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)|定义一个基元数据类型，表示用于存储的二进制内容组成的数据块的集合[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)元素。|  
|[DataItem 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|定义一个基元数据类型，该类型表示数据项的数据相关特征，如列或属性。|  
|[DataMiningMeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dataminingmeasuregroupdimension-data-type-assl.md)|定义一个派生数据类型，该类型表示某个度量值组和数据挖掘维度之间的关系。|  
|[数据源数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|定义表示中的数据源的抽象基元数据类型[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)元素。|  
|[DataSourceViewBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|定义一个派生数据类型，该类型表示数据源视图和父元素之间的绑定。|  
|[DegenerateMeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)|定义一个派生数据类型，该类型表示退化维度（即事实维度）和度量值组之间的关系。|  
|[Dimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|定义表示数据库维度的基元数据类型。|  
|[DimensionAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|定义一个基元数据类型，该类型表示维度中的属性。|  
|[DimensionBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|定义一个派生的数据类型，表示数据源之间的绑定和一个[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)元素。|  
|[DimensionPermission 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md)|定义一个派生数据类型，该类型表示分配给数据库维度的权限。|  
|[DrillThroughAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|定义表示钻取操作的派生数据类型。|  
|[DSVTableBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md)|定义一个派生的数据类型，表示一个表之间的绑定和一个[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)元素。|  
|[EventColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|定义一个基元数据类型，表示要为捕获的信息的列[事件](../../../analysis-services/scripting/objects/event-element-assl.md)作为的一部分的元素[跟踪](../../../analysis-services/scripting/objects/trace-element-assl.md)元素。|  
|[层次结构数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/hierarchy-data-type-assl.md)|定义一个表示维度中的层次结构的基元数据类型。|  
|[ImpersonationInfo 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|定义一个基元数据类型，该类型表示用于模拟用户的信息。|  
|[IncrementalProcessingNotification 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/incrementalprocessingnotification-data-type-assl.md)|定义一个派生的数据类型，它表示信息[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关要执行以确定的进度增量处理的查询的元素。|  
|[InheritedBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|定义一个派生的数据类型，该值指示[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)元素继承其绑定的属性。|  
|[ManyToManyMeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md)|定义一个派生的数据类型，该类型表示多对多维度和度量值组之间的关系。|  
|[MeasureBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|定义一个派生数据类型，该类型表示与父元素的度量值绑定。|  
|[MeasureGroupAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|定义一个基元数据类型，该类型表示属性和度量值组之间的关系。|  
|[MeasureGroupBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|定义一个派生的数据类型，表示一种绑定到[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素。|  
|[MeasureGroupBinding 数据类型 &#40; 超行 &#41;&#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|定义一个基元数据类型，该类型表示与度量值组的绑定。|  
|[MeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|定义一个抽象的基元数据类型，该类型表示某个维度和度量值组之间的关系。|  
|[MeasureGroupDimensionBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|定义一个派生数据类型，该类型表示某个维度和度量值组之间的绑定。|  
|[MeasureGroupHierarchy 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/measuregrouphierarchy-data-type-assl.md)|定义一个基元数据类型，该类型表示度量值组中层次结构的相关信息。|  
|[MiningModelColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)|定义一个基元数据类型，表示列中的相关信息[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。|  
|[MiningModelingFlag 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningmodelingflag-data-type-assl.md)|定义一个基元数据类型，表示的可用的建模标志[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)元素。|  
|[MiningStructureColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|定义表示列中的相关信息的抽象基元数据类型[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)元素。|  
|[OlapDataSource 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md)|定义一个派生的数据类型，表示多维[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。|  
|[PartitionBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|定义一个派生的数据类型，表示一种绑定到[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)元素。|  
|[权限数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|定义一个抽象的基元数据类型，该类型表示单个权限的相关信息。|  
|[PerspectiveAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|定义一个基元数据类型，表示有关中的操作信息[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[PerspectiveAttribute 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|定义一个基元数据类型，表示有关中的属性的信息[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)元素。|  
|[PerspectiveCalculation 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)|定义一个基元数据类型，表示计算之间的关系和[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[PerspectiveDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|定义一个基元数据类型，该类型表示透视中的维度的相关信息。|  
|[PerspectiveHierarchy 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|定义一个基元数据类型，表示有关层次结构中的信息[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)元素。|  
|[PerspectiveKpi 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|表示关键绩效指标 (KPI) 有关的信息的基元数据类型定义中[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[度量值数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|定义一个基元数据类型，表示有关中的度量值信息[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)元素。|  
|[PerspectiveMeasureGroup 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|定义一个基元数据类型，表示有关度量值组中的信息[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。|  
|[ProactiveCachingBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|定义表示信息，用以抽象派生的数据类型[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)元素有关数据源更改需要重新生成缓存，或重新生成进程的状态。|  
|[ProactiveCachingIncrementalProcessingBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingincrementalprocessingbinding-data-type-assl.md)|定义一个派生的数据类型，表示一种绑定到[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)过程的重新生成缓存的状态有关的元素。|  
|[ProactiveCachingInheritedBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachinginheritedbinding-data-type-assl.md)|定义一个派生的数据类型，表示信息，用以[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关数据源所更改的表和视图需要重新生成缓存的现有数据绑定通过标识的元素。|  
|[ProactiveCachingObjectNotificationBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|定义表示信息，用以抽象派生的数据类型[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关数据源更改的元素，在指定的表和视图或表和视图中通过标识现有数据需要重新生成缓存的绑定。|  
|[ProactiveCachingQueryBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingquerybinding-data-type-assl.md)|定义一个派生的数据类型，表示信息，用以[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)有关数据源所更改的表和视图，通过指定需要重新生成缓存的查询的执行标识的元素。|  
|[ProactiveCachingTablesBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingtablesbinding-data-type-assl.md)|定义一个派生的数据类型，表示信息，用以[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)元素中指定的表和视图，需要重新生成缓存的数据源更改。|  
|[PushedDataSource 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|定义一个基元数据类型，表示的数据源 (如[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]包) 用于将"推送"到数据[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。|  
|[QueryBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)|定义一个派生的数据类型，表示此关联的[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)具有元素[QueryDefinition](../../../analysis-services/scripting/properties/querydefinition-element-assl.md)元素。|  
|[ReferenceMeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md)|定义一个派生数据类型，该类型表示通过中间维度与事实数据表间接相关的维度。 （例如，“销售”度量值组可引用“地域”维度，它们之间通过“客户”维度相关联。）|  
|[RegularMeasureGroupDimension 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|定义一个派生数据类型，该类型表示某个维度和度量值组之间的常规关系。|  
|[RelationalDataSource 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md)|定义一个派生的数据类型，表示[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素基于关系数据源。|  
|[ReportAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)|定义一个派生数据类型，该类型表示可生成 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报告的操作。|  
|[RowBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|定义一个派生的数据类型，表示的绑定中的表行[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)元素。|  
|[ScalarMiningStructureColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|定义一个派生的数据类型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含标量值，而不是与关联的嵌套表的元素[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)包含嵌套的表的元素。|  
|[StandardAction 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|定义一个派生的数据类型，表示任何[操作](../../../analysis-services/scripting/objects/action-element-assl.md)以外的其他元素[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)元素或[ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)元素。|  
|[TableBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|定义一个派生数据类型，该类型表示与表的绑定。|  
|[TableMiningStructureColumn 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|定义一个派生的数据类型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含嵌套的表，而不是与关联的标量值的元素[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)包含标量值的元素。|  
|[TabularBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|定义一个抽象的派生数据类型，该类型表示与表格格式项（如表或多维数据集维度）的绑定。|  
|[TimeAttributeBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md)|定义一个派生数据类型，该类型表示服务器时间维度中生成数据项的“占位符”绑定，如属性的键列。|  
|[TimeBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|定义一个派生数据类型，该类型表示与时间段的绑定。|  
|[转换数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/translation-data-type-assl.md)|定义表示本地化翻译的基元数据类型。|  
|[UserDefinedGroupBinding 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|定义一个派生数据类型，该类型表示用户定义的属性分组。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 元素层次结构 &#40;ASSL &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
