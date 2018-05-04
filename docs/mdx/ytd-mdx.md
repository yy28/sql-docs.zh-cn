---
title: Ytd (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- YTD
dev_langs:
- kbMDX
helpviewer_keywords:
- Ytd function
ms.assetid: b77fdba2-d4a9-4271-8c21-c1f12eba526d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b647c31febd5ef06b8cb2e6f808e296518f98af6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="ytd-mdx"></a>Ytd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  为给定成员，与第一个同级的开始和结束与约束通过将给定成员属于同一级别返回一组同级成员*年*时间维度中的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果未指定一个成员表达式，默认值是第一个层次结构使用的类型级别的当前成员*年*中类型的第一个维度*时间*度量值组中。  
  
 **Ytd**函数是快捷函数[PeriodsToDate](../mdx/periodstodate-mdx.md)函数其中级别所基于的属性层次结构的类型属性设置为*年*。 也就是说，`Ytd(Member_Expression)` 等效于 `PeriodsToDate(Year_Level_Expression,Member_Expression)`。 请注意，此功能将不运行时类型属性设置为*FiscalYears*。  
  
## <a name="example"></a>示例  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，在第一个八个月内的日历年 2003年中包含聚合`Date`维度，从**Adventure Works**多维数据集。  
  
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
  
 **Ytd**不带参数指定，也就是说，通常用在组合[CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md)函数将显示运行累积年度截止到现在总在报表中中, 所示以下查询：  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
