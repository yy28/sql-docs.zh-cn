---
description: Covariance (MDX)
title: 协变 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32471a48f0a669f7b72b5946f07403d6851dfb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500530"
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
 **协方差**函数根据第一个数值表达式对指定的集求值，以获得 y 轴的值。 然后，此函数对指定的集计算第二个数值表达式（如果指定），以获得 x 轴的一组值。 如果未指定第二个数值表达式，此函数将使用指定集中单元的当前上下文作为 x 轴的值。  
  
 **协方差**函数使用有偏差总体公式。 这与 [CovarianceN](../mdx/covariancen-mdx.md) 函数相反，后者使用无偏差总体公式 (除以 x-y 对的数目，然后减去 1) 。  
  
> [!NOTE]  
>  **协变**函数忽略空单元或包含文本或逻辑值的单元格被忽略。 但是，该函数将包含值为零的单元。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
