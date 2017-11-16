---
title: "指定切片器轴 (MDX) 的内容 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- slicer axis
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a1b4ad6c837bb442af7f5bd5a98ab09527ef707
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-slicer-axis"></a>MDX 查询轴和切片器轴-指定切片器轴的内容
  切片器轴将对多维表达式 (MDX) SELECT 语句返回的数据进行筛选，限定返回的数据，从而只返回与指定成员相关的数据。 可以将其看成是在查询中不可见的多余的轴。 切片器轴是在 MDX 中 SELECT 语句的 WHERE 子句中定义的。  
  
## <a name="slicer-axis-syntax"></a>切片器轴的语法  
 若要显式指定切片器轴，请使用 MDX 中的 `<SELECT slicer axis clause>` ，如以下语法所述。  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 在所示的切片器轴语法中，可以向 `Set_Expression` 传递元组表达式（被视为集以便对子句求值）或集表达式。 如果指定了集表达式，则 MDX 通过将结果单元聚合到集的每个元组中，尝试对该集求值。 也就是说，MDX 将尝试对集使用 [Aggregate](../../../mdx/aggregate-mdx.md) 函数，用与其相关的聚合函数来聚合每个度量值。 另外，如果集表达式无法表示为属性层次结构成员的叉积，则 MDX 在求值时将切片器集表达式以外的单元视为空。  
  
> [!IMPORTANT]  
>  与 SQL 中的 WHERE 子句不同，MDX SELECT 语句的 WHERE 子句不从直接筛选针对查询行轴返回的内容。 若要筛选查询行或列轴上显示的内容，请使用多种 MDX 函数，例如 FILTER、NONEMPTY 和 TOPCOUNT。  
  
### <a name="implicit-slicer-axis"></a>隐式切片器轴  
 如果多维数据集中某个层次结构的成员未显式包括在查询轴中，则该层次结构的默认成员隐式包括在切片器轴中。 有关默认成员的详细信息，请参阅 [定义默认成员](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
## <a name="examples"></a>示例  
 下面的查询不包括 WHERE 子句，并返回所有日历年的 Internet Sales Amount 度量值。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 按如下方式添加 WHERE 子句：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 不会更改针对查询行或列返回的内容;它将更改针对每个单元返回的值。 在本示例中，将对查询进行切片，以使其针对所有日历年返回 Internet Sales Amount（但仅针对居住在美国的客户）。可以将来自不同层次结构的多个成员添加到 WHERE 子句中。 以下查询说明了针对居住在美国并在 Category Bikes 中购买了产品的客户的所有日历年的 Internet Sales Amount 的值。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 如果您要使用来自同一层次结构的多个成员，您需要在 WHERE 子句中包括一个集。 例如，以下查询说明了针对在 Category Bikes 中购买了产品并居住在美国或英国的客户的所有日历年的 Internet Sales Amount 的值：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 如上所述，如果使用 WHERE 子句的集，则会 隐式聚合该集中的所有成员的值。 在这种情况下，该查询说明了在每个单元中的美国和英国的聚合的值。  
  
  

