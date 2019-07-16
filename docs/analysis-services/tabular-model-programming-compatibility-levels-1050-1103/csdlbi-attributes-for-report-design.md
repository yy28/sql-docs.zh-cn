---
title: 用于报表设计的 CSDLBI 属性 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7f4b1ef3b46e4564ffc4622b39e8326adf443a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163454"
---
# <a name="csdlbi-attributes-for-report-design"></a>用于报表设计的 CSDLBI 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本节介绍用于表格建模的 CSDL 扩展插件中将会影响 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 查询设计的属性。  
  
## <a name="model-attributes"></a>模型属性  
 这些属性定义的子元素的 CSDL [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx)元素。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|Culture|Text|指示用于货币格式的区域性。 如果省略，则使用 EN-US。|  
|IsRightToLeft|Boolean|指示文本字段值是否应默认为从右向左读取|  
  
## <a name="entity-attributes"></a>实体属性  
 这些属性是针对 CSDL EntitySet 或 EntityType 元素的子元素定义的。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Text|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用名称。|  
|**Caption**|Text|实体的显示名称。|  
|**文档**|Text|帮助业务用户理解数据含义的描述性文本。|  
|**Hidden**|Boolean|指示是否应显示实体。 默认值为 **false**。|  
|**CollectionCaption**|Text|用于引用一组实体实例的复数名称。 如果省略，则使用 Caption 属性。|  
|**DisplayKey**|MemberRef[]|用于对业务用户标识实体实例的字段的排序列表。 这些引用可以包含实例属性和导航属性。 当引用导航属性时， **DisplayKey**目标的显示实体。 如果**DisplayKey**省略值，则使用键字段。|  
|**DefaultImage**|MemberRef|对包含用于在视觉上向业务用户标识实体实例的图像的字段的引用。 如果省略，则使用实体中的第一个图像字段（如果有）。|  
|**DefaultDetails**|MemberRef[]|表示默认值的字段的排序的列表设置的详细信息显示给业务用户的有关实体实例的信息。如果省略，使用实体中的第一次五 （5） 字段，但不包括那些已被**键**， **DisplayKey**，或**DefaultImage**。|  
|**SortProperties**|MemberRef[]|实体实例通常按其排序的字段的排序列表。 当对这些字段进行排序**SortDirection**指定每个使用字段。 如果省略， **DisplayKey**使用字段|  
|**DefaultMeasure**|MemberRef|对在模型中定义的度量值的引用，或者对具有默认聚合函数的数值字段的引用，以便指示该度量值或字段应该用作实体的多个实例的默认表示形式。 如果省略，则使用实体实例的计数。|  
|**DefaultLocation**|MemberRef|对其值表示与实体实例相关联的默认位置的字段的引用。 如果省略，则使用实体中的第一个位置字段（如果有）。|  
  
## <a name="field-attributes"></a>字段属性  
 CSDL 属性的子元素定义了这些属性或[NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx)元素。  
  
|属性名称|数据类型|描述|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Text|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用字段名称。|  
|**Caption**|Text|实体的显示名称。 如果省略，该字段的**ReferenceName**使用。|  
|**文档**|Text|帮助业务用户理解字段含义的描述性文本。|  
|**Hidden**|Boolean|指示是否应显示字段。 默认值是**false**，这意味着该字段将显示。|  
|**DisplayFolder**|Text|在其中显示此字段的文件夹的名称（完整路径）。 如果省略，则字段显示在模型根中。|  
|**ContextualNameRule**|Enum|一个值，该值指示是否以及如何基于使用其属性的上下文来修改属性名称。 可能的值有：**无**，**角色**，**合并**。|  
|**对齐**|Enum|一个值，该值指示在表格显示中应该如何对齐字段值。 可能的值为**默认**， **Center**，**左侧**，**右侧**。 如果省略，默认值将确定基于字段的数据类型的对齐方式。|  
|**FormatString**|Text|默认情况下应如何格式化字段的值，该值指示一个.NET 格式字符串。 如果省略，则假定采用以下格式：<br /><br /> -Datetime 字段： 区域短日期或"d"<br /><br /> 的浮点字段和整型字段默认值聚合函数： 区域数字或"n"<br /><br /> -无默认值整数聚合函数： 区域小数或"d"<br /><br /> 对于所有其他类型的字段，没有任何格式字符串适用。|  
|**单位**|Text|适用于字段值以便表示单位的符号。 如果省略，则假定单位未知。|  
|宽度 |Integer|首选的宽度，以在表格显示中显示字段的值应保留的字符。 如果省略，则默认宽度基于字段的数据类型。|  
|**SortDirection**|Enum|指示通常如何对字段值进行排序的一个值。 可能的值为**默认**， **Ascending**，**降序**。 如果省略，默认值将分配排序方向基于字段的数据类型。|  
|**IsRightToLeft**|Boolean|指示字段是否包含应该从右向左读取的文本。 如果省略，则假定采用模型设置。|  
|**OrderBy**|MemberRef|对模型内用于定义此字段的值的排序顺序的另一个字段的引用。 这两个字段的值必须具有 1:1 映射，否则排序行为是未定义的。 如果省略，则基于字段自己的值对字段进行排序。|  
|**目录**|Enum|描述字段的子类型或内容的枚举。 如果省略，没有特定的子类型被假定，除非该字段的数据类型为 Binary，在这种情况下，假定为 Image。 有关支持的内容类型的完整列表，请参阅 AMO 文档。|  
|**DefaultAggregateFunction**|Enum|一个值，指示通常用于对此字段进行聚合的默认函数（如果有）。 可能的值为**无**， **Sum**，**平均**，**计数**， **Min**，**最大**. 如果省略，**总和**对于数值字段，则假定**None**对于所有其他字段。|  
|**IsSimpleMeasure**|Boolean|指示度量值是否仅为数值字段的简单聚合。 此类聚合可以根据需要在查询中轻松地定义，因此，应该从模型定义中省略此类聚合以便提高性能。 如果省略， **false**假定。|  
|**Kpi**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|子元素|指示度量值元素要用作 KPI。 该 KPI 子元素使用 KpiGoal 和 KpiStauts 元素定义关联的显示图像和目标范围。|  
  
  
