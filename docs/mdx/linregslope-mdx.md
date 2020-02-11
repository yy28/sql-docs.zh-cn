---
title: LinRegSlope （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6d43d2ccc961e465c5430c525fd6178d74e29ca9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905539"
---
# <a name="linregslope-mdx"></a>LinRegSlope (MDX)


  计算集的线性回归，并返回回归线公式 y = ax + b 中斜率的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegSlope**函数根据第一个数值表达式对指定的集求值，以获得 y 轴的值。 然后，此函数根据第二个数值表达式（如果已指定）对指定的集表达式求值，以获取 X 轴的值。 如果未指定第二个数值表达式，则此函数使用指定集中的单元的当前上下文作为 X 轴的值。 不指定 x 轴参数经常与 Time 维度一起使用。  
  
 获取点集后， **LinRegSlope**函数将返回回归线的斜率（上一个公式中的）。  
  
> [!NOTE]  
>  **LinRegSlope**函数将忽略空单元或包含文本或逻辑值的单元。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下面的示例返回单位销售额和商店销售额度量值的回归线的斜率。  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
