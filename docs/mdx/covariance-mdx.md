---
title: 协方差 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b86c47b5da75c44d528f77a60e8168fd8b2260
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577879"
---
# <a name="covariance-mdx"></a>Covariance (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 **协方差**函数的计算结果的第一个数值表达式，以获取 y 轴的值针对指定的集。 然后，此函数对指定的集计算第二个数值表达式（如果指定），以获得 x 轴的一组值。 如果未指定第二个数值 expressionis，该功能会将指定集的单元格的当前上下文值用作 x 轴中。  
  
 **协方差**函数使用有偏差的总体公式。 这是与此相反[CovarianceN](../mdx/covariancen-mdx.md)使用无偏差的总体公式 （x，y 对的数目除以然后数减去 1） 的函数。  
  
> [!NOTE]  
>  **协方差**函数将忽略空单元格包含文本或逻辑值将被忽略。 但是，该函数将包含值为零的单元。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
