---
title: CovarianceN (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 054acaaca417ca7d3fa5303fb31b5ea027bfcd72
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249603"
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)


  通过使用无偏差总体公式（除以 x-y 对的数目），返回对集求得的 x-y 值对的样本协方差。  
  
## <a name="syntax"></a>语法  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **CovarianceN**函数的第一个数值表达式，以获取 y 轴的值对指定的集计算。 然后，此函数对指定的集计算第二个数值表达式（如果指定），以获得 x 轴的一组值。 如果未指定第二个数值表达式，则该函数使用指定集中的单元的当前上下文作为 X 轴的值。  
  
 **CovarianceN**函数使用无偏差的总体公式。 这是与此相反[协方差](../mdx/covariance-mdx.md)函数使用有偏差的总体公式 （除以 x-y 对的数量）。  
  
> [!NOTE]  
>  **CovarianceN**函数将忽略空单元或单元格包含文本或逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
