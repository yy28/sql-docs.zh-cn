---
title: TopCount (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa8edcf8af510a41affdcbcc9924edf69cf4c220
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743216"
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
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 如果指定数值表达式，则**TopCount**函数以降序顺序，指定通过根据指定的数值表达式的值指定一组为指定集求得集中的元组排序。 对集进行排序之后**TopCount**函数然后返回指定的数目的具有最高值的元组。  
  
> [!IMPORTANT]  
>  如[BottomCount](../mdx/bottomcount-mdx.md)函数， **TopCount**函数始终中断层次结构。  
  
 如果未指定数值表达式，函数将返回成员组成的集在自然顺序排序，不进行任何排序，如行为[头 (MDX)](../mdx/head-mdx.md)函数。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
