---
title: 维度特性属性参考 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b4667930214fff6b0c3d620e68a1ceaf0f22de7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-attribute-properties-reference"></a>维度特性属性参考
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，提供了许多可确定维度和维度特性工作方式的属性。 下表列出了这些特性属性并逐一对其进行说明。  
  
|属性|Description|  
|--------------|-----------------|  
|**AttributeHierarchyDisplayFolder**|标识向最终用户显示关联的特性层次结构的文件夹。|  
|**AttributeHierarchyEnabled**|确定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 是否为特性生成特性层次结构。 如果未启用特性层次结构，则不能在用户定义的层次结构中使用该特性，也不能在多维表达式 (MDX) 语句中引用该特性层次结构。|  
|**AttributeHierarchyOptimizedState**|确定应用于属性层次结构的优化级别。 默认情况下，特性层次结构处于 **FullyOptimized**状态，也就是说 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会为特性层次结构生成索引以提高查询性能。 另一个选项 **NotOptimized**表示没有为该特性层次结构生成索引。 如果特性层次结构用于查询之外的其他用途，则使用 **NotOptimized** 会很有用，因为不会为该特性生成其他索引。 特性层次结构的其他用途可用于帮助对另一个特性进行排序。|  
|**AttributeHierarchyOrdered**|确定关联的属性层次结构是否已排序。 默认值是 **True**秒。 但是，如果某特性层次结构将不用于查询，则您可以通过将该属性的值更改为 **False**来节省处理时间。|  
|**AttributeHierarchyVisible**|确定属性层次结构是否对客户端应用程序可见。 默认值是 **True**秒。 但是，如果某特性层次结构将不用于查询，则您可以通过将该属性的值更改为 **False**来节省处理时间。|  
|**CustomRollupColumn**|指定定义自定义汇总公式的列。|  
|**CustomRollupPropertiesColumn**|指定包含自定义汇总公式的属性的列。|  
|**DefaultMember**|指定用于定义该特性默认度量值的多维表达式 (MDX)。|  
|**Description**|包含对特性的说明。|  
|**DiscretizationBucketCount**|包含以其进行离散化的存储桶数。|  
|**DiscretizationMethod**|定义用于离散化的方法。|  
|**EstimatedCount**|指定该特性的估计成员数。 在运行聚合设计向导之前，该值默认为零。 您可以允许向导对记录数目进行计数，也可以输入一个估计值。 如果您知道成员数目并且希望减少在数据库中查询计数所需的时间，则可以手动输入值。 如果正在使用生产数据的测试子集，则可以使用生产数据的计数，从而针对生产数据而不是测试数据来优化聚合设计。|  
|**GroupingBehavior**|一个用户定义的值，可为客户端应用程序提供如何对特性进行分组的提示。|  
|**ID**|包含维度的唯一标识符 (ID)。|  
|**InstanceSelection**|向客户端应用程序提供提示，建议应该如何根据列表中预期的项数来显示项列表。 可用选项如下所示：<br /><br /> **None** 对客户端应用程序不提供提示。 这是默认值。<br /><br /> **DropDown** 项数很少，足以在下拉列表中显示。<br /><br /> **List** 项数太多，无法在下拉中显示，但不需要进行筛选。<br /><br /> **FilteredList** 项数太多，需要用户进行筛选，然后才能显示。<br /><br /> **MandatoryFilter** 项数太多，必须一直使用筛选才能显示。|  
|**IsAggregatable**|指定是否可以聚合特性成员的值。 默认值为 **True**，表示特性层次结构将包含“(全部)”级别。 如果该属性的值为 **False**，则此特性层次结构不包含“(全部)”级别。|  
|**KeyColumns**|包含表示特性键的一个或多个列，这些列是数据源视图的基础关系表中与该特性绑定在一起的列。 除非为 **NameColumn** 属性指定一个值，否则，将为用户显示每个成员该列的值。|  
|**MemberNamesUnique**|确定特性层次结构中的成员名称是否必须唯一。|  
|**MembersWithData**|父特性用于确定是否显示父特性中非叶成员的数据成员。 仅当 **Usage** 属性的值设置为 Parent 时才使用该属性值。 也就是说已定义父子层次结构。 可用选项如下所示：<br /><br /> **NonLeafDataHidden** 非叶数据已隐藏。<br /><br /> **NonLeafDataVisible** 非叶数据可见。|  
|**MembersWithDataCaption**|提供父特性为其系统生成的数据成员创建标题时所用的模板字符串。 仅当 **Usage** 属性的值设置为 Parent 时才使用该属性值。 也就是说已定义父子层次结构。|  
|**名称**|包含特性的用户友好名称。|  
|**NameColumn**|标识提供显示给用户的特性名称的列，而不是特性键列中的值。 当特性成员的键列值隐晦不清或对用户来说没用时，或者当键列基于组合键时，将使用该列。 **NameColumn** 属性不用于父子层次结构中，而是将子成员的 **NameColumn** 属性用作父子层次结构中的成员名称。|  
|**NamingTemplate**|定义如何在基于父特性构造的父子层次结构中命名级别。 仅当 **Usage** 属性的值设置为 Parent 时才使用该属性值。 也就是说已定义父子层次结构。|  
|**OrderBy**|说明如何对特性层次结构中包含的成员进行排序。 默认值为 Name，该值指定了特性成员的排序基于 **NameColumn** 属性的值（如果有）。 否则，按键列的值对成员进行排序。 可用选项如下所示：<br /><br /> **NameColumn** 按 **NameColumn** 属性的值进行排序。<br /><br /> **Key** 按特性成员键列值进行排序。<br /><br /> **AttributeKey** 按指定特性的成员键值进行排序，该特性必须与此特性具有特性关系。<br /><br /> **AttributeName** 按指定特性的成员名称值进行排序，该特性必须与此特性具有特性关系。|  
|**OrderByAttribute**|标识对特性层次结构成员进行排序所依据的特性。|  
|**RootMemberIf**|确定如何识别父子层次结构的根成员或最顶层成员。 仅当 **Usage** 属性的值设置为 Parent 时才使用该属性值。 也就是说已定义父子层次结构。 默认值为 **ParentIsBlankSelfOrMissing**，表示只有符合一个或多个为 **ParentIsBlank**、 **ParentIsSelf**或 **ParentIsMissing** 所描述的条件的成员才被视为根成员。 下面是其他可用的值：<br /><br /> **ParentIsBlank** 只有键列中具有空字符串的成员才被视为根成员。<br /><br /> **ParentIsSelf** 只有本身为父级的成员才被视为根成员。<br /><br /> **ParentIsMissing** 只有无法找到父级的成员才被视为根成员。|  
|**类型**|包含属性的类型。 有关详细信息，请参阅 [配置属性类型](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md)。|  
|**UnaryOperatorColumn**|指定提供一元运算符的列。 这是 DataItem 类型的绑定，它定义了提供一元运算符的列的详细信息。|  
|**Usage**|说明如何使用属性。<br /><br /> 可用选项如下所示：<br /><br /> **Regular** 该特性为常规特性。 这是默认值。<br /><br /> **Key** 该特性为键特性。<br /><br /> **Parent** 该特性为父特性。|  
|**ValueColumn**|标识提供特性值的列。 如果指定了特性的 **NameColumn** 元素，则将使用相同的 **DataItem** 值作为 **ValueColumn** 元素的默认值。 如果未指定特性的 **NameColumn** 元素并且特性的 **KeyColumns** 集合包含单个表示字符串数据类型键列的 **KeyColumn** 元素，则使用相同的 **DataItem** 值作为 **ValueColumn** 元素的默认值。|  
  
> [!NOTE]  
>  有关在处理 null 值和其他数据完整性问题时如何设置 **KeyColumn** 属性的值的详细信息，请参阅 [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891)（在 Analysis Services 2005 中处理数据完整性问题）。  
  
> [!NOTE]  
>  当查询中不显式包含层次结构中的成员时，将使用特性的默认成员来计算表达式。 特性的默认成员由特性的 **DefaultMember** 属性来指定。 当查询中包括维度的层次结构时，将忽略与该层次结构中的级别相对应的特性中的所有默认成员。 如果查询中不包括维度的层次结构，则默认成员将用于维度中的所有特性。 有关默认成员的详细信息，请参阅 [定义默认成员](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
