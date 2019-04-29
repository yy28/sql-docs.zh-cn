---
title: LinRegPoint (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc47b5910f0d5323b1b7e29cd3313b36d615265c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136084"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  对集进行线性回归计算，并返回的值*y 截距*中回归线，y = ax + b 表示特定的 x 值。  
  
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
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归线具有如下公式，其中是增量的斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegPoint**函数以获得 y 轴的值的第二个数值表达式对指定的集计算。 然后，此函数根据第三个数值表达式（如果已指定）对指定集求值，以获取 X 轴的值。 如果未指定第三个数值表达式，则该函数将使用指定集中单元的当前上下文作为 X 轴的值。 不指定 x 轴参数通常不对时间维度。  
  
 一旦计算完线性回归线，即为第一个数值表达式计算等式的值，并且随后返回该值。  
  
> [!NOTE]  
>  **LinRegPoint**函数将忽略空单元或包含文本的单元格。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下例根据单位销售额和商店销售额之间的统计关系，依据过去十个时期的数据得出单位销售额的预测值。  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
