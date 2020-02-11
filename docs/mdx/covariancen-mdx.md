---
title: CovarianceN （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 796dc37127eba984477aef628e4ae9161db4637e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047179"
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
 **CovarianceN**函数根据第一个数值表达式对指定的集求值，以获得 y 轴的值。 然后，此函数对指定的集计算第二个数值表达式（如果指定），以获得 x 轴的一组值。 如果未指定第二个数值表达式，则该函数使用指定集中的单元的当前上下文作为 X 轴的值。  
  
 **CovarianceN**函数使用无偏差总体公式。 这与使用有偏差总体公式（除以 x-y 对的数目）的[协方差](../mdx/covariance-mdx.md)函数相反。  
  
> [!NOTE]  
>  **CovarianceN**函数将忽略空单元或包含文本或逻辑值的单元。 但是，该函数将包含值为零的单元。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
