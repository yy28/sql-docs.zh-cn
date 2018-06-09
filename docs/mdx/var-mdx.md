---
title: Var (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14caf6e96b41fdf2e7f8b4d20f16852e890bd166
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743916"
---
# <a name="var-mdx"></a>Var (MDX)


  返回数值表达式对集求得使用无偏差的总体公式的样本方差 (除以*n*)。  
  
## <a name="syntax"></a>语法  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **Var**函数返回指定数值表达式对指定集求得的公平的方差。  
  
 **Var**函数使用无偏差的总体公式中，与[VarP](../mdx/varp-mdx.md)函数使用有偏差的总体公式。  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
