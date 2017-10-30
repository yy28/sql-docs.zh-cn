---
title: "值 (MDX) |Microsoft 文档"
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
- Value
dev_langs:
- kbMDX
helpviewer_keywords:
- Value function
ms.assetid: ff76628e-2d49-49f6-a6cb-f6da07d83d65
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63e24e0f701332747e3129a57768bfe1b6fbb45d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="value-mdx"></a>Value (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  返回查询上下文中的属性层次结构的当前成员与 Measures 维度的当前成员的交集的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 **值**函数返回字符串形式的指定成员的值。 **值**参数是可选的因为成员的值的默认属性的成员，并且如果未不指定任何其他值的成员返回的值。 有关成员的属性的详细信息，请参阅[内部成员属性 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md)和[用户定义的成员属性 &#40;MDX &#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MemberValue &#40;MDX &#41;](../mdx/membervalue-mdx.md)   
 [属性 &#40;MDX &#41;](../mdx/properties-mdx.md)   
 [名称 &#40;MDX &#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX &#41;](../mdx/uniquename-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

