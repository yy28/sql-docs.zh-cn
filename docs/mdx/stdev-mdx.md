---
title: Stdev (MDX) |Microsoft 文档
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
- STDEV
dev_langs:
- kbMDX
helpviewer_keywords:
- Stdev function [MDX]
ms.assetid: c3e31763-18ca-4a2b-bc03-3ee777970c68
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 14f4fbb734c2aa67b21f7016e83416a4d90219a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stdev-mdx"></a>Stdev (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回数值表达式用无偏差总体公式（除以 n-1）对集求得的样本标准偏差。  
  
## <a name="syntax"></a>语法  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **Stdev**函数使用无偏差的总体公式、 时[StdevP](../mdx/stdevp-mdx.md)函数使用有偏差的总体公式。  
  
## <a name="example"></a>示例  
 下例将使用无偏差总体公式返回对日历年 2003 的前三个月求得的 Internet Order Quantity 的标准偏差。  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
