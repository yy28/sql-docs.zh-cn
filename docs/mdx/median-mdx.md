---
title: 中值（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b6f941e269bb9948dd39ba52db0ea4d0961c029a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68033851"
---
# <a name="median-mdx"></a>Median (MDX)


  返回对集求值的数值表达式的中值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则对集计算指定数值表达式的值，然后返回求得的中值。 如果没有指定数值表达式，则在指定集成员的当前上下文中计算指定集，然后返回求得的中值。  
  
 中值是一组有序数值的中间值。 （中值不同于平均值，平均值是一组数值的总和除以这组数值的个数所得的值）。 中值是通过选择最小值以使这组数值中至少有一半值不大于所选的值来确定的。 如果这组数值的个数为奇数，则中值对应于单个值。 如果这组数值的个数为偶数，则中值对应于两个中间值的和除以 2 所得的值。  
  
> [!NOTE]  
>  计算一组有序数值的中值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略空值。  
  
## <a name="example"></a>示例  
 下例将返回 Adventure Works 多维数据集中每个季度、每个子类别和每个国家（地区）的每月销售额中值。  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
