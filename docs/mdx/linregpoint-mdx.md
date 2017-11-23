---
title: "LinRegPoint (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINREGPOINT
dev_langs: kbMDX
helpviewer_keywords: LinRegPoint function
ms.assetid: 28298d7c-2b8a-4423-ae52-9c2d6f0f0064
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d16da44758873659145058f9e5dab30fae8ff05c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  一组中，线性回归计算，并返回的值*y 轴截距*在回归行中，y = ax + b x 的特定值。  
  
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
  
## <a name="remarks"></a>注释  
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归行都有以下公式，其中是斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegPoint**函数的计算结果可获取 y 轴的值的第二个数值表达式对指定的集。 然后，此函数根据第三个数值表达式（如果已指定）对指定集求值，以获取 X 轴的值。 如果未指定第三个数值表达式，则该函数将使用指定集中单元的当前上下文作为 X 轴的值。 与时间维度经常使用未指定的 x 轴自变量。  
  
 一旦计算完线性回归线，即为第一个数值表达式计算等式的值，并且随后返回该值。  
  
> [!NOTE]  
>  **LinRegPoint**函数将忽略空单元格包含文本。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下例根据单位销售额和商店销售额之间的统计关系，依据过去十个时期的数据得出单位销售额的预测值。  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
