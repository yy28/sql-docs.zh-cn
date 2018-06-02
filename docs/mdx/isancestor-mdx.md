---
title: IsAncestor (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59c997398ce7a3e4477136d1c5ef2ebcd2686e2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578619"
---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回一个指定成员是否为另一个指定成员的祖先。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsAncestor(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression1*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Member_Expression2*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **IsAncestor**函数返回**true**如果指定的第一个成员为指定的第二个成员的祖先。 否则，该函数返回**false**。  
  
## <a name="example"></a>示例  
 下面的示例返回**true**如果 [Date]。 [会计]。CurrentMember 是 2003 年 1 月的祖先：  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [上级&#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
