---
description: LinRegR2 (MDX)
title: LinRegR2 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 748b332d7925313c5b5d8c1d3dfe868e3eb3e9cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429819"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  计算集的线性回归并返回确定系数 R<sup>2</sup>。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegR2**函数将计算指定的 setagainst 第一个数值 expressionto 获取 y 轴的值。 然后，该函数对指定集计算第二个数值表达式（如果指定）的值，以获得 X 轴的值。 如果未指定第二个数值表达式，则该函数使用指定集中的单元的当前上下文作为 X 轴的值。 通常不对时间维度指定 X 轴 参数。  
  
 获取点集后， **LinRegR2** 函数将返回统计 R<sup>2</sup> ，该统计说明了线性方程与点的拟合度。  
  
> [!NOTE]  
>  **LinRegR2**函数将忽略空单元或包含文本或逻辑值的单元。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下面的示例返回统计 R<sup>2</sup> ，该统计说明将线性回归公式拟合到 unit sales 和商店销售度量值的位置。  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
