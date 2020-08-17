---
description: Stdev (MDX)
title: Stdev (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e443cd7be9301dc5b5907e49fd967b1507feae03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386943"
---
# <a name="stdev-mdx"></a>Stdev (MDX)


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
  
## <a name="remarks"></a>备注  
 **Stdev**函数使用无偏差总体公式，而[StdevP](../mdx/stdevp-mdx.md)函数使用有偏差总体公式。  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
