---
title: Qtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 182a86a05cd0dae6adf85d2168fe884ace910a82
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278422"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  从与给定成员，从第一个同级成员开始和结尾的约束将给定成员相同的级别返回一组同级成员*季度*时间维度中的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员 expressionis，默认值是第一个层次结构的当前成员类型的级别*季度*类型的第一个维中*时间*度量值组中。  
  
 **Qtd**的快捷函数技术支持部门[PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md)其级别表达式参数设置为*季度*。 也就是说，`Qtd(Member_Expression)` 的功能与 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 相同。  
  
## <a name="example"></a>示例  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，包含在 2003年日历年度的第三季度前两个月内的聚合`Date`维度中，从**Adventure Works**多维数据集。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
