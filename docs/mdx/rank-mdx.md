---
title: 排名 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d234f02c8dfcd36073059210c1999cb95f5ab0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200661"
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
 如果指定了数值表达式，则**排名**函数通过计算指定数值表达式对元组来确定指定的元组基于 1 的秩。 如果指定了数值表达式，则**排名**函数的一组中的重复值元组分配相同的排名。 为值相同的元组分配相同的排名，会影响该集中后续元组的排名。 例如，由以下元组组成的集：`{(a,b), (e,f), (c,d)}`。 元组 `(a,b)` 与元组 `(c,d)` 具有相同的值。 如果元组 `(a,b)` 的排名为 1，则 `(a,b)` 和 `(c,d)` 的排名都为 1。 但元组 `(e,f)` 的排名为 3。 此集中可能没有排名为 2 的元组。  
  
 如果未指定数值表达式，**排名**函数将返回指定元组的基于 1 的序号位置。  
  
 **排名**函数不会对集进行排序。  
  
## <a name="example"></a>示例  
 下面的示例返回包含客户和采购日期，通过使用元组集**筛选器**， **NonEmpty**，**项**，和**排名**函数来查找最后一个日期，每个客户购买。  
  
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
  
 下面的示例使用**顺序**函数，而不是**排名**函数，City 层次结构的成员排名根据 Reseller Sales Amount 度量值，然后按照排名高低显示它们。 通过使用**顺序**函数先对 City 层次结构的成员的集，排序是仅执行一次，并再后跟线性扫描之前显示按排序顺序。  
  
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
  
## <a name="see-also"></a>请参阅  
 [订单&#40;MDX&#41;](../mdx/order-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
