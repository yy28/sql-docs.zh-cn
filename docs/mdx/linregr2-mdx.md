---
title: LinRegR2 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 42c703e703e8c557b4de8466a0cd1b686217fd4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136208"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  一组进行线性回归计算，并返回确定，R 系数<sup>2</sup>。  
  
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
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归线具有如下公式，其中是增量的斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegR2**函数计算指定的 setagainst 第一个数值 expressionto 获得 y 轴的值。 然后，该函数对指定集计算第二个数值表达式（如果指定）的值，以获得 X 轴的值。 如果未指定第二个数值 expressionis，该函数使用指定集中单元的当前上下文作为值在 x 轴。 不指定 x axisargument 通常不对时间维度。  
  
 获取点集后**LinRegR2**函数返回统计量 R<sup>2</sup> ，它描述线性方程与点的拟合度。  
  
> [!NOTE]  
>  **LinRegR2**函数将忽略空单元或单元格包含文本或逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下面的示例返回统计量 R<sup>2</sup> ，它描述线性回归方程与单元销售额和存储销售额度量值点的拟合度。  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
