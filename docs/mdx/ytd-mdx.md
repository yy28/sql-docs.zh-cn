---
title: Ytd （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125763"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  从与给定成员相同的级别返回一组同级成员，从第一个同级成员开始，到给定成员的末尾，按时间维度中的*年份*级别进行约束。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员表达式，则默认值为第一个层次结构的当前成员，该层次结构的第一个层次结构中的类型为 "*年*"，在度量值组中的类型为*Time* 。  
  
 **Ytd**函数是[PeriodsToDate](../mdx/periodstodate-mdx.md)函数的快捷函数，其中级别所基于的属性层次结构的 Type 属性设置为 "*年份*"。 也就是说，`Ytd(Member_Expression)` 等效于 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 请注意，在 Type 属性设置为*FiscalYears*时，此函数将不起作用。  
  
## <a name="example"></a>示例  
 下面的示例返回从**艾德工作**多维`Measures.[Order Quantity]`数据集中包含在`Date`维度中的前八个月的日历年2003的成员的总和。  
  
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
  
 **Ytd**经常与未指定的参数结合使用，这意味着[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)函数将在报表中显示运行的累积年初至今总计，如以下查询所示：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
