---
title: Sum (MDX) |Microsoft 文档
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
- SUM
dev_langs:
- kbMDX
helpviewer_keywords:
- Sum function [MDX]
ms.assetid: 6c3db1e3-2c02-49f2-a0bf-cab0fb78c622
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4ca31da42f2a8b41ab4c4247ea0b6d33759b6e3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sum-mdx"></a>Sum (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>注释  
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
  
 下面的示例使用与成员关键字和**总和**函数定义中包含的 Country 属性层次结构中 Geography 维度的加拿大和美国成员的 Reseller Sales Amount 度量值之和的度量值维度的计算的成员。  
  
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
  
 通常情况下，**总和**函数用于处理**CURRENTMEMBER**函数或功能，例如**YTD**返回一组的层次结构 currentmember 而异。 例如，下面的查询返回所有日期（从日历年的开始到行轴上显示的日期）的 Internet Sales Amount 度量值的总和。  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
