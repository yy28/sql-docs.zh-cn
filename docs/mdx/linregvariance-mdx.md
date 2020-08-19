---
description: LinRegVariance (MDX)
title: LinRegVariance (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd223530c0b184dd723abbb68c2acccd1240d870
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477029"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  计算集的线性回归，并返回与回归线 y = ax + b 关联的方差。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归线具有以下公式，其中 a 为斜率，b 为截距：  
  
 y = ax+b  
  
 **LinRegVariance**函数对第一个数值表达式求值，以获得 y 轴的值。 然后，该函数根据第二个数值表达式计算指定集（如果已指定），以获得 X 轴的值。 如果未指定第二个数值表达式，则该函数使用指定集中的单元的当前上下文作为 X 轴的值。 不指定 x 轴参数经常与 Time 维度一起使用。  
  
 获取点集后， **LinRegVariance** 函数将返回描述线性方程与点的拟合度的统计方差。  
  
> [!NOTE]  
>  **LinRegVariance**函数将忽略空单元或包含文本或逻辑值的单元。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下例返回一个方差，该方差描述了单位销售额和商店销售额度量值的线性方程与点的拟合程度。  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
