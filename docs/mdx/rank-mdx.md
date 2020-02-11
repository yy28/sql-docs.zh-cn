---
title: Rank （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1081cacd0676f4eb0512780e9ddc7641edb99ca1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037067"
---
# <a name="rank-mdx"></a>Rank (MDX)


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
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**rank**函数通过对元组计算指定的数值表达式来确定指定元组的从1开始的秩。 如果指定了数值表达式，则**rank**函数会将相同的秩分配给具有该集内的重复值的元组。 为值相同的元组分配相同的排名，会影响该集中后续元组的排名。 例如，由以下元组组成的集：`{(a,b), (e,f), (c,d)}`。 元组 `(a,b)` 与元组 `(c,d)` 具有相同的值。 如果元组 `(a,b)` 的排名为 1，则 `(a,b)` 和 `(c,d)` 的排名都为 1。 但元组 `(e,f)` 的排名为 3。 此集中可能没有排名为 2 的元组。  
  
 如果未指定数值表达式， **Rank**函数将返回指定元组的序号位置（从1开始）。  
  
 **Rank**函数不会对集进行排序。  
  
## <a name="example"></a>示例  
 以下示例返回包含客户和采购日期的元组集，方法是使用**筛选器**、**非空**的、**项**和**排名**函数来查找每个客户购买的最后日期。  
  
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
  
 下面的示例使用**Order**函数（而不是**排名**函数）根据 "分销商销售额" 度量值对 City 层次结构的成员进行排序，然后按排名顺序显示它们。 通过使用**order**函数对 City 层次结构的成员集进行第一次排序，排序只完成一次，然后在呈现排序顺序之前进行线性扫描。  
  
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
 [&#40;MDX&#41;顺序](../mdx/order-mdx.md)   
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
