---
title: "LinRegVariance (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LINREGVARIANCE
dev_langs:
- kbMDX
helpviewer_keywords:
- LinRegVariance function
ms.assetid: 09803510-2d71-401b-970e-bbdcac06558d
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 30ce6e0e7f43be71824734b7ab9790007a9f4763
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  一组中，线性回归计算，并返回与回归线，关联的方差 y = ax + b。  
  
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
  
## <a name="remarks"></a>注释  
 线性回归使用最小二乘法，可以计算出回归线（即一系列点的最佳拟合线）的公式。 回归行都有以下公式，其中是斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegVariance**函数的计算结果指定的 setagainst 获取 y 轴的值的第一个数值表达式。 如果指定，以获取 x 轴的值，则函数然后计算结果指定的 setagainst 的第二个数值表达式。 如果未指定第二个数值 expressionis，该功能将用作值具有 x 轴中指定集的单元格的当前上下文。 与时间维度经常使用未指定的 x 轴自变量。  
  
 获取组点之后, **LinRegVariance**函数将返回描述最适合的线性方程式与点状态的统计方差。  
  
> [!NOTE]  
>  **LinRegVariance**函数将忽略空单元格包含文本或逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="example"></a>示例  
 下例返回一个方差，该方差描述了单位销售额和商店销售额度量值的线性方程与点的拟合程度。  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

