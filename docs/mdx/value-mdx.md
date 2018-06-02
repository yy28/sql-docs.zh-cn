---
title: 值 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f1d30c54661602fc1f21d37c92480202533928c2
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582089"
---
# <a name="value-mdx"></a>Value (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回查询上下文中的属性层次结构的当前成员与 Measures 维度的当前成员的交集的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **值**函数返回字符串形式的指定成员的值。 **值**参数是可选的因为成员的值的默认属性的成员，并且如果未不指定任何其他值的成员返回的值。 有关成员的属性的详细信息，请参阅[内部成员属性&#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)和[用户定义成员属性&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [属性&#40;MDX&#41;](../mdx/properties-mdx.md)   
 [名称&#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
