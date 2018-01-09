---
title: "报表设计的 CSDLBI 属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4b2c46d037112cb79502e8d0ce56a5c9c319ec09
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="csdlbi-attributes-for-report-design"></a>用于报表设计的 CSDLBI 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]本部分介绍在 CSDL 的扩展属性表格建模的影响[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]查询设计。  
  
## <a name="model-attributes"></a>模型属性  
 子元素的 CSDL 定义了这些属性[EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx)元素。  
  
|属性名称|数据类型|Description|  
|--------------------|---------------|-----------------|  
|Culture|文本|指示用于货币格式的区域性。 如果省略，则使用 EN-US。|  
|IsRightToLeft|Boolean|指示文本字段值是否应默认为从右向左读取|  
  
## <a name="entity-attributes"></a>实体属性  
 这些属性是针对 CSDL EntitySet 或 EntityType 元素的子元素定义的。  
  
|属性名称|数据类型|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|文本|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用名称。|  
|**Caption**|文本|实体的显示名称。|  
|**文档**|文本|帮助业务用户理解数据含义的描述性文本。|  
|**Hidden**|Boolean|指示是否应显示实体。 默认值为 **false**。|  
|**CollectionCaption**|文本|用于引用一组实体实例的复数名称。 如果省略，则使用 Caption 属性。|  
|**DisplayKey**|MemberRef[]|用于对业务用户标识实体实例的字段的排序列表。 这些引用可以包含实例属性和导航属性。 当引用导航属性时， **DisplayKey**实体显示的目标。 如果**DisplayKey**省略值，使用密钥字段。|  
|**DefaultImage**|MemberRef|对包含用于在视觉上向业务用户标识实体实例的图像的字段的引用。 如果省略，则使用实体中的第一个图像字段（如果有）。|  
|**DefaultDetails**|MemberRef[]|表示默认值的字段的已排序的列表设置的详细信息显示给业务用户实体实例有关的信息。如果省略，则使用实体中的第一次五 （5） 字段，但不包括那些已被引用**密钥**， **DisplayKey**，或**DefaultImage**。|  
|**SortProperties**|MemberRef[]|实体实例通常按其排序的字段的排序列表。 当对这些字段进行排序时**SortDirection**上每个指定使用字段。 如果省略， **DisplayKey**使用字段|  
|**DefaultMeasure**|MemberRef|对在模型中定义的度量值的引用，或者对具有默认聚合函数的数值字段的引用，以便指示该度量值或字段应该用作实体的多个实例的默认表示形式。 如果省略，则使用实体实例的计数。|  
|**位置**|MemberRef|对其值表示与实体实例相关联的默认位置的字段的引用。 如果省略，则使用实体中的第一个位置字段（如果有）。|  
  
## <a name="field-attributes"></a>字段属性  
 这些属性定义的 CSDL 属性的子元素上或[NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx)元素。  
  
|属性名称|数据类型|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|文本|用于在 DAX 查询中引用此实体的标识符。 如果省略，则使用字段名称。|  
|**Caption**|文本|实体的显示名称。 如果省略，则该字段的**ReferenceName**使用。|  
|**文档**|文本|帮助业务用户理解字段含义的描述性文本。|  
|**Hidden**|Boolean|指示是否应显示字段。 默认值是**false**，这意味着该字段将显示。|  
|**DisplayFolder**|文本|在其中显示此字段的文件夹的名称（完整路径）。 如果省略，则字段显示在模型根中。|  
|**ContextualNameRule**|Enum|一个值，该值指示是否以及如何基于使用其属性的上下文来修改属性名称。 可能的值为：**无**，**角色**，**合并**。|  
|**对齐**|Enum|一个值，该值指示在表格显示中应该如何对齐字段值。 可能的值为**默认**， **Center**，**左**，**右**。 如果省略，则默认值将基于字段的数据类型确定对齐方式。|  
|**FormatString**|文本|一个 .NET 格式字符串，指示默认应该如何设置字段值的格式。 如果省略，则假定采用以下格式：<br /><br /> -Datetime 字段： 区域的短日期或"d"<br /><br /> 的浮点字段和整数字段的默认聚合函数： 区域数或"n"<br /><br /> 的无默认值为整数聚合函数： 区域的十进制数或"d"<br /><br /> 对于所有其他类型的字段，没有任何格式字符串适用。|  
|**单位**|文本|适用于字段值以便表示单位的符号。 如果省略，则假定单位未知。|  
|宽度|Integer|应为在表格显示中显示字段值而保留的字符的首选宽度。 如果省略，则默认宽度将基于字段的数据类型。|  
|**SortDirection**|Enum|指示通常如何对字段值进行排序的一个值。 可能的值为**默认**，**升序**，**降序**。 如果省略，则分配排序方向的默认值将基于字段的数据类型。|  
|**IsRightToLeft**|Boolean|指示字段是否包含应该从右向左读取的文本。 如果省略，则假定采用模型设置。|  
|**OrderBy**|MemberRef|对模型内用于定义该字段值的排序顺序的其他字段的引用。 这两个字段的值必须具有 1:1 映射，否则排序行为是未定义的。 如果省略，则基于字段自己的值对字段进行排序。|  
|**目录**|Enum|描述字段的子类型或内容的枚举。 如果省略，则假定没有特定的子类型，除非该字段的数据类型为 Binary，在此情况下，假定为 Image。 有关支持的内容类型的完整列表，请参阅 AMO 文档。|  
|**DefaultAggregateFunction**|Enum|一个值，指示通常用于对此字段进行聚合的默认函数（如果有）。 可能的值为**无**，**总和**，**平均**，**计数**， **Min**，**最大**. 如果省略，**总和**对于数字字段，假定**无**为所有其他字段。|  
|**IsSimpleMeasure**|Boolean|指示度量值是否仅为数值字段的简单聚合。 此类聚合可以根据需要在查询中轻松地定义，因此，应该从模型定义中省略此类聚合以便提高性能。 如果省略， **false**假定。|  
|**Kpi**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|子元素|指示度量值元素要用作 KPI。 该 KPI 子元素使用 KpiGoal 和 KpiStauts 元素定义关联的显示图像和目标范围。|  
  
  
