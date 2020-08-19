---
description: LinRegPoint (MDX)
title: LinRegPoint (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f298d58b14f3005b86f8fa7773a4faef1c94c79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429839"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  对集进行线性回归计算，并返回回归线公式 y = ax + b 中 *y 截距* 的值，以指定 x 的特定值。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>参数  
 *Slice_Expression_x*  
 一个有效的数值表达式，通常为返回一个数值（该数值表示切片轴的值）的单元坐标的多维表达式 (MDX)。  
  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归线具有以下公式，其中 a 为斜率，b 为截距：  
  
 y = ax+b  
  
 **LinRegPoint**函数根据第二个数值表达式对指定的集求值，以获得 y 轴的值。 然后，此函数根据第三个数值表达式（如果已指定）对指定集求值，以获取 X 轴的值。 如果未指定第三个数值表达式，则该函数将使用指定集中单元的当前上下文作为 X 轴的值。 不指定 x 轴参数经常与 Time 维度一起使用。  
  
 一旦计算完线性回归线，即为第一个数值表达式计算等式的值，并且随后返回该值。  
  
> [!NOTE]  
>  **LinRegPoint**函数将忽略空单元或包含文本的单元格。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下例根据单位销售额和商店销售额之间的统计关系，依据过去十个时期的数据得出单位销售额的预测值。  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
