---
title: StdevP (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14117ed4a3e3e7afc0152c5e659d1c7f040957e9
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742926"
---
# <a name="stdevp-mdx"></a>StdevP (MDX)


  返回数值表达式对集求得使用有偏差的总体公式计算总体标准偏差 (除以*n*)。  
  
## <a name="syntax"></a>语法  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **StdevP**函数使用有偏差的总体公式、 时[Stdev](../mdx/stdev-mdx.md)函数使用无偏差的总体公式。  
  
## <a name="example"></a>示例  
 下面的示例将使用有偏差总体公式返回对 2003 日历年度中前三个月求得的 Internet Order Quantity 的标准偏差。  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
