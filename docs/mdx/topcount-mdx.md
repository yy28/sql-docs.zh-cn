---
title: TopCount （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e0f607f3111c150bff3d5dc562c77901a381bedc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036603"
---
# <a name="topcount-mdx"></a>TopCount (MDX)


  按降序对集进行排序，并返回指定数目的最大值元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**TopCount**函数将根据由数值表达式指定的值（根据指定集进行计算），按降序对指定集指定的集内的元组进行排序。 对集进行排序后， **TopCount**函数将返回指定数量的具有最高值的元组。  
  
> [!IMPORTANT]  
>  与[BottomCount](../mdx/bottomcount-mdx.md)函数一样， **TopCount**函数始终中断层次结构。  
  
 如果未指定数值表达式，则函数将以自然顺序返回成员集，而不进行任何排序，行为类似于[Head （MDX）](../mdx/head-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例按 Internet Sales Amount 返回前 10 个日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下面的示例返回 Bike 类别包含 Geography 维度中 Geography 层次结构的 City 级别的所有成员组合的集中的前五个成员，并按照 Reseller Sales Amount 度量值进行排序（从成员集中销售额最高的成员开始）。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
