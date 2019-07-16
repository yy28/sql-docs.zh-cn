---
title: 协方差 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3755fb103362b797735d74c9cbe67523aace59
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047196"
---
# <a name="covariance-mdx"></a>Covariance (MDX)


  返回使用有偏差总体公式（除以 x-y 对的数目）对集求得的 x-y 值对的总体协方差。  
  
## <a name="syntax"></a>语法  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **协方差**函数的第一个数值表达式，以获取 y 轴的值对指定的集计算。 然后，此函数对指定的集计算第二个数值表达式（如果指定），以获得 x 轴的一组值。 如果未指定第二个数值 expressionis，该函数使用指定集中单元的当前上下文作为值在 x 轴。  
  
 **协方差**函数使用有偏差的总体公式。 这是与此相反[CovarianceN](../mdx/covariancen-mdx.md)函数，它使用无偏差的总体公式 （除以 x-y 对的数目，然后再减 1）。  
  
> [!NOTE]  
>  **协方差**函数将忽略空单元格包含文本或将忽略逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下面的示例说明如何使用 Covariance 函数：  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
