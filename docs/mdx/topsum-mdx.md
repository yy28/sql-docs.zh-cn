---
title: TopSum （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5bbcfe52e62757ea00427eb9fd6ed979eb8d32e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097391"
---
# <a name="topsum-mdx"></a>TopSum (MDX)


  对集进行排序并返回累计合计至少达到指定值的最前面的元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *值*  
 指定与每个元组相比较的值的有效数值表达式。  
  
 *Numeric_Expression*  
 返回度量值的有效数值表达式，通常是多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **TopSum**函数计算对指定集求值的指定度量值的总和，并按降序对集进行排序。 然后，该函数返回最大值元素，其指定数值表达式的合计至少为指定值。 此函数返回集的最小子集，其累积合计至少为指定值。 返回的元素按从大到小的顺序排序。  
  
> [!IMPORTANT]  
>  与[BottomSum](../mdx/bottomsum-mdx.md)函数一样， **TopSum**函数始终中断层次结构。  
  
## <a name="example"></a>示例  
 下面的示例返回 Geography 维度中 Geography 层次结构内 City 级别的最小成员集（对于 Bike 类别），使用 Reseller Sales Amount 度量值时该集的累积合计至少为 6,000,000（从集中具有最大销售额的成员开始）。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
