---
title: BottomCount （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd09c823e09270ebf7c9851b3c6760baf720db39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016956"
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)


  按升序对集进行排序，并返回指定集中具有最小值的指定数目的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则此函数根据在指定集中计算出的指定数值表达式的值，对指定集中的元组按升序进行排序。 然后， **BottomCount**函数返回具有最小值的指定数目的元组。  
  
> [!IMPORTANT]  
>  **BottomCount**函数（如[TopCount](../mdx/topcount-mdx.md)函数）始终中断层次结构。  
  
 如果未指定数值表达式，则函数将以自然顺序返回成员集，而不进行任何排序，行为类似于[Tail （MDX）](../mdx/tail-mdx.md)函数。  
  
## <a name="example"></a>示例  
 下例将返回每个日历年中最后五个“产品子类别”销售额的“分销商订单数量”度量值，并根据“分销商销售额”度量值进行排序。  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
