---
title: Ytd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67df625611f2451c3442d5d59b56c76dfc14a74a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63295160"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  从与给定成员，从第一个同级成员开始和结尾的约束将给定成员相同的级别返回一组同级成员*年*时间维度中的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员表达式，默认值是第一个层次结构的当前成员类型的级别*年*类型的第一个维中*时间*度量值组中。  
  
 **Ytd**的快捷函数技术支持部门[PeriodsToDate](../mdx/periodstodate-mdx.md)函数的属性层次结构级别所基于的 Type 属性设置为*年*。 也就是说，`Ytd(Member_Expression)` 等效于 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 请注意，此功能将不运行时的 Type 属性设置为*FiscalYears*。  
  
## <a name="example"></a>示例  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，包含在 2003年日历年度前八个月内的聚合`Date`维度中，从**Adventure Works**多维数据集。  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **Ytd**经常结合起来使用不带参数指定，这表示[CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md)函数将显示的年初至今的连续累积合计在报表中，如中所示以下查询：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
