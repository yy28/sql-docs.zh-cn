---
description: Value (MDX)
title: " (MDX) 的值 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3d6bf8edd7cbeefefa723c1acc374daa8d2c9407
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449609"
---
# <a name="value-mdx"></a>Value (MDX)


  返回查询上下文中的属性层次结构的当前成员与 Measures 维度的当前成员的交集的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **值**函数将指定成员的值作为字符串返回。 **值**参数是可选的，因为成员的值是成员的默认属性，并且是在没有指定其他值时为成员返回的值。 有关成员属性的详细信息，请参阅 [&#41;&#40;Mdx 成员属性 ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 和 [用户定义的成员属性 &#40;mdx&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)。  
  
## <a name="examples"></a>示例  
 下例将返回成员值并显式返回该成员的名称。  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 下例将以轴上成员的默认返回值返回成员值。  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [MDX&#41;&#40;属性 ](../mdx/properties-mdx.md)   
 [MDX &#40;名称&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
