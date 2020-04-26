---
title: 报表设计的 CSDLBI 属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7d2a9f075879ce1bfa0c0e7257ea8a2495562c0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "62757940"
---
# <a name="csdlbi-attributes-for-report-design"></a>用于报表设计的 CSDLBI 属性
  本节介绍用于表格建模的 CSDL 扩展插件中将会影响 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 查询设计的属性。  
  
## <a name="model-attributes"></a>模型属性  
 这些特性是在 CSDL [EntityContainer](https://msdn.microsoft.com/library/bb399169.aspx)元素的子元素上定义的。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|环境|Text|指示用于货币格式的区域性。 如果省略，则使用 EN-US。|  
|IsRightToLeft|布尔|指示文本字段值是否应默认为从右向左读取|  
  
## <a name="entity-attributes"></a>实体属性  
 这些属性是针对 CSDL EntitySet 或 EntityType 元素的子元素定义的。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用名称。|  
|`Caption`|Text|实体的显示名称。|  
|`Documentation`|Text|帮助业务用户理解数据含义的描述性文本。|  
|`Hidden`|布尔|指示是否应显示实体。 默认值为 `false`。|  
|`CollectionCaption`|Text|用于引用一组实体实例的复数名称。 如果省略，则使用 Caption 属性。|  
|`DisplayKey`|MemberRef[]|用于对业务用户标识实体实例的字段的排序列表。 这些引用可以包含实例属性和导航属性。 在引用某一导航属性时，将显示目标实体的 `DisplayKey`。 如果省略 `DisplayKey` 值，则使用键字段。|  
|`DefaultImage`|MemberRef|对包含用于在视觉上向业务用户标识实体实例的图像的字段的引用。 如果省略，则使用实体中的第一个图像字段（如果有）。|  
|`DefaultDetails`|MemberRef[]|表示详细信息的默认组的字段的排序列表，这些详细信息是显示给业务用户的有关实体实例的详细信息。如果省略，将使用实体中的前五 (5) 个字段，但不包括已由 `Key`、`DisplayKey` 或 `DefaultImage` 引用的那些字段。|  
|`SortProperties`|MemberRef[]|实体实例通常按其排序的字段的排序列表。 在对这些字段排序时，将使用对各字段指定的 `SortDirection`。 如果省略，则使用 `DisplayKey` 字段|  
|`DefaultMeasure`|MemberRef|对在模型中定义的度量值的引用，或者对具有默认聚合函数的数值字段的引用，以便指示该度量值或字段应该用作实体的多个实例的默认表示形式。 如果省略，则使用实体实例的计数。|  
|`DefaultLocation`|MemberRef|对其值表示与实体实例相关联的默认位置的字段的引用。 如果省略，则使用实体中的第一个位置字段（如果有）。|  
  
## <a name="field-attributes"></a>字段属性  
 这些属性是在 CSDL 属性或[NavigationProperty](https://msdn.microsoft.com/library/bb387104.aspx)元素的子元素上定义的。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用字段名称。|  
|`Caption`|Text|实体的显示名称。 如果省略，则使用字段`ReferenceName`的。|  
|`Documentation`|Text|帮助业务用户理解字段含义的描述性文本。|  
|`Hidden`|布尔|指示是否应显示字段。 默认值为 `false`，表示显示字段。|  
|`DisplayFolder`|Text|在其中显示此字段的文件夹的名称（完整路径）。 如果省略，则字段显示在模型根中。|  
|`ContextualNameRule`|枚举|一个值，该值指示是否以及如何基于使用其属性的上下文来修改属性名称。 可能的值有：`None`、`Role`、`Merge`。|  
|`Alignment`|枚举|一个值，该值指示在表格显示中应该如何对齐字段值。 可能的值有：`Default`、`Center`、`Left`、`Right`。 如果省略，则默认值根据字段的数据类型确定对齐方式。|  
|`FormatString`|Text|一个 .NET 格式字符串，指示默认情况下应如何设置字段值的格式。 如果省略，则假定采用以下格式：<br /><br /> -Datetime 字段：区域短日期或 "d"<br />-具有默认聚合函数的浮点字段和整数字段：地区性号或 "n"<br />-无默认聚合函数的整数：区域小数或 "d"<br /><br /> 对于所有其他类型的字段，没有任何格式字符串适用。|  
|`Units`|Text|适用于字段值以便表示单位的符号。 如果省略，则假定单位未知。|  
|`Width`|Integer|应为在表格表示形式中显示字段值而保留的首选宽度（字符）。 如果省略，则默认宽度基于字段的数据类型。|  
|`SortDirection`|枚举|指示通常如何对字段值进行排序的一个值。 可能的值有：`Default`、`Ascending`、`Descending`。 如果省略，则默认值将基于字段的数据类型分配排序方向。|  
|`IsRightToLeft`|布尔|指示字段是否包含应该从右向左读取的文本。 如果省略，则假定采用模型设置。|  
|`OrderBy`|MemberRef|对模型中另一个字段的引用，该字段定义此字段的值的排序顺序。 这两个字段的值必须具有 1:1 映射，否则排序行为是未定义的。 如果省略，则基于字段自己的值对字段进行排序。|  
|`Contents`|枚举|描述字段的子类型或内容的枚举。 如果省略，则不采用任何特定的子类型，除非该字段的数据类型为 Binary，在这种情况下，将采用 Image。 有关支持的内容类型的完整列表，请参阅 AMO 文档。|  
|`DefaultAggregateFunction`|枚举|一个值，指示通常用于对此字段进行聚合的默认函数（如果有）。 可能的值有：`None`、`Sum`、`Average`、`Count`、`Min`、`Max`。 如果省略，则假定对于数值字段为 `Sum`，对于所有其他字段则为 `None`。|  
|`IsSimpleMeasure`|布尔|指示度量值是否仅为数值字段的简单聚合。 此类聚合可以根据需要在查询中轻松地定义，因此，应该从模型定义中省略此类聚合以便提高性能。 如果省略，则假定为 `false`。|  
|`Kpi`<br /><br /> `KpiGoal`<br /><br /> `KpiStatus`|子元素|指示度量值元素要用作 KPI。 该 KPI 子元素使用 KpiGoal 和 KpiStauts 元素定义关联的显示图像和目标范围。|  
  
  
