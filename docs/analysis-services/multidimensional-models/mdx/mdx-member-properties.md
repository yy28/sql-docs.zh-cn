---
title: 使用成员属性 (MDX) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7876031fddb74115fd1fe412f4c8a9d9aacdb054
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740237"
---
# <a name="mdx-member-properties"></a>MDX 成员属性
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  成员属性提供有关各个元组中的每个成员的基本信息。 此基本信息包括成员名、父级别、子成员数目等等。 成员属性适用于给定级别的所有成员。 就组织结构而言，成员属性可视为存储在单个维度上按维度组织的数据。  
  
> [!NOTE]
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，成员属性被称为“属性关系”。 有关详细信息，请参阅 [属性关系](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
 成员属性可以是“内部”  的，也可以是“自定义”  的：  
  
 内部成员属性  
 所有成员都支持内部成员属性，如成员的格式化值；而维度和级别提供附加的内部维度和级别成员属性，如成员的 ID。  
  
 有关详细信息，请参阅[内部成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)。  
  
 用户定义成员属性  
 成员通常还与其他属性相关联。 例如，Products 级别可为每件产品提供 SKU、SRP、Weight 和 Volume 属性。 这些属性不是成员，但包含有关 Products 级别的成员的附加信息。  
  
 有关详细信息，请参阅[用户定义的成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
 内部成员属性和用户定义成员属性都可以通过使用 **PROPERTIES** 关键字或 [Properties](../../../mdx/properties-mdx.md) 函数进行检索。  
  
## <a name="using-the-properties-keyword"></a>使用 PROPERTIES 关键字  
 **PROPERTIES** 关键字指定要用于给定轴维度的成员属性。 **PROPERTIES** 关键字隐藏在 MDX `<axis specification>` SELECT [语句的](../../../mdx/mdx-data-manipulation-select.md) 子句中：  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 `<axis_specification>` 子句包含可选的 `<dim_props>` 子句，如下列语法所示：  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  有关 `<set>` 和 `<axis_name>` 值的详细信息，请参阅[指定查询轴的内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
 `<dim_props>` 子句允许使用 **PROPERTIES** 关键字查询维度、级别和成员属性。 下列语法显示了 `<dim_props>` 子句的格式：  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 `<property>` 语法的细分因要查询的属性而异：  
  
-   上下文相关的内部成员属性前必须是维度或级别的名称。 但是，非上下文相关的内部成员属性不能由维度或级别的名称限定。 有关如何将 **PROPERTIES** 关键字与内部成员属性一起使用的详细信息，请参阅[内部成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)。  
  
-   用户定义成员属性前应是其所在级别的名称。 有关如何将 **PROPERTIES** 关键字与内部成员属性一起使用的详细信息，请参阅[内部成员属性 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建和使用属性值 (MDX)](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  
