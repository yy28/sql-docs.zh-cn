---
description: Filter (MDX)
title: 筛选 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 026e4720803d828ae9ba96a4d3df7f5a72d59e8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387503"
---
# <a name="filter-mdx"></a>Filter (MDX)


  返回根据搜索条件对指定集进行筛选后得到的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Logical_Expression*  
 计算结果为 True 或 False 的有效多维表达式 (MDX) 逻辑表达式。  
  
## <a name="remarks"></a>备注  
 **Filter**函数对指定集中的每个元组计算指定的逻辑表达式。 函数返回一个集，该集由指定集中的每个元组组成，其中逻辑表达式的计算结果为 **true**。 如果元组的计算结果不为 **true**，则返回空集。  
  
 **Filter**函数的工作方式与[IIf](../mdx/iif-mdx.md)函数的工作方式类似。 **IIf**函数基于 MDX 逻辑表达式的计算返回两个选项中的一个，而**Filter**函数返回一组满足指定的搜索条件的元组。 实际上， **筛选器** 函数 `IIf(Logical_Expression, Set_Expression.Current, NULL)` 在集合中的每个元组上执行，并返回结果集。  
  
## <a name="examples"></a>示例  
 以下示例说明 Filter 函数在查询的行轴上的用法，以便仅返回 Internet Sales Amount 大于 $10000 的 Date：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter function 函数还可以在计算成员定义内部使用。 下面的示例 `Measures.[Order Quantity]` `Date` 从 **艾德工作** 多维数据集中返回维度中包含的前九个月（2003）聚合的成员的总和。 **PeriodsToDate**函数定义**聚合**函数对其进行运算的集中的元组。 **筛选器**函数将返回的元组的值限制为具有较低值的元组，即上一个时间段的 "分销商销售额" 度量值。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
