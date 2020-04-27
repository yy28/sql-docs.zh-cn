---
title: 使用成员属性（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c0326d45af68db966f120fa12e35eb59f30becc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074160"
---
# <a name="using-member-properties-mdx"></a>使用成员属性 (MDX)
  成员属性提供有关各个元组中的每个成员的基本信息。 此基本信息包括成员名、父级别、子成员数目等等。 成员属性适用于给定级别的所有成员。 就组织结构而言，成员属性可视为存储在单个维度上按维度组织的数据。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，成员属性被称为“属性关系”。 有关详细信息，请参阅 [属性关系](../../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
 成员属性可以是“内部” ** 的，也可以是“自定义” ** 的：  
  
 内部成员属性  
 所有成员都支持内部成员属性，如成员的格式化值；而维度和级别提供附加的内部维度和级别成员属性，如成员的 ID。  
  
 有关详细信息，请参阅[内部成员属性 (MDX)](mdx-member-properties-intrinsic-member-properties.md)。  
  
 用户定义成员属性  
 成员通常还与其他属性相关联。 例如，Products 级别可为每件产品提供 SKU、SRP、Weight 和 Volume 属性。 这些属性不是成员，但包含有关 Products 级别的成员的附加信息。  
  
 有关详细信息，请参阅[用户定义的成员属性 (MDX)](mdx-member-properties-user-defined-member-properties.md)。  
  
 内部成员属性和用户定义成员属性都可以通过使用`PROPERTIES`关键字或[properties](/sql/mdx/properties-mdx)函数进行检索。  
  
## <a name="using-the-properties-keyword"></a>使用 PROPERTIES 关键字  
 `PROPERTIES` 关键字指定要用于给定轴维度的成员属性。 关键字隐藏在 MDX SELECT 语句`<axis specification>`的子句中： [SELECT](/sql/mdx/mdx-data-manipulation-select) `PROPERTIES`  
  
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
>  有关 `<set>` 和 `<axis_name>` 值的详细信息，请参阅[指定查询轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
 `<dim_props>` 子句允许您使用 `PROPERTIES` 关键字查询维度、级别和成员属性。 下列语法显示了 `<dim_props>` 子句的格式：  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 `<property>` 语法的细分因要查询的属性而异：  
  
-   上下文相关的内部成员属性前必须是维度或级别的名称。 但是，非上下文相关的内部成员属性不能由维度或级别的名称限定。 有关如何将关键字与内部成员属性`PROPERTIES`一起使用的详细信息，请参阅[&#40;MDX&#41;的内部成员属性](mdx-member-properties-intrinsic-member-properties.md)。  
  
-   用户定义成员属性前应是其所在级别的名称。 有关如何将关键字与用户定义的`PROPERTIES`成员属性一起使用的详细信息，请参阅[&#40;MDX&#41;的用户定义的成员属性](mdx-member-properties-user-defined-member-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建和使用属性值 (MDX)](../../creating-and-using-property-values-mdx.md)  
  
  
