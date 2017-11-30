---
title: "级别 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: RANK
dev_langs: kbMDX
helpviewer_keywords: Rank function [MDX]
ms.assetid: 3cea35ed-57c4-4b47-a736-cee00275509b
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ba556f2a298ea65ff2d9662a8deba90334d31a0f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="rank-mdx"></a>Rank (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定元组在指定集中的排名（从 1 开始）。  
  
## <a name="syntax"></a>语法  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果指定数值表达式，则**级别**函数将确定通过对此元组指定的数值表达式求值的指定元组 1 为基的秩。 如果指定数值表达式，则**级别**函数将相同的排名指派给与集合中的重复值的元组。 为值相同的元组分配相同的排名，会影响该集中后续元组的排名。 例如，由以下元组组成的集：`{(a,b), (e,f), (c,d)}`。 元组 `(a,b)` 与元组 `(c,d)` 具有相同的值。 如果元组 `(a,b)` 的排名为 1，则 `(a,b)` 和 `(c,d)` 的排名都为 1。 但元组 `(e,f)` 的排名为 3。 此集中可能没有排名为 2 的元组。  
  
 如果未指定数值表达式，**级别**函数将返回指定元组的基于 1 的序号位置。  
  
 **级别**函数未排序集。  
  
## <a name="example"></a>示例  
 下面的示例返回包含客户和购买日期，使用元组的一套**筛选器**， **NonEmpty**，**项**，和**级别**函数来查找每个客户购买过的最后日期。  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用**顺序**函数，而不是**级别**函数，进行排名，城市层次结构的成员基于 Reseller Sales Amount 度量值，然后按排序顺序显示它们。 通过使用**顺序**函数到第一个订单的市/县层次结构的成员组成的集，排序仅一次执行，并对后跟线性扫描之前要呈现在排序顺序。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [顺序 &#40;MDX &#41;](../mdx/order-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
