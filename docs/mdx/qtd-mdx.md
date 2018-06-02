---
title: Qtd (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 218e90b5e43a1603978ba912fccb85ae16b34072
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580919"
---
# <a name="qtd-mdx"></a>Qtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  为给定成员，与第一个同级的开始和结束与约束通过将给定成员属于同一级别返回一组同级成员*季度*时间维度中的级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 如果未指定成员 expressionis，默认值是第一个层次结构使用的类型级别的当前成员*季度*中类型的第一个维度*时间*度量值组中。  
  
 **Qtd**函数是快捷函数[PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md)函数其级别表达式参数设置为*季度*。 也就是说，`Qtd(Member_Expression)` 的功能与 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 相同。  
  
## <a name="example"></a>示例  
 下面的示例返回的总和`Measures.[Order Quantity]`成员，在某段前两个月的公历 2003 年的第三个季度中包含聚合`Date`维度，从**Adventure Works**多维数据集。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
