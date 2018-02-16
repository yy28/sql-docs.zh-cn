---
title: "指定查询轴 (MDX) 的内容 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cellsets [MDX]
- query axis [MDX]
ms.assetid: c745ade0-738e-4a98-a3f0-3eabfd3eeba2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 99ee0b35cbb913a1e0332bda07394fe6541309a4
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-query-axis"></a>MDX 查询轴和切片器轴-指定查询轴的内容
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
查询轴用于指定多维表达式 (MDX) SELECT 语句返回的单元集的范围。 通过指定单元集的范围可以限定客户端可以看到的返回数据。  
  
 若要指定查询轴，请使用 `<SELECT query axis clause>` 将某个集分配给特定的查询轴。 每个 `<SELECT query axis clause>` 值均定义一个查询轴。 数据集中的轴数等于 SELECT 语句中 `<SELECT query axis clause>` 值的数目。  
  
## <a name="query-axis-syntax"></a>查询轴的语法  
 以下语法显示了 `<SELECT query axis clause>`的语法：  
  
```  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression [ <SELECT dimension property list clause> ] [<HAVING clause>]  
   ON {  
      Integer_Expression |   
      AXIS( Integer_Expression ) |   
      {COLUMNS | ROWS | PAGES | SECTIONS | CHAPTERS}     
      }  
  
```  
  
 每个查询轴具有一个编号：零 (0) 表示 x 轴，1 表示 y 轴，2 表示 z 轴，依此类推。 在 `<SELECT query axis clause>`的语法中， `Integer_Expression` 值指定了轴编号。 MDX 查询最多可以指定 128 个轴，但几乎没有 MDX 查询会用到 5 个以上的轴。 对于前 5 个轴，也可以改为使用 COLUMNS、ROWS、PAGES、SECTIONS 和 CHAPTERS 别名。  
  
 MDX 查询无法跳过查询轴。 也就是说，包括一个或多个查询轴的查询不能排除编号较低的轴或中间轴。 例如，查询不能有 ROWS 轴而无 COLUMNS 轴，或有 COLUMNS 和 PAGES 轴而无 ROWS 轴。  
  
 但是，可以指定不带任何轴的 SELECT 子句，即，空的 SELECT 子句。 在这种情况下，所有维度均为切片器维度，并且 MDX 查询选择一个单元。  
  
 在前面所示的查询轴语法中，每个 `Set_Expression` 值均指定用于定义查询轴内容的集。 有关集的详细信息，请参阅[使用成员、元组和集 (MDX)](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
## <a name="examples"></a>示例  
 下面的简单 SELECT 语句针对 Columns 轴返回度量值 Internet Sales Amount，并使用 MDX MEMBERS 函数返回 Rows 轴的 Date 维度上的 Calendar 层次结构中的所有成员。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 下面的两个查询返回完全相同的结果，但说明的是使用轴编号而不是别名：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON 0,  
{[Date].[Calendar].MEMBERS} ON 1  
FROM [Adventure Works]  
  
SELECT {[Measures].[Internet Sales Amount]} ON AXIS(0),  
{[Date].[Calendar].MEMBERS} ON AXIS(1)  
FROM [Adventure Works]  
  
```  
  
 在集定义前面使用的 NON EMPTY 关键字提供了一种简便方法，从轴中删除所有空元组。 例如，在这些示例中，到目前为止，我们还没有在多维数据集中看到 2004 年 8 月以后的数据。 要从单元集中删除列中没有数据的所有行，只需在 Rows 轴定义中的集前面添加 NON EMPTY 即可，如下所示：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].MEMBERS} ON ROWS  
FROM [Adventure Works]  
  
```  
  
 可以在查询中的所有轴上使用 NON EMPTY。 将以下两个查询的结果进行比较，第一个结果不使用 NON EMPTY，第二个结果在两个轴上都使用 NON EMPTY：  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
SELECT NON EMPTY {[Measures].[Internet Sales Amount]}   
* [Promotion].[Promotion].[Promotion].MEMBERS  
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Calendar Year].MEMBERS} ON ROWS  
FROM [Adventure Works]  
WHERE([Product].[Subcategory].&[19])  
  
```  
  
 可以使用 HAVING 子句基于特定条件筛选某个轴的内容；它没有可获得相同结果的其他方法（如 FILTER 函数）灵活，但使用起来更简单一些。 下面的示例仅返回 Internet Sales Amount 大于 $15,000 的日期：  
  
```  
SELECT {[Measures].[Internet Sales Amount]}   
ON COLUMNS,  
NON EMPTY  
{[Date].[Calendar].[Date].MEMBERS}   
HAVING [Measures].[Internet Sales Amount]>15000  
ON ROWS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [指定切片器轴 &#40; 的内容MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
