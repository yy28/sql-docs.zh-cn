---
description: Var (MDX)
title: Var (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 46aad9a9b7c328d23680df3c74bcf09a465b868d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483710"
---
# <a name="var-mdx"></a>Var (MDX)


  返回数值表达式对集求得的样本方差（使用无偏差总体公式 (除以 *n*) 。  
  
## <a name="syntax"></a>语法  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **Var**函数返回指定数值表达式对指定集求得的无偏差方差。  
  
 **Var**函数使用无偏差总体公式，而[VarP](../mdx/varp-mdx.md)函数使用有偏差总体公式。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
