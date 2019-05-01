---
title: 使用集函数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca9c5e1a3e110e1f1f2f14e9bd9b52e245d457a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251592"
---
# <a name="using-set-functions"></a>使用集函数


  集函数从维度、层次结构、级别中检索集，或通过遍历这些对象中的成员的绝对位置和相对位置来检索集，从而以多种方法构造集。  
  
 与成员函数和元组函数一样，集函数对协商 Analysis Services 中的多维结构至关重要。 集函数对获得多维表达式 (MDX) 查询结果也很重要，因为集表达式定义了 MDX 查询的轴。  
  
 一个最常见的集函数是[成员&#40;设置&#41; &#40;MDX&#41; ](../mdx/members-set-mdx.md)函数，这将检索包含所有来自维度、 层次结构或级别的成员的集。 以下是该函数在查询中的用法示例：  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 另一个常用的函数是[叉积&#40;MDX&#41; ](../mdx/crossjoin-mdx.md)函数。 它返回元组的集，表示作为参数传递到该函数的集的笛卡尔积。 实际上，利用此函数可以在查询中创建“嵌套”轴或“交叉表”轴：  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 [后代&#40;MDX&#41; ](../mdx/descendants-mdx.md)函数是类似**子级**起作用，但功能更强大。 它返回层次结构中一个或多个级别任何成员的后代：  
  
 SELECT  
  
 [Measures].[Internet Sales Amount]  
  
 ON Columns,  
  
 //返回一个集，该集包含 Date 维度的 Calendar 层次结构中 Calendar Year  
  
 //2004 下的所有日期  
  
 DESCENDANTS(  
  
 [Date]。[Calendar]。[Calendar Year]。 & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 [顺序&#40;MDX&#41; ](../mdx/order-mdx.md)函数可以按升序或降序根据特定的数值表达式对集的内容进行排序。 以下查询返回的行成员与前一查询返回的行成员相同，但现在按 Internet Sales Amount 度量值对这些成员进行排序：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 此查询还说明如何将从一个集函数 Descendants 返回的集作为参数传递到另一个集函数 Order。  
  
 时编写查询，筛选根据某些条件的一组会非常有用，可以使用为此目的[筛选器&#40;MDX&#41; ](../mdx/filter-mdx.md)函数，如以下示例所示：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 另外，存在允许您以其他方式筛选集的更复杂的函数。 例如，以下查询说明[TopCount &#40;MDX&#41; ](../mdx/topcount-mdx.md)函数返回一组中的前 n 项：  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 最后就可以执行多个使用类似于函数的逻辑集运算[Intersect &#40;MDX&#41;](../mdx/intersect-mdx.md)，[联合&#40;MDX&#41; ](../mdx/union-mdx.md)并[&#40;MDX&#41; ](../mdx/except-mdx-function.md)函数。 以下查询说明后两个函数的示例：  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用成员函数](../mdx/using-member-functions.md)   
 [使用元组函数](../mdx/using-tuple-functions.md)  
  
  
