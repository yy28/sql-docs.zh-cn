---
title: IsAncestor (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5cc8352b0d087b54a623cce892a05dfed29258b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105263"
---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)


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
  
## <a name="remarks"></a>备注  
 **IsAncestor**函数将返回**true**如果指定的第一个成员是指定的第二个成员的祖先。 否则，该函数返回**false**。  
  
## <a name="example"></a>示例  
 下面的示例返回 **，则返回 true**如果 [Date]。 [会计]。CurrentMember 是 2003 年 1 月的祖先：  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [祖先&#40;MDX&#41;](../mdx/ancestor-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
