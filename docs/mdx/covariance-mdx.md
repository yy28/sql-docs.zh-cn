---
title: 协方差 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COVARIANCE
dev_langs:
- kbMDX
helpviewer_keywords:
- Covariance function
ms.assetid: 5faf6742-62db-4c5c-8797-096bf1cab273
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9c5ddb426c812027c7ec77e21bed1fdddce4d14c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
