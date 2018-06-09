---
title: PeriodsToDate (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e33ac5562e7304b71779134b02488733b9d576a4
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742546"
---
# <a name="periodstodate-mdx"></a>PeriodsToDate (MDX)


  按照时间维度中的指定级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。  
  
## <a name="syntax"></a>语法  
  
```  
  
PeriodsToDate( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 在指定级别的作用域内**PeriodsToDate**函数返回的一套段上与指定的成员，第一个期间开始和结束、 指定的成员相同的级别。  
  
-   如果指定一个级别，则层次结构的当前成员，则会推断*层次结构*。**CurrentMember**，其中*层次结构*是指定级别的层次结构。  
  
-   如果既未指定级别，也未指定成员，则该级别是度量值组中 Time 类型的第一个维度上第一个层次结构的当前成员的父级。  
  
 `PeriodsToDate( Level_Expression, Member_Expression )` 的功能与以下 MDX 表达式相同：  
  
 `TopCount(Descendants(Ancestor(Member_Expression, Level_Expression), Member_Expression.Level), 1):Member_Expression`  
  
## <a name="examples"></a>示例  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，在第一个八个月内的日历年 2003年中包含聚合`Date`维度，从**Adventure Works**多维数据集。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 下面的示例对 2003 日历年第二个半期的前两个月聚合。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Semester],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>请参阅  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
