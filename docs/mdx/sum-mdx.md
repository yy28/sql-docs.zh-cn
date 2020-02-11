---
title: Sum （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb4e9d55ef2228404dd9113170066e4a3612a0a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036672"
---
# <a name="sum-mdx"></a>Sum (MDX)


  返回对指定集计算数值表达式求得的和。  
  
## <a name="syntax"></a>语法  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 有效的多维表达式 (MDX) 集表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则对集计算指定数值表达式的值然后求和。 如果没有指定数值表达式，则在指定集成员的当前上下文中计算指定集然后求和。 如果将 SUM 函数应用于非数值表达式，则结果不确定。  
  
> [!NOTE]  
>  计算一组数值的总和时，Analysis Services 将忽略空值。  
  
## <a name="examples"></a>示例  
 下例将返回 2001 和 2002 日历年 Product.Category 属性层次结构的所有成员的 Reseller Sales Amount 之和。  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 下例将返回截至 2002 年 7 月 20 日 7 月份的 Internet 销售运费之和。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例使用 WITH MEMBER 关键字和**SUM**函数在 "度量值" 维度中定义计算成员，该计算成员包含 "地域" 维度中 "国家/地区" 属性层次结构的 "分销商销售额" 度量美国值的总和。  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 通常情况下，SUM 函数与**CURRENTMEMBER**函数一起使用，或者与根据层次结构的 CURRENTMEMBER 返回不同的计算**集的计算****所得**集的函数。 例如，下面的查询返回所有日期（从日历年的开始到行轴上显示的日期）的 Internet Sales Amount 度量值的总和。  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
