---
title: 筛选器 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132694"
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
 **筛选器**函数计算指定的逻辑表达式对指定集中每个元组。 该函数返回指定集中的逻辑表达式的计算结果为每个元组构成的集 **，则返回 true**。 如果没有元组的计算结果为 **，则返回 true**，则返回空集。  
  
 **筛选器**函数的工作方式类似于[IIf](../mdx/iif-mdx.md)函数。 **IIf**函数将返回两个选项之一基于 MDX 逻辑表达式的计算，而**筛选器**函数将返回一组符合指定的搜索条件的元组。 实际上，**筛选器**函数执行`IIf(Logical_Expression, Set_Expression.Current, NULL)`集，并返回每个元组所得到的集。  
  
## <a name="examples"></a>示例  
 以下示例说明 Filter 函数在查询的行轴上的用法，以便仅返回 Internet Sales Amount 大于 $10000 的 Date：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Filter function 函数还可以在计算成员定义内部使用。 下面的示例返回的总和`Measures.[Order Quantity]`成员，2003 年中包含的第一个九个月内的聚合`Date`维度中，从**Adventure Works**多维数据集。 **PeriodsToDate**函数对其定义元组的集中**聚合**函数进行操作。 **筛选器**函数限制上一个时间段内返回到那些具有较低值 Reseller Sales Amount 度量值的那些元组。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
