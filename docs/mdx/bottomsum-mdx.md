---
title: BottomSum （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e49fc5a7ffd4c0adff38628a143ded695785e29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016888"
---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)


  按升序对指定集进行排序，并返回一个最小值元组集，这些元组的和等于或小于指定值。  
  
## <a name="syntax"></a>语法  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *值*  
 指定与每个元组相比较的值的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **BottomSum**函数计算对指定集求值的指定度量值的总和，按升序对集进行排序。 然后，此函数返回最小值元素，其指定数值表达式的合计至少为指定值（和）。 此函数返回集的最小子集，其累积合计至少为指定值。 返回的元素按从小到大的顺序排列。  
  
> [!IMPORTANT]  
>  **BottomSum**函数（如[TopSum](../mdx/topsum-mdx.md)函数）始终中断层次结构。  
  
## <a name="examples"></a>示例  
 以下示例返回 2003 会计年度 Geography 维度 Geography 层次结构中 City 级别的最小成员集（对于 Bike 类别），其使用 Reseller Sales Amount 度量值的累积合计至少是 50,000（从具有最小销售额的集的成员开始）：  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
